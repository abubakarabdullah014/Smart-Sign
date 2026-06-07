
# Smart Sign

Smart Sign is a desktop application that translates sign language videos into text. Upload a recording or use your webcam, and the app extracts body pose, runs a neural translation model, and shows the predicted sentence on screen.

Built with Python, [Flet](https://flet.dev/) for the UI, PyTorch for the model, and pose estimation via [rtmlib](https://github.com/Tau-J/rtmlib).

## Features

- **User accounts** — register, sign in, and sign out
- **Video upload** — pick a local video file and run translation
- **Live camera** — record from a webcam and translate in real time
- **Feedback** — rate results and leave comments (stored locally)
- **Modern UI** — dark theme with sidebar navigation

## Project structure

```
smart_sign/
├── app.py                 # Flet desktop application entry point
├── sign_model.py          # Smart Sign neural network (pose + MT5 decoder)
├── sign_data.py           # Dataset loaders for training and online inference
├── sign_utils.py          # Training helpers, metrics, and CLI argument parsing
├── settings.py            # Dataset paths and model configuration
├── sign_network/          # Graph convolution and attention building blocks
├── pipeline/
│   ├── inference.py       # Video → pose → text inference pipeline
│   └── vision.py          # Batch pose extraction utility
├── training_scripts/      # Shell scripts for multi-stage model training
├── checkpoints/           # Model weights (not committed — see setup below)
├── logo.png               # App branding asset
└── requirements.txt       # Python dependencies
```

## Requirements

- Windows 10/11 (primary target; Linux may work with extra setup)
- Python 3.11+
- NVIDIA GPU with CUDA (recommended for inference speed)
- FFmpeg (optional, for some video formats)

## Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/YOUR_USERNAME/smart_sign.git
   cd smart_sign
   ```

2. **Create a virtual environment**

   ```bash
   python -m venv smart_sign_env
   smart_sign_env\Scripts\activate        # Windows
   # source smart_sign_env/bin/activate   # Linux/macOS
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Add model checkpoint**

   Place your trained checkpoint at:

   ```
   checkpoints/openasl_pose_only_slt.pth
   ```

   Checkpoints are excluded from Git because of file size. Download or train your own weights before running inference.

5. **Run the app**

   ```bash
   python app.py
   ```

   To force browser mode instead of the desktop window:

   ```bash
   set FLET_VIEW=web
   python app.py
   ```

## Inference (CLI)

You can run translation on a single video from the command line:

```bash
python -m pipeline.inference ^
  --online_video path\to\video.mp4 ^
  --finetune checkpoints\openasl_pose_only_slt.pth ^
  --dataset OpenASL ^
  --task SLT ^
  --eval ^
  --dtype bf16
```

## Building a standalone executable

PyInstaller spec file is included:

```bash
pyinstaller smart_sign.spec
```

The output executable is written to the `dist/` folder.

## Training

Multi-stage training scripts live in `training_scripts/`. They expect sign-language datasets (CSL, WLASL, OpenASL, etc.) configured in `settings.py`. Training data and large video folders are not part of this repository.

## Configuration

Edit `settings.py` to point at your local dataset directories and label files. Runtime files such as `users.json`, `feedback.json`, and `uploads/` are created automatically and are ignored by Git.



https://github.com/user-attachments/assets/cd827c47-c848-40e3-ab23-de7f59efdfd7





## Author

Built as **Smart Sign** — an original sign language translation application.
=======
# Smart-Sign
Smart Sign is an AI-based American Sign Language (ASL) to text translation system that recognizes hand gestures using computer vision and deep learning models. It provides real-time conversion of sign language into readable text, helping bridge communication between deaf or hard-of-hearing individuals and others. (FYP project)

