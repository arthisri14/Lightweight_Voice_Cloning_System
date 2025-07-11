# IndiaSpeaks Voice Cloning System – Rapid Prototype

This repository contains a functional **multi-speaker voice cloning prototype** built for the **IndiaSpeaks** initiative. The system takes a short reference mel-spectrogram and generates a cloned mel-spectrogram in the target speaker's voice.

---

## Objective

Develop a **lightweight, personalized IVR** system that can:
- Accept **short reference utterances**
- Clone voices from **5 speakers**
- Output mel-spectrograms (no vocoder required)

---

## Architecture Overview

### 🔹 1. **Speaker Encoder**
- Takes (80, 50) mel spectrogram as input
- Uses 2 convolutional layers + adaptive pooling
- Outputs 128-dimensional fixed speaker embedding

### 🔹 2. **Tacotron-style Mel Decoder**
- Uses shallow **attention-based GRU decoder**
- Produces mel-spectrogram output conditioned on the speaker embedding
- Attention improves temporal alignment and speech quality

### 🔹 3. **Loss Function**
- `MSE Loss` for frame-level accuracy
- `Cosine Similarity` loss to preserve spectral direction and phonetic identity
- Total Loss = `MSE + 0.1 × Cosine`

---

## Dataset

Provided CSV files:
- `mel_train.csv` (300 samples)
- `mel_val.csv` (60 samples)
- `mel_reference.csv` (5 samples; 1 per speaker)

Each sample:
- 4,000 values = (80 mel bins × 50 time steps)
- Normalized to zero-mean, unit variance per channel

---
##  Training Results  

- Final Training Loss ≈ *~1.003* depending on epochs  
- Training curve shows **steady decline**  
- Model successfully overfits on small dataset (as expected for prototype)  


---

##  Output Format  

### `cloned_mel_predictions(1).csv`

| speaker_id | predicted_mel_flat     |
|------------|------------------------|
| 0          | 4000 floats (80×50)    |
| 1          | ...                    |

---

##  How to Run  

###  Google Colab or Local (Python ≥ 3.8, PyTorch ≥ 1.12)


