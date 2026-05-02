# VidiQA

Video Question Answering is the task of answering open-ended questions based on a video clip. They output natural language responses to natural language questions about the content of a video clip. This project uses one of the popular multimodal models, [**MiniCPM-o 4.5**](https://huggingface.co/openbmb/MiniCPM-o-4_5) from the Hugging Face model hub.

[**MiniCPM-o 4.5**](https://huggingface.co/openbmb/MiniCPM-o-4_5) is the latest and most capable model in the MiniCPM-o series. The model is built in an end-to-end fashion based on **SigLip2**, **Whisper-medium**, **CosyVoice2**, and **Qwen3-8B** with a total of 9B parameters. It exhibits a significant performance improvement, and introduces new features for full-duplex multimodal live streaming.

## Project Structure

The project is structured as follows:

- `src\`: The folder that contains the source code for the project.

  - `minicpm\`: The folder containing the source code for the application's main functionality.

    - `model.py`: The file that contains the code for loading the model and the tokenizer.
    - `response.py`: The file that contains the function for generating the response for the input video and question.

  - `utils\`: The folder containing the project's utility function.
    - `video_processing.py`: This file contains the functions for processing the video input.

  - `config.py`: This file contains the configuration for the used model.
  - `logger.py`: This file contains the project's logging configuration.
  - `exception.py`: This file contains the exception handling for the project.

- `app.py`: The main file that contains the Gradio application for video question answering.
- `requirements.txt`: The file containing the project's required dependencies.
- `LICENSE`: The license file for the project.
- `README.md`: The README file that contains information about the project.
- `assets`: The folder that contains the screenshots for working on the application.
- `videos`: The folder that contains the videos for testing the application.

## Tech Stack

- Python (for the programming language)
- PyTorch (for the deep learning framework)
- Hugging Face Transformers Library (for the visual question-answering model)
- Gradio (for the web application)
- Hugging Face Spaces (for hosting the gradio application)

## Usage

The web application allows you to upload a video and input a question. The model will analyze the video frames and generate an answer based on the content of the video and the question. This can assist in video summarization, enhance video retrieval by identifying specific scenes or actions, and support visually impaired individuals by describing video content. The application is also useful in educational settings for providing detailed explanations or context based on video material.

## Results

For results, refer to the `assets/` directory for the output screenshots, which show the application in action.

## Contributing

Contributions are welcome! If you would like to contribute to this project, please raise an issue to discuss the changes you want to make. Once the changes are approved, you can create a pull request.

## License

This project is licensed under the [MIT License](LICENSE).

## Contact

If you have any questions or suggestions regarding the project, feel free to reach out to me on my GitHub profile.


