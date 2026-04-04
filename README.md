# Analyzing Spotify Audio Features and Discovering Natural Song Clusters

**CS 4412: Data Mining — Kennesaw State University**  
**Author:** Sarbani Adhikari (sadhika7@students.kennesaw.edu)

---

## Project Overview

This project applies data mining techniques to the [Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset) to discover natural clusters of songs based on audio features. This means looking at if audio-based clustering aligns or diverges from Spotify's existing genre labels and uncover patterns that may cross traditional genre boundaries.

## Discovery Questions

1. **Primary:** What natural clusters of songs emerge from audio features, and how do these clusters align or conflict with Spotify's genre labels?
2. **Supporting:** What latent dimensions underlie the audio feature space? (answered via PCA)
3. **Supporting:** What decision rules characterize each cluster's audio profile? (answered via decision trees)

## Dataset

- **Source:** [Spotify Tracks Dataset on Kaggle](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset)
- **Size:** ~114,000 rows × 20 columns (~15 MB)
- **After dedup:** 89,740 tracks × 20 columns
- **Unique Genres:** 113

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
│   ├── proposal.pdf           # Proposal document
│   ├── proposal.tex
│   ├── initial_implementation.pdf  # Initial implementation summary
│   ├── initial_implementation.tex
│   ├── complete_implementation.pdf # Complete implementation summary
│   └── complete_implementation.tex
├── notebooks/
│   ├── analysis_v1.ipynb      # Initial implementation (EDA, preprocessing, K-Means)
│   └── analysis_v2.ipynb      # Complete implementation (DBSCAN, decision trees, LOF)
└── outputs/
    └── figures/               # Generated visualizations (fig1-fig18)
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

5. **Run the notebooks:**
   ```bash
   jupyter notebook notebooks/analysis_v1.ipynb  # initial implementation
   jupyter notebook notebooks/analysis_v2.ipynb  # complete implementation
   ```

## Milestone Progress

### Proposal
- Identified dataset and discovery questions
- Defined planned techniques (PCA, K-Means, DBSCAN, Decision Trees)
- Set up GitHub repository

### Initial Implementation
- **EDA:** 14 visualizations exploring distributions, correlations, genre profiles, duration, and feature relationships
- **Preprocessing:** Dropped 1-3 rows with missing metadata, removed 24,259 duplicate track_ids, outlier assessment (retained as legitimate variation), z-score standardization
- **PCA:** Identified two key latent dimensions -- "Acoustic vs Produced" (PC1) and "Upbeat vs Moody" (PC2)
- **Clustering:** K-Means with k=5, selected via elbow method and silhouette analysis
- **Findings:** Five distinct sonic archetypes discovered; genre labels do not map neatly onto audio-based clusters, confirming cross-genre patterns

### Complete Implementation
- **DBSCAN:** Compared density-based clustering with K-Means on a 20k sample. DBSCAN finds one dominant cluster with small speech-heavy offshoots, confirming that K-Means partitions a continuous space rather than finding truly separated groups. Noise points dominated by sleep, comedy, and iranian music.
- **Decision Trees:** Depth-4 tree on K-Means cluster labels achieves ~85% training accuracy. Energy and valence are the top splitting features. Each cluster can be described by 2-3 feature thresholds in plain English.
- **Anomaly Detection (LOF):** Local Outlier Factor flagged ~2% of tracks as anomalies. These tend to be quieter, more acoustic/instrumental, and higher speechiness. About half overlap with DBSCAN noise points. Anomalies scatter on the edges of PCA space rather than forming a hidden cluster.
- **Discovery Questions:** All three questions now have substantive answers.

### Final Report (In work)
- Complete analysis synthesis
- Limitations discussion
- Final report and presentation

## Tools & Libraries

| Library | Purpose |
|---------|---------|
| pandas | Data manipulation |
| numpy | Numerical operations |
| matplotlib | Visualization |
| seaborn | Statistical visualization |
| scikit-learn | Clustering, PCA, classification, anomaly detection, preprocessing |
| jupyter | Interactive notebook environment |

