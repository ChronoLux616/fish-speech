<div align="center">
<h1>Fish Speech</h1>

**English** | [简体中文](docs/README.zh.md) | [Portuguese](docs/README.pt-BR.md) | [日本語](docs/README.ja.md) | [한국어](docs/README.ko.md) | [Español](docs/README.es.md) <br>

<a href="https://www.producthunt.com/posts/fish-speech-1-4?embed=true&utm_source=badge-featured&utm_medium=badge&utm_souce=badge-fish&#0045;speech&#0045;1&#0045;4" target="_blank">
    <img src="https://api.producthunt.com/widgets/embed-image/v1/featured.svg?post_id=488440&theme=light" alt="Fish&#0032;Speech&#0032;1&#0046;4 - Open&#0045;Source&#0032;Multilingual&#0032;Text&#0045;to&#0045;Speech&#0032;with&#0032;Voice&#0032;Cloning | Product Hunt" style="width: 250px; height: 54px;" width="250" height="54" />
</a>
<a href="https://trendshift.io/repositories/7014" target="_blank">
    <img src="https://trendshift.io/api/badge/repositories/7014" alt="fishaudio%2Ffish-speech | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/>
</a>
<br>
</div>
<br>

<div align="center">
    <img src="https://count.getloli.com/get/@fish-speech?theme=asoul" /><br>
</div>

<br>

<div align="center">
    <a target="_blank" href="https://discord.gg/Es5qTB9BcN">
        <img alt="Discord" src="https://img.shields.io/discord/1214047546020728892?color=%23738ADB&label=Discord&logo=discord&logoColor=white&style=flat-square"/>
    </a>
    <a target="_blank" href="https://hub.docker.com/r/fishaudio/fish-speech">
        <img alt="Docker" src="https://img.shields.io/docker/pulls/fishaudio/fish-speech?style=flat-square&logo=docker"/>
    </a>
    <a target="_blank" href="https://huggingface.co/spaces/fishaudio/fish-speech-1">
        <img alt="Huggingface" src="https://img.shields.io/badge/🤗%20-space%20demo-yellow"/>
    </a>
</div>

Este código fuente y todos los modelos se publican bajo la licencia CC-BY-NC-SA-4.0. Consulte el archivo [LICENSE](LICENSE) para más detalles.

---

## Características

1. **TTS de cero y pocos ejemplos**: Ingresa una muestra vocal de 10 a 30 segundos para generar una salida TTS de alta calidad. **Para obtener instrucciones detalladas, consulta [Mejores Prácticas para Clonación de Voz](https://docs.fish.audio/text-to-speech/voice-clone-best-practices).**

2. **Soporte Multilingüe y Cruzado entre Idiomas**: Simplemente copia y pega texto multilingüe en el cuadro de entrada, sin preocuparte por el idioma. Actualmente soporta inglés, japonés, coreano, chino, francés, alemán, árabe y español.

3. **Sin Dependencia de Fonemas**: El modelo tiene una gran capacidad de generalización y no depende de fonemas para TTS. Puede procesar texto en cualquier sistema de escritura.

4. **Alta Precisión**: Logra una baja tasa de error de caracteres (CER) y de error de palabras (WER) de alrededor del 2 % en textos en inglés de 5 minutos.

5. **Rápido**: Con aceleración fish-tech, el factor de tiempo real es aproximadamente 1:5 en una laptop con Nvidia RTX 4060 y 1:15 en una Nvidia RTX 4090.

6. **Inferencia en WebUI**: Ofrece una interfaz web fácil de usar basada en Gradio, compatible con Chrome, Firefox, Edge y otros navegadores.

7. **Inferencia en GUI**: Incluye una interfaz gráfica PyQt6 que funciona sin problemas con el servidor API. Compatible con Linux, Windows y macOS. [Ver GUI](https://github.com/AnyaCoder/fish-speech-gui).

8. **Fácil de Desplegar**: Permite configurar un servidor de inferencia con soporte nativo para Linux, Windows y macOS, minimizando la pérdida de velocidad.

## Aviso legal

No asumimos ninguna responsabilidad por el uso ilegal de este código fuente. Consulte las leyes locales sobre DMCA y otras leyes relacionadas.

## Demostración en Línea

[Fish Audio](https://fish.audio)

## Inicio Rápido para Inferencia Local

[inference.ipynb](/inference.ipynb)

## Videos

#### V1.4 Vídeo de demostración: [Youtube](https://www.youtube.com/watch?v=Ghc8cJdQyKQ)

## Documentos

- [English](https://speech.fish.audio/)
- [中文](https://speech.fish.audio/zh/)
- [日本語](https://speech.fish.audio/ja/)
- [Portuguese (Brazil)](https://speech.fish.audio/pt/)

## Muestras (2024/10/02 V1.4)

- [English](https://speech.fish.audio/samples/)
- [中文](https://speech.fish.audio/zh/samples/)
- [日本語](https://speech.fish.audio/ja/samples/)
- [Portuguese (Brazil)](https://speech.fish.audio/pt/samples/)

## Créditos

- [VITS2 (daniilrobnikov)](https://github.com/daniilrobnikov/vits2)
- [Bert-VITS2](https://github.com/fishaudio/Bert-VITS2)
- [GPT VITS](https://github.com/innnky/gpt-vits)
- [MQTTS](https://github.com/b04901014/MQTTS)
- [GPT Fast](https://github.com/pytorch-labs/gpt-fast)
- [GPT-SoVITS](https://github.com/RVC-Boss/GPT-SoVITS)

## Patrocinador

<div>
  <a href="https://6block.com/">
    <img src="https://avatars.githubusercontent.com/u/60573493" width="100" height="100" alt="6Block Avatar"/>
  </a>
  <br>
  <a href="https://6block.com/">Patrocinador del procesamiento de datos por 6Block</a>
</div>
<div>
  <a href="https://www.lepton.ai/">
    <img src="https://www.lepton.ai/favicons/apple-touch-icon.png" width="100" height="100" alt="Lepton Avatar"/>
  </a>
  <br>
  <a href="https://www.lepton.ai/">Fish Audio se ofrece en Lepton.AI</a>
</div>