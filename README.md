# Audio Fingerprinting-Based Song Identification System

An audio fingerprinting app, built on the **spectrogram / constellation map / hash matching** pipeline.

---

## What it does

### Single Clip Mode

- Upload one query clip and see:
  - The spectrogram
  - The constellation map (detected peaks)
  - The offset histogram
  - The predicted song

### Batch Mode

- Upload several query clips at once.
- Download `results.csv` with exactly two columns:
  - `filename`
  - `prediction`

---

## Repository Layout

```text
fingerprint.py       Core fingerprinting pipeline (spectrogram, peaks, hashes, matching)
build_database.py    One-time script: fingerprints every song in a folder and saves database.pkl
database.pkl         Pre-built fingerprint database (committed so the app starts instantly)
app.py               The Streamlit app
requirements.txt     Python dependencies
packages.txt         System dependency (ffmpeg, needed by librosa to decode mp3)
```

---

## Running Locally

Install dependencies:

```bash
pip install -r requirements.txt
```

If you don't already have `database.pkl`, build it once from your song folder:

```bash
python build_database.py "/path/to/your/song/database/folder"
```

This writes `database.pkl` in the current directory.

Run the app:

```bash
streamlit run app.py
```

---

## Notes

- If you add or change songs in the database, re-run `build_database.py` and commit the updated `database.pkl`.
- `fingerprint.py` is shared between `build_database.py` and `app.py`, so the matching logic used during database creation and query matching always stays in sync.
