## 📁 Project Structure

```
├── models/
│   └── deepfake_modelv3.keras     # Trained CNN
├── train.ipynb                    # Feature extraction, training, evaluation
├── utils.py                       # MFCC / Mel extraction and spectrogram plotting
├── auth.py                        # Sign-up, login, password hashing, session helpers
├── database.py                    # SQLite: users, analyses, PDF reports, stats
├── reports.py                     # PDF forensic report generation
├── batch_test_upload.py           # Batch upload app with Excel export
├── settingadmin.py                # Helper script to promote a user to admin
└── requirements.txt
```

---

## 🚀 Setup

```bash
# 1. Clone
git clone https://github.com/ashhley04/Echosheild-AI-Based-Audio-Deepfake-Detection-System.git
cd Echosheild-AI-Based-Audio-Deepfake-Detection-System

# 2. Create a virtual environment
python -m venv venv
venv\Scripts\activate          # Windows
# source venv/bin/activate     # macOS / Linux

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run the app
streamlit run app.py
```

To run only the batch analyser: `streamlit run batch_test_upload.py`

### Retraining the model

1. Download ASVspoof 2019 LA and place the training audio and your protocol file at:
```
   dataset/ASVspoof2019_LA_train/flac/
   dataset/ASVspoof2019_LA_train/train_protocol.txt
```
   The protocol is space-separated with columns: speaker, file ID, unused, attack ID, label (`bonafide` or `spoof`).
2. Update `DATA_PATH` and `PROTOCOL_PATH` in `train.ipynb`.
3. Run all cells. The trained model is saved to `models/`.

---

## 🛠️ Tech Stack

**Language:** Python  
**Deep learning:** TensorFlow / Keras, scikit-learn  
**Audio:** Librosa (MFCC, Mel-spectrogram)  
**App:** Streamlit, SQLite  
**Reporting:** FPDF, openpyxl (Excel export)  
**Analysis and plots:** NumPy, Pandas, Matplotlib, Seaborn

---

## 👩‍💻 Author

**Ashley James**: B.E. Information Technology, Fr. C. Rodrigues Institute of Technology, Navi Mumbai
[GitHub](https://github.com/ashhley04) · [LinkedIn](https://www.linkedin.com/in/ashley-james-4bb4092b5)

<!-- Add co-authors here if applicable:
**Co-authors:** Name 1, Name 2
-->

## 📚 Citation

```bibtex
@inproceedings{echoshield2026,
  title     = {EchoShield: Audio Deepfake Detection},
  author    = {James, Ashley and others},
  booktitle = {Springer Proceedings},
  year      = {2026},
  note      = {In press}
}
```

---

## 📄 Licence

Add a `LICENSE` file (MIT is a common choice for student projects). The ASVspoof 2019 dataset has its own licence terms; see the link above.
