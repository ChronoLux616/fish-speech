# Ajuste fino

Evidentemente, al abrir esta página, no estabas satisfecho con el rendimiento del modelo preentrenado de pocos ejemplos. Quieres ajustar finamente un modelo para mejorar su desempeño en tu conjunto de datos.

En la versión actual, solo necesitas ajustar finamente la parte de 'LLAMA'.

## Ajuste fino de LLAMA
### 1. Preparar el conjunto de datos

```
.
├── SPK1
│   ├── 21.15-26.44.lab
│   ├── 21.15-26.44.mp3
│   ├── 27.51-29.98.lab
│   ├── 27.51-29.98.mp3
│   ├── 30.1-32.71.lab
│   └── 30.1-32.71.mp3
└── SPK2
    ├── 38.79-40.85.lab
    └── 38.79-40.85.mp3
```

Debes convertir tu conjunto de datos al formato mencionado anteriormente y colocarlo en la carpeta `data`. Los archivos de audio pueden tener las extensiones `.mp3`, `.wav` o `.flac`, y el archivo de anotaciones debe tener la extensión `.lab`.

!!! info "Dataset Format"
    El archivo de anotaciones `.lab` solo necesita contener la transcripción del audio, sin ningún formato especial. Por ejemplo, si `hi.mp3` dice "Hola, adiós," entonces el archivo `hi.lab` contendría una sola línea de texto: "Hola, adiós."

!!! advertencia
    Es recomendable aplicar normalización de volumen al conjunto de datos. Puedes usar [fish-audio-preprocess](https://github.com/fishaudio/audio-preprocess) para hacerlo.

    ```bash
    fap loudness-norm data-raw data --clean
    ```


### 2. Extracción por lotes de tokens semánticos

Asegúrate de haber descargado VQGAN weights. Si no lo has hecho, ejecuta el siguiente comando:

```bash
huggingface-cli download fishaudio/fish-speech-1.4 --local-dir checkpoints/fish-speech-1.4
```

Luego, puedes ejecutar el siguiente comando para extraer los tokens semánticos:

```bash
python tools/vqgan/extract_vq.py data \
    --num-workers 1 --batch-size 16 \
    --config-name "firefly_gan_vq" \
    --checkpoint-path "checkpoints/fish-speech-1.4/firefly-gan-vq-fsq-8x1024-21hz-generator.pth"
```

!!! nota
    Puedes ajustar `--num-workers` y `--batch-size` para aumentar la velocidad de extracción, pero asegúrate de no exceder el límite de memoria de tu GPU.
    Para el formato VITS, puedes especificar una lista de archivos usando `--filelist xxx.list`.

Este comando creará archivos `.npy` en el directorio `data`, como se muestra a continuación:

```
.
├── SPK1
│   ├── 21.15-26.44.lab
│   ├── 21.15-26.44.mp3
│   ├── 21.15-26.44.npy
│   ├── 27.51-29.98.lab
│   ├── 27.51-29.98.mp3
│   ├── 27.51-29.98.npy
│   ├── 30.1-32.71.lab
│   ├── 30.1-32.71.mp3
│   └── 30.1-32.71.npy
└── SPK2
    ├── 38.79-40.85.lab
    ├── 38.79-40.85.mp3
    └── 38.79-40.85.npy
```

### 3. Empaqueta el conjunto de datos en formato protobuf.

```bash
python tools/llama/build_dataset.py \
    --input "data" \
    --output "data/protos" \
    --text-extension .lab \
    --num-workers 16
```

Después de que el comando haya terminado de ejecutarse, deberías ver el archivo `quantized-dataset-ft.protos` en el directorio `data`.

### 4. Finalmente, ajuste fino con LoRA.

De manera similar, asegúrate de haber descargado `LLAMA` weights. Si no lo has hecho, ejecuta el siguiente comando:

```bash
huggingface-cli download fishaudio/fish-speech-1.4 --local-dir checkpoints/fish-speech-1.4
```

Por último, puedes iniciar el ajuste fino ejecutando el siguiente comando:

```bash
python fish_speech/train.py --config-name text2semantic_finetune \
    project=$project \
    +lora@model.model.lora_config=r_8_alpha_16
```

!!! nota
    Puedes modificar los parámetros de entrenamiento, como `batch_size`, `gradient_accumulation_steps`, etc. para ajustarlos a la memoria de tu GPU editando el archivo `fish_speech/configs/text2semantic_finetune.yaml`.

!!! nota
    Para usuarios de Windows, puedes usar `trainer.strategy.process_group_backend=gloo` para evitar problemas con `nccl`.

Una vez completado el entrenamiento, puedes consultar la sección de [inferencia](inference.md) para generar el habla.

!!! info
    De forma predeterminada, el modelo solo aprenderá los patrones de habla del hablante y no el timbre. Aún necesitarás usar prompts para garantizar la estabilidad del timbre.
    Si deseas que el modelo aprenda el timbre, puedes aumentar el número de pasos de entrenamiento, pero esto podría provocar sobreajuste (overfitting).

Después del entrenamiento, debes convertir los pesos de LoRA en pesos regulares antes de realizar la inferencia.

```bash
python tools/llama/merge_lora.py \
	--lora-config r_8_alpha_16 \
	--base-weight checkpoints/fish-speech-1.4 \
	--lora-weight results/$project/checkpoints/step_000000010.ckpt \
	--output checkpoints/fish-speech-1.4-yth-lora/
```
!!! nota
    También puedes probar otros puntos de control (checkpoints). Se sugiere usar el punto de control más temprano que cumpla con tus requisitos, ya que suelen tener un mejor rendimiento en datos fuera de la distribución (OOD).
