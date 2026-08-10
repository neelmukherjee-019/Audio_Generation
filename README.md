# 🎙️ Text-to-Speech using Hugging Face

A simple **Text-to-Speech (TTS)** project that converts user-provided text into natural-sounding speech using a **pretrained Hugging Face model**.

The project uses Meta's **Massively Multilingual Speech (MMS)** TTS model, `facebook/mms-tts-eng`, to generate `.wav` audio files directly from text.

---

## 📌 Project Overview

This project demonstrates how a pretrained Transformer-based TTS model can be used to convert text into speech without training a model from scratch.

The application:

1. Takes text input from the user.
2. Tokenizes the text using the pretrained tokenizer.
3. Passes the tokens to the pretrained TTS model.
4. Generates an audio waveform.
5. Saves the generated speech as a `.wav` file.
6. Plays the generated audio directly in Jupyter Notebook or Google Colab.

---

## 🤖 Model Used

**Model:** `facebook/mms-tts-eng`

**Task:** Text-to-Speech

**Framework:** Hugging Face Transformers

**Model Architecture:** VITS

**Language:** English

The model is part of Meta's Massively Multilingual Speech (MMS) project.

---

## 🛠️ Technologies Used

* Python
* PyTorch
* Hugging Face Transformers
* Meta MMS TTS
* SciPy
* IPython
* Jupyter Notebook / Google Colab

---

## 📂 Project Structure

```text
Text-to-Speech/
│
├── text_to_speech.py
├── speech_1.wav
├── speech_2.wav
├── requirements.txt
└── README.md
```

> The generated `.wav` files are created when the program is executed.

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/your-username/text-to-speech-huggingface.git
```

### 2. Navigate to the project directory

```bash
cd text-to-speech-huggingface
```

### 3. Install the required dependencies

```bash
pip install -r requirements.txt
```

Alternatively:

```bash
pip install transformers torch scipy soundfile
```

---

## 📦 Requirements

Create a `requirements.txt` file containing:

```text
transformers
torch
scipy
soundfile
```

---

## 🚀 Usage

Run the Python program:

```bash
python text_to_speech.py
```

The program will ask you to enter the text:

```text
Enter text (type 'exit' to stop):
```

Enter any English sentence.

For example:

```text
Artificial intelligence is transforming the way we interact with technology.
```

The model will convert the text into speech and save the result as:

```text
speech_1.wav
```

The generated audio will also be played directly in a Jupyter Notebook or Google Colab environment.

---

## 💻 Core Implementation

```python
import torch
import scipy.io.wavfile as wavfile
from IPython.display import Audio, display
from transformers import AutoTokenizer, VitsModel

# Load pretrained model
model_name = "facebook/mms-tts-eng"

tokenizer = AutoTokenizer.from_pretrained(model_name)
model = VitsModel.from_pretrained(model_name)

count = 1

while True:

    text = input("\nEnter text (type 'exit' to stop): ")

    if text.lower() == "exit":
        print("Program terminated.")
        break

    # Tokenize input
    inputs = tokenizer(text, return_tensors="pt")

    # Generate speech
    with torch.no_grad():
        waveform = model(**inputs).waveform

    # Convert waveform to NumPy
    audio = waveform.squeeze().cpu().numpy()

    # Save audio
    filename = f"speech_{count}.wav"

    wavfile.write(
        filename,
        rate=model.config.sampling_rate,
        data=audio
    )

    print(f"Saved: {filename}")

    # Play audio
    display(
        Audio(
            audio,
            rate=model.config.sampling_rate
        )
    )

    count += 1
```

---

## 🔄 How It Works

```text
             User Input
                 │
                 ▼
        ┌─────────────────┐
        │   Text Input    │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │    Tokenizer    │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │  VITS TTS Model │
        │ facebook/mms... │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │ Audio Waveform  │
        └────────┬────────┘
                 │
          ┌──────┴───────┐
          ▼              ▼
    Save as .wav      Play Audio
```

---

## 🧠 Key Concepts Demonstrated

### 1. Pretrained Models

The project uses an already-trained TTS model instead of training a neural network from scratch.

```python
VitsModel.from_pretrained("facebook/mms-tts-eng")
```

### 2. Tokenization

The input text is converted into tokens that the model can process.

```python
inputs = tokenizer(text, return_tensors="pt")
```

### 3. Inference

The pretrained model generates an audio waveform from the tokenized text.

```python
with torch.no_grad():
    waveform = model(**inputs).waveform
```

### 4. Audio Generation

The waveform is converted into a NumPy array and saved as a WAV file.

```python
wavfile.write(
    filename,
    rate=model.config.sampling_rate,
    data=audio
)
```

---

## ✨ Features

* ✅ Uses a pretrained Hugging Face model
* ✅ No model training required
* ✅ Simple text input
* ✅ Generates speech in real time
* ✅ Saves generated speech as `.wav`
* ✅ Supports multiple inputs in one session
* ✅ Works with Jupyter Notebook and Google Colab
* ✅ Lightweight implementation
* ✅ Easy to extend into a larger application

---

## 📊 Example

### Input

```text
Welcome to my Text-to-Speech project using Hugging Face.
```

### Output

```text
speech_1.wav
```

The generated `.wav` file contains the spoken version of the input sentence.

---

## ⚠️ Limitations

* The current implementation supports English using `facebook/mms-tts-eng`.
* Voice characteristics are determined by the pretrained model.
* The quality and speed depend on the available hardware.
* Very long text inputs may produce longer processing times.
* The current implementation does not provide voice cloning or custom speaker selection.

---

## 🔮 Future Improvements

Potential improvements include:

* 🌍 Support for multiple languages
* 🎭 Multiple speaker/voice options
* 🖥️ Build a Streamlit web interface
* 🎧 Add audio playback controls
* 📥 Allow users to download generated audio
* 📚 Support longer paragraphs
* ⚡ GPU acceleration
* 🎤 Add speech-to-text functionality
* 🔄 Build a complete Speech-to-Speech application
* 🤖 Integrate an LLM to generate the text automatically

---

## 📚 Learning Outcomes

Through this project, the following concepts are demonstrated:

* Hugging Face Transformers
* Pretrained AI models
* Natural Language Processing
* Text-to-Speech synthesis
* VITS architecture
* PyTorch inference
* Tokenization
* Audio waveform generation
* WAV file generation
* Model inference without fine-tuning

---

## 📜 License

This project is intended for educational and experimentation purposes.

The pretrained model is provided by Meta through Hugging Face. Please refer to the model's license and usage conditions before using it in production or commercial applications.

---

## 👨‍💻 Author

**Neel Mukherjee**

B.Tech – Computer Science & Engineering
Specialization in Artificial Intelligence & Machine Learning

---

## ⭐ Acknowledgements

* [Hugging Face](https://huggingface.co/)
* Meta AI
* MMS – Massively Multilingual Speech
* PyTorch
* Hugging Face Transformers
