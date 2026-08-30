# MusicBrainz Artist Collaboration Graphs

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
![Python 3](https://img.shields.io/badge/Python-3-3776AB?style=flat-square&logo=python&logoColor=white)
![Requests](https://img.shields.io/badge/Requests-HTTP%20client-informational?style=flat-square)
![MusicBrainz API](https://img.shields.io/badge/MusicBrainz-API-BA478F?style=flat-square&logo=musicbrainz&logoColor=white)
![NetworkX](https://img.shields.io/badge/NetworkX-graphs-2C7FB8?style=flat-square)
![Matplotlib](https://img.shields.io/badge/Matplotlib-visualization-11557C?style=flat-square)

**Who records with whom? 🎵 Collaboration networks of seven mainstream artists, fetched live from the MusicBrainz API and drawn as graphs with NetworkX and matplotlib.**

Coursework project — BSc in Applied Data Science, Universitat Oberta de Catalunya (UOC), Data Visualization course.

> Notebook narrative is in Spanish.

## Objective

Collect discography data for seven mainstream artists (Drake, Beyoncé, Rihanna, Jay-Z, Eminem, Nicki Minaj, David Guetta) through the MusicBrainz web-service API, and explore their collaboration networks as graphs. The notebook poses four analysis questions:

1. **Collaboration network** — which artists collaborate frequently with others?
2. **Album collaborations** — how are artists interconnected through releases with multiple credited artists?
3. **Genre crossover** — which artists bridge different musical genres through their collaborations?
4. **Temporal analysis** — how have collaborations evolved over time?

## Data & methods

- **Data collection** with `requests` against the [MusicBrainz API](https://musicbrainz.org/doc/MusicBrainz_API): artist search by name, then release-group lookups including artist credits and genres (`inc=artist-credits+genres`, up to 100 results per call). The raw responses are stored as a local JSON file (`artist_data.json`).
- **Graph construction and visualization** with **NetworkX** and **matplotlib**: nodes for artists and releases, edges for collaboration credits, genre-based node coloring via matplotlib colormaps. The notebook keeps its successive refinement iterations of the graph rendering (node sizing, colormap legends, escaping of special characters in labels), showing how the final layout was reached.

Data comes live from the API — no third-party dataset files are included in this repository.

### MusicBrainz User-Agent requirement

The MusicBrainz API [requires an identifying `User-Agent` header](https://musicbrainz.org/doc/MusicBrainz_API/Rate_Limiting) with contact information on every request. The notebook builds it as `MiAplicacion/1.0 (<email>)` from the `user_email` variable, which is set to the placeholder `your_email@example.com` — **replace it with your own contact email before running**, or requests may be rejected or throttled.

## Tech stack

- Python (developed in Google Colab)
- requests
- NetworkX
- matplotlib
- NumPy

## How to run

1. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```
2. Open `musicbrainz_collab_graphs.ipynb` (Jupyter or Google Colab). The original run used a Google Drive mount; outside Colab, skip the `google.colab.drive` cell and change the `/content/drive/MyDrive/...` paths to a local folder.
3. Set `user_email` in the data-collection cell to your own email (see the User-Agent note above).
4. Run the data-collection cell to fetch and save `artist_data.json`, then run the graph cells — each one loads that JSON and draws a variant of the collaboration network.

## Repository structure

```
musicbrainz-collab-graphs/
├── musicbrainz_collab_graphs.ipynb   # API data collection + graph visualizations (narrative in Spanish)
├── requirements.txt
└── README.md
```
