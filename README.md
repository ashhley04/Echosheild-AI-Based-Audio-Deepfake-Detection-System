# 🛡️ EchoShield — Audio Deepfake Detection

**Detect synthetic speech. Analyze audio. Generate forensic reports.**

EchoShield is an AI-powered audio deepfake detection and forensic analysis platform designed to distinguish **genuine human speech from AI-generated or manipulated audio**. It combines deep learning, audio feature engineering, and an interactive Streamlit application to make audio authenticity analysis more accessible.

Built using Python, TensorFlow, Librosa, scikit-learn, and Streamlit, EchoShield provides audio classification, batch analysis, user authentication, analysis history, and downloadable forensic reports.

## ✨ Key Features

- 🎙️ **Audio Deepfake Detection:** Classifies audio recordings as `bonafide` (genuine) or `spoof` (synthetic or manipulated).
- 🧠 **CNN-Based Classification:** Uses Mel-spectrogram representations to learn discriminative audio patterns.
- 📊 **SVM-Based Classification:** Uses Mel-Frequency Cepstral Coefficients (MFCCs) for machine learning-based audio classification.
- 🔬 **Audio Forensics:** Supports audio preprocessing, feature extraction, and spectrogram visualization.
- 📂 **Batch Audio Analysis:** Processes multiple audio files through a dedicated batch-upload interface.
- 📑 **PDF Forensic Reports:** Generates downloadable reports containing analysis results.
- 📈 **Excel Export:** Exports batch analysis results for further investigation.
- 🔐 **User Authentication:** Includes registration, login, password hashing, session management, and administrator support.
- 🗄️ **Analysis History:** Uses SQLite to store user information, analysis records, reports, and statistics.
- 🖥️ **Interactive Dashboard:** Provides a Streamlit-based interface for accessing the system's analysis features.

---

## 🧠 Models & Performance

EchoShield explores two approaches to audio deepfake detection.

| Model | Input Features | Reported Accuracy |
|---|---|---:|
| Convolutional Neural Network (CNN) | Mel-spectrograms | **96.8%** |
| Support Vector Machine (SVM) | MFCC features | **93.4%** |

*These are the reported evaluation results for the project. Performance may vary across datasets, recording conditions, and unseen spoofing methods.*

### 1. Convolutional Neural Network (CNN)

The CNN learns patterns from Mel-spectrograms to distinguish genuine speech from synthetic audio.

- Converts audio recordings into Mel-spectrogram representations.
- Uses convolutional layers to learn relevant time-frequency patterns.
- Applies dense layers to classify audio into bonafide and spoof categories.
- Saves the trained model in Keras format for application inference.

### 2. Support Vector Machine (SVM)

The SVM provides a traditional machine learning baseline using handcrafted audio features.

- Extracts MFCCs from preprocessed audio.
- Applies feature scaling using `StandardScaler`.
- Trains an SVM classifier on the extracted features.
- Evaluates classification performance against the CNN approach.

Comparing both approaches demonstrates the differences between learned spectrogram representations and handcrafted audio features.

---

## 🔬 Dataset & Audio Processing

**Dataset:** ASVspoof 2019 — Logical Access (LA)

EchoShield uses the ASVspoof 2019 LA dataset for model development and evaluation. The dataset contains genuine speech and spoofed speech generated using different spoofing techniques.

### Audio preprocessing pipeline

1. **Audio loading:** Loads recordings using Librosa.
2. **Resampling:** Standardizes audio to 16 kHz.
3. **Segmentation:** Processes audio in five-second segments.
4. **Feature extraction:** Generates Mel-spectrograms for CNN input and MFCCs for SVM input.
5. **Model inference:** Passes the extracted representations to the selected classifier.
6. **Classification:** Produces a bonafide or spoof prediction.

The training notebook handles feature extraction, model training, and evaluation, while the application components support inference and result management.

> **Note:** EchoShield is a research and screening tool. Its predictions should not be treated as definitive proof of audio authenticity.

---

## 🏗️ System Architecture

```text
               Audio Input
                    |
                    v
           Audio Preprocessing
            (16 kHz, 5-second)
                    |
                    v
            Feature Extraction
              /           \
             v             v
      Mel-Spectrogram     MFCCs
             |             |
             v             v
         CNN Model      SVM Model
             |             |
             v             v
         Classification Results
                    |
                    v
           Analysis Dashboard
                    |
          +---------+---------+
          |         |         |
          v         v         v
        SQLite      PDF     Excel
        History   Reports   Export
```

*Conceptual overview of the detection and reporting workflow.*

---

## 📁 Project Structure

```text
Echosheild-AI-Based-Audio-Deepfake-Detection-System/
│
├── app.py                       # Main Streamlit application
├── batch_test_upload.py         # Batch analysis and Excel export
├── train.ipynb                  # Feature extraction, training and evaluation
├── utils.py                     # Audio features and spectrogram utilities
│
├── models/
│   └── deepfake_modelv3.keras   # Trained CNN model
│
├── auth.py                      # Authentication and session helpers
├── database.py                  # SQLite database operations
├── reports.py                   # PDF forensic report generation
├── settingadmin.py              # Administrator promotion helper
├── requirements.txt             # Python dependencies
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10 or 3.11 recommended
- Git
- pip
- Windows, macOS, or Linux

Python 3.11 is a suitable starting point for compatibility with the project's audio processing and machine learning dependencies.

### 1. Clone the repository

```bash
git clone https://github.com/ashhley04/Echosheild-AI-Based-Audio-Deepfake-Detection-System.git
```

Navigate to the project directory:

```bash
cd Echosheild-AI-Based-Audio-Deepfake-Detection-System
```

### 2. Create a virtual environment

**Windows — PowerShell**

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

If PowerShell blocks environment activation, use Command Prompt instead:

```cmd
venv\Scripts\activate.bat
```

**macOS / Linux**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

Upgrade pip and install the required packages:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Launch the application

Start the main Streamlit application:

```bash
streamlit run app.py
```

Streamlit will display a local URL in the terminal. Open that URL in your browser to access EchoShield.

### 5. Run batch analysis

To launch the batch-upload interface separately:

```bash
streamlit run batch_test_upload.py
```

**Note:** Ensure the trained model and required application files are present. Depending on your configuration, SQLite databases and generated reports may be created when the application runs.

---

## 🔁 Retraining the Model

To retrain the CNN, download the ASVspoof 2019 LA dataset and prepare the required audio files and protocol file.

### Expected dataset layout

```text
dataset/
└── ASVspoof2019_LA_train/
    ├── flac/
    │   ├── LA_T_....flac
    │   └── ...
    └── train_protocol.txt
```

### Protocol format

The training protocol is space-separated and contains the following fields:

```text
speaker file_id unused attack_id label
```

The label identifies the recording as `bonafide` or `spoof`.

### Training steps

1. Place the training audio files and protocol file in the expected directories.
2. Update `DATA_PATH` and `PROTOCOL_PATH` in `train.ipynb`.
3. Run the notebook cells for data loading, preprocessing, feature extraction, training, and evaluation.
4. Review the evaluation metrics.
5. Save the trained CNN model in the `models/` directory.

Ensure that the saved model filename and input shape match the configuration expected by `app.py`.

**Dataset:** [ASVspoof Official Website](https://www.asvspoof.org/)

Obtain the dataset through the official website and comply with its applicable access and usage terms.

---

## 🛠️ Tech Stack

| Category | Technologies |
|---|---|
| Programming Language | Python |
| Deep Learning | TensorFlow, Keras |
| Machine Learning | scikit-learn, SVM |
| Audio Processing | Librosa |
| Data Processing | NumPy, Pandas |
| Visualization | Matplotlib, Seaborn |
| Web Application | Streamlit |
| Database | SQLite |
| PDF Reports | FPDF |
| Excel Export | openpyxl |
| Development | Jupyter Notebook, Git, GitHub |

---

## 📊 Evaluation Metrics

EchoShield evaluates model performance using standard classification metrics:

- **Accuracy:** Overall proportion of correct predictions.
- **Precision:** Proportion of predicted positive samples that are actually positive.
- **Recall:** Proportion of actual positive samples correctly identified.
- **F1-score:** Harmonic mean of precision and recall.

These metrics provide a more informative comparison than accuracy alone, particularly when evaluating audio spoof detection.

For reproducible research, report the dataset split, class distribution, test-set size, and per-class performance alongside the headline accuracy.

---

## 🔮 Future Improvements

- Integrate additional state-of-the-art audio deepfake detection architectures.
- Evaluate robustness against unseen spoofing techniques and real-world recording conditions.
- Add explainability tools to highlight influential time-frequency regions.
- Extend analysis with speaker verification and anti-spoofing workflows.
- Improve calibration and confidence reporting for model predictions.
- Introduce a deployment-ready API and containerized application.
- Expand support for large-scale audio analysis and forensic case management.

---

## 📄 License

A `LICENSE` file has not been specified in this project structure. Add an appropriate license before distributing the code for reuse.

If you choose the MIT License, include a `LICENSE` file containing its complete terms. Also review the dataset's separate licensing and usage conditions.

---

⭐ **If you find EchoShield useful for research or learning, consider starring the repository!**

*Built to explore the intersection of artificial intelligence, audio forensics, and trustworthy speech technologies.*
