# Spotify Audio Feature Clustering  
Unsupervised Learning with PCA and K-Means

This project uses unsupervised machine learning techniques to identify natural
groupings ("vibes") in a Spotify audio feature dataset. By combining exploratory
data analysis (EDA), feature scaling, PCA for dimensionality reduction, and
K-Means clustering, the project uncovers meaningful musical structure without
using genre labels as a target.

---

## Project Overview

**Goal**

Use unsupervised learning to discover clusters of songs based purely on Spotify’s
numeric audio features (e.g., danceability, energy, loudness, acousticness,
instrumentalness, valence, tempo, duration).

**Techniques Used**

- Exploratory Data Analysis (EDA)
- Feature scaling (StandardScaler)
- Principal Component Analysis (PCA)
- K-Means clustering (k = 4)
- Cluster interpretation using cluster centers

**Dataset**

The project uses the `genres_v2.csv` file from the Kaggle dataset:

> Dataset of Songs in Spotify by mrmorj  
> (Downloaded and stored locally in the `data/` directory.)

Each row corresponds to a single track and includes metadata (track name,
artist, genre, popularity) and numerical audio attributes obtained from
Spotify’s audio analysis API.

---

## Repository Structure

Project layout:

    spotify-unsupervised-clustering/
    ├── data/
    │   └── genres_v2.csv              # Spotify audio feature dataset (from Kaggle)
    │
    ├── notebook/
    │   └── spotify-clustering.ipynb   # Main analysis notebook
    │
    └── README.md                      # Project description and instructions

The main work for the assignment is contained in `notebook/spotify-clustering.ipynb`.

---

## Methods and Analysis

1. **EDA and Data Cleaning**
   - Inspected dataset shape, column types, and missing values.
   - Identified and excluded non-numeric or ID-like columns (e.g., URIs, URLs, IDs).
   - Focused on continuous audio features suitable for clustering:
     `danceability`, `energy`, `loudness`, `speechiness`, `acousticness`,
     `instrumentalness`, `liveness`, `valence`, `tempo`, `duration_ms`.
   - Noted that `key`, `mode`, and `time_signature` are categorical-encoded
     integers and excluded them from the clustering feature set.

2. **Feature Scaling**
   - Applied `StandardScaler` to the selected audio features so that all
     variables have zero mean and unit variance, which is important for
     distance-based methods like PCA and K-Means.

3. **PCA (Principal Component Analysis)**
   - Fitted PCA on the scaled features to understand the main axes of variation.
   - The first two principal components capture roughly 45% of the total
     variance, and the first three components capture close to 60%.
   - Used the first two components to visualize the dataset in 2D, revealing a
     continuous but structured distribution of songs.

4. **Choosing the Number of Clusters**
   - Used the Elbow Method (inertia vs. k) and Silhouette scores to select an
     appropriate number of clusters.
   - The Elbow plot indicates diminishing returns at **k = 4**.
   - While k = 2 yields the highest Silhouette score, it is too coarse to be
     musically interesting. k = 4 provides a good balance between separation and
     interpretability.
   - **Final choice: k = 4 clusters.**

5. **K-Means Clustering**
   - Applied K-Means with k = 4 to the scaled audio features.
   - Visualized resulting clusters in the 2D PCA space.
   - Examined cluster centers to interpret each group’s audio profile.

---

## Cluster Summaries

Based on the standardized cluster centers, the four clusters can be interpreted as:

1. **Cluster 0 — Acoustic / Mellow**
   - Very low energy and loudness
   - Very high acousticness
   - Below-average danceability and instrumentalness  
   → Quiet, mellow, and acoustic tracks (soft indie, folk, lo-fi acoustic).

2. **Cluster 1 — Intense / Loud Rock-Pop**
   - High energy and loudness
   - Low danceability and acousticness
   - Slightly higher liveness  
   → Energetic, loud tracks that are not strongly dance-focused (rock,
     alternative, high-energy pop, intense ballads).

3. **Cluster 2 — Upbeat / Rhythmic / Danceable**
   - High danceability
   - Higher valence (more positive mood)
   - Higher speechiness
   - Near-average loudness and acousticness  
   → Upbeat, rhythmic, and catchy tracks (dance-pop, R&B, rap, groove-heavy music).

4. **Cluster 3 — Instrumental / Ambient / Electronic**
   - Very high instrumentalness
   - Longer duration
   - Lower tempo and speechiness  
   → Instrumental, ambient, or cinematic tracks (soundtracks, ambient electronic,
     long-form electronic pieces).

---

## Visualizations

The notebook includes:

- Histograms of audio feature distributions
- Correlation heatmap of audio features
- PCA scree plot (explained variance by component)
- 2D PCA projection of all songs
- PCA scatterplot colored by K-Means cluster
- Cluster center comparisons

These visualizations support the interpretation of how features interact and how
clusters differ in audio characteristics.

---

## Technologies

- Python
- NumPy, Pandas
- Scikit-learn
- Matplotlib, Seaborn
- Jupyter Notebook

---

## Notes

This repository was created as part of a machine learning course project focused
on unsupervised learning. The accompanying notebook can be used as a
portfolio piece to demonstrate EDA, dimensionality reduction, clustering, and
model interpretation skills.
