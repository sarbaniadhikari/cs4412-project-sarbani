# Analyzing Spotify Audio Features and Discovering Natural Song Clusters

**CS 4412: Data Mining — Kennesaw State University**  
**Author:** Sarbani Adhikari (sadhika7@students.kennesaw.edu)

---

## Project Overview

This project applies data mining techniques to the [Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset) to discover natural clusters of songs based on audio features. This means looking at if audio-based clustering aligns or diverges from Spotify's existing genre labels and uncover patterns that may cross traditional genre boundaries.

## Discovery Questions

1. **Primary:** What natural clusters of songs emerge from audio features, and how do these clusters align or conflict with Spotify's genre labels?
2. **Supporting:** What latent dimensions underlie the audio feature space? (with PCA)
3. **Supporting:** What decision rules characterize each cluster's audio profile? (in work)

## Dataset

- **Source:** [Spotify Tracks Dataset on Kaggle](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset)
- **Size:** ~114,000 rows × 20 columns (~15 MB)
- **Unique Artists:** ~31,000
- **Unique Genres:** 114

### Key Audio Features

| Feature | Range | Description |
|---------|-------|-------------|
| danceability | 0.0–1.0 | Suitability for dancing |
| energy | 0.0–1.0 | Intensity and activity |
| valence | 0.0–1.0 | Musical positiveness |
| acousticness | 0.0–1.0 | Acoustic sound confidence |
| instrumentalness | 0.0–1.0 | Absence of vocals |
| speechiness | 0.0–1.0 | Spoken word presence |
| liveness | 0.0–1.0 | Audience presence |
| loudness | dB | Overall loudness |
| tempo | BPM | Beats per minute |

## Repository Structure

```
cs4412-project-sarbani/
├── README.md                  # This file
├── requirements.txt           # Python dependencies
├── .gitignore                 # Git ignore rules
├── data/
│   └── .gitkeep               # Dataset not tracked (see instructions below)
├── docs/
│   ├── proposal.pdf           # M1 proposal document
│   └── M2_Summary.pdf         # M2 summary document
├── notebooks/
│   └── M2_Analysis.ipynb      # M2 analysis notebook (EDA, preprocessing, clustering)
└── outputs/
    └── figures/               # Generated visualizations
```

## Setup & Installation

### Prerequisites

- Python 3.10+
- pip

### Steps

1. **Clone the repository:**
   ```bash
   git clone https://github.com/sarbaniadhikari/cs4412-project-sarbani.git
   cd cs4412-project-sarbani
   ```

2. **Create a virtual environment (recommended):**
   ```bash
   python -m venv venv
   source venv/bin/activate        # macOS/Linux
   # or: venv\Scripts\activate     # Windows
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Download the dataset:**
   - Go to [Spotify Tracks Dataset on Kaggle](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset)
   - Download `dataset.csv`
   - Place it in the `data/` folder

5. **Run the notebook:**
   ```bash
   jupyter notebook notebooks/M2_Analysis.ipynb
   ```

## Milestone Progress

### Proposal
- Identified dataset and discovery questions
- Defined planned techniques (PCA, K-Means, DBSCAN, Decision Trees)
- Set up GitHub repository

### Initial Implementation
- **EDA:** 14 visualizations exploring distributions, correlations, genre profiles, duration, and feature relationships
- **Preprocessing:** Dropped 1–3 rows with missing metadata, removed 24,259 duplicate track_ids, outlier assessment (retained as legitimate variation), z-score standardization
- **PCA:** Identified two key latent dimensions — "Acoustic ↔ Produced" (PC1) and "Upbeat ↔ Moody" (PC2)
- **Clustering:** K-Means with k=5, selected via elbow method and silhouette analysis
- **Findings:** Five distinct sonic archetypes discovered; genre labels do not map neatly onto audio-based clusters, confirming cross-genre patterns

### Advanced Analysis (In work)
- DBSCAN clustering for comparison with K-Means
- Decision tree classification to generate interpretable cluster rules
- Anomaly detection for genre-defying tracks
- Broader genre groupings for more meaningful cluster-genre comparison

### Final Report (In work)
- Complete analysis synthesis
- Final report and presentation

## Tools & Libraries

| Library | Purpose |
|---------|---------|
| pandas | Data manipulation |
| numpy | Numerical operations |
| matplotlib | Visualization |
| seaborn | Statistical visualization |
| scikit-learn | Clustering, PCA, preprocessing, evaluation metrics |
| mlxtend | Association rules (part 3) |
| jupyter | Interactive notebook environment |

## References

1. M. Pandya, "Spotify Tracks Dataset," Kaggle, 2022. [Link](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset)
2. Zaki & Meira, *Data Mining and Machine Learning*. [Free PDF](https://dataminingbook.info)

## License

This project is for academic purposes as part of CS 4412 at Kennesaw State University.
