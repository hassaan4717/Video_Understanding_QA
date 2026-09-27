# Video Understanding QA

Video Understanding QA is a Gradio application for asking natural-language questions about the visual content of a video. It samples frames from an uploaded clip, sends those images with the question to [MiniCPM-o 4.5](https://huggingface.co/openbmb/MiniCPM-o-4_5), and displays the model's generated answer.

## Research Question

**How can a user ask a natural-language question about a video and receive an answer from a multimodal language model?**

This project answers that question with an interactive frame-based workflow: the application samples video frames, combines them with the user's question, and passes the resulting prompt to MiniCPM-o 4.5 for text generation. The answer is returned in the web interface. The application demonstrates this workflow; it does not include a benchmark or quantitative model evaluation.

## How It Works

1. The user uploads a video or selects one of the bundled examples and enters a question.
2. Decord reads the video and samples frames at approximately one frame per second. If more than 64 frames would be selected, the sampler reduces the set to a maximum of 64 frames.
3. The sampled images and question are sent to MiniCPM-o 4.5 using its chat interface.
4. The generated text is shown as the predicted answer in Gradio.

The application loads the model's vision branch only. It does not extract a soundtrack, transcribe speech, or pass audio to the model. Answers are based on sampled frames, so brief events between sampled frames may be missed.

## Features

- Video upload and three bundled example clips.
- Natural-language questions about the video imagery.
- Adjustable generation settings:
  - Temperature: 0.01–1.99 (default 0.7)
  - Top-p: 0–1 (default 0.8)
  - Top-k: 0–1000 (default 100)
  - Maximum generated tokens: 1–4096 (default 512)
- Text answer output with a copy control.

## Screenshots and Examples

The screenshots below are the existing application/result images in `assets/`.

![Video Understanding QA example 1](assets/Screenshot%20%28434%29.png)

![Video Understanding QA example 2](assets/Screenshot%20%28435%29.png)

![Video Understanding QA example 3](assets/Screenshot%20%28436%29.png)

The sample videos used by the Gradio examples are `videos/sample_video_1.mp4`, `videos/sample_video_2.mp4`, and `videos/sample_video_3.mp4`.

## Requirements

- Python 3.10 or newer is recommended.
- An NVIDIA GPU with CUDA support is required by the current configuration, which sets the model device to `cuda` and loads weights in bfloat16 precision.
- Internet access is needed on the first run to download the model from Hugging Face. Allow sufficient disk space for the model weights.

## Run Locally

Clone the repository and enter its directory:

```powershell
git clone https://github.com/hassaan4717/Video_Understanding_QA.git
cd Video_Understanding_QA
```

Create and activate a virtual environment, then install the dependencies:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m pip install spaces
```

The application imports `spaces` for its GPU decorator, but that package is not currently listed in `requirements.txt`, so it is installed separately above.

Start the application:

```powershell
python app.py
```

Open the local URL printed in the terminal (typically `http://127.0.0.1:7860`). The first startup loads the model and may take several minutes. On macOS or Linux, activate the environment with `source .venv/bin/activate` instead.

### Hugging Face Authentication

The model is loaded from the Hugging Face Hub. An access token is optional for a public model, but can be supplied through an `ACCESS_TOKEN` entry in a `.env` file in the project root if authenticated access is needed:

```text
ACCESS_TOKEN=your_hugging_face_token
```

Do not commit the token. The repository's `.gitignore` excludes `.env` files.

## Project Structure

```text
Video Understanding QA/
├── app.py                     # Gradio interface and example inputs
├── assets/                    # Existing application screenshots
├── videos/                    # Bundled example videos
├── src/
│   ├── config.py              # Model and generation defaults
│   ├── exception.py           # Exception formatting
│   ├── logger.py              # File logging setup
│   ├── minicpm/
│   │   ├── model.py           # MiniCPM-o model loading
│   │   └── response.py        # Video-question inference
│   └── utils/
│       └── video_processing.py # Video frame sampling
├── requirements.txt
└── LICENSE
```

## Limitations

- This is a frame-based visual QA demo, not a full-video temporal analysis system. Events not captured in the sampled frames may not inform the answer.
- Audio is not processed, even though the selected model family supports audio capabilities.
- Generated answers can be incomplete or incorrect; verify important details against the original video.
- The configured `cuda` device means the current application is not set up for CPU-only inference.

## License

This project is distributed under the [MIT License](LICENSE).


