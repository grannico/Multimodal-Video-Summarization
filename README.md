# Multimodal-Video-Summarization
Pipeline multimodale per l’analisi e la summarization automatica di video tecnici tramite UniVTG, Video-LLaVA e Whisper. Caso studio: contenuti YouTube forniti da Benelli Armi.

Questo repository contiene i materiali di un progetto universitario dedicato alla **video summarization automatica** di contenuti informativi e tecnici, tramite l’utilizzo di modelli multimodali di ultima generazione.

Il sistema combina l’estrazione di clip salienti (UniVTG) con modelli di generazione testuale visivo-linguistici (Video-LLaVA) e modelli alternativi basati su audio e immagini (Whisper + BLIP).

## 📁 Contenuti

- `relazione.pdf` — Relazione completa del progetto
- `presentazione.pdf` — Slide finali
- `Notebook_Colab_UniVTG.ipynb` — Notebook per l’estrazione automatica delle clip salienti
- `cli.py` — File modificato da `videollava/serve/cli.py` per l'inferenza batch
- `outputs/` — Esempi di output generati (JSON, TXT) e ground trouth

---

## 🔗 Repository e modelli utilizzati

| Componente     | Repository originale                          |
|----------------|-----------------------------------------------|
| UniVTG         | https://github.com/showlab/UniVTG             |
| Video-LLaVA    | https://huggingface.co/LanguageBind/Video-LLaVA-7B |
| Whisper        | https://github.com/openai/whisper             |
| BLIP           | https://github.com/salesforce/BLIP            |

---

## ⚙️ Estrazione delle clip con UniVTG

L’estrazione delle clip salienti è stata realizzata tramite un **notebook Colab**, `Notebook_Colab_UniVTG.ipynb`, che:

1. Analizza il video fornito
2. Estrae i frame più significativi tramite UniVTG
3. Genera automaticamente le clip tramite `ffmpeg`

I parametri principali (durata clip, framerate, top-k segmenti) vengono calcolati dinamicamente in base alla lunghezza del video.

---

## 🖥️ Inferenza testuale con Video-LLaVA (da terminale)

Per generare descrizioni testuali sulle clip, è stato utilizzato il comando:

```bash
python -m videollava.serve.cli \
  --model-path LanguageBind/Video-LLaVA-7B \
  --input-dir "/home/vrai/videollava/clip_output_univtg/clip_video_10" \
  --output-json "/home/vrai/videollava/descr_output/video 10/video_10.json" \
  --output-txt "/home/vrai/videollava/descr_output/video 10/video_10.txt"
