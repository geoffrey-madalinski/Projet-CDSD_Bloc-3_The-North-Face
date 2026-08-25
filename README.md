# The North Face e-commerce - NLP, Clustering & Recommendation

> Mandatory project for **block 3** (Predictive analysis of structured data with
> artificial intelligence) of the French **CDSD certification** - Concepteur
> Développeur en Science des Données | RNCP35288 | JEDHA

NLP analysis of a catalogue of **500 product descriptions** to help The North Face
boost online sales through machine learning: a **recommendation system**
("you may also like…") on each product page, and an automatic **topic extraction**
to restructure the catalogue with more relevant navigation than the current categories.

## Problem statement

The North Face wants to increase online sales using machine learning, with two levers:
a product recommendation engine on each product sheet, and a catalogue reorganisation
based on the automatic extraction of latent themes, offering navigation that is more
relevant than the existing categories.

## Installation

```bash
git clone https://github.com/geoffrey-madalinski/Projet_TheNorthFace.git
cd Projet_TheNorthFace
```

The spaCy English model is required for lemmatisation:

```bash
python -m spacy download en_core_web_sm
```

## Technical stack

- Python - Pandas, NumPy, Matplotlib
- spaCy (`en_core_web_sm`) - text preprocessing & lemmatisation
- scikit-learn - TfidfVectorizer, DBSCAN, TruncatedSVD, cosine_similarity, silhouette_score
- wordcloud - cluster & topic visualisation

## Usage

```bash
jupyter notebook Projet-TheNorthFace_GM.ipynb
```

## Project structure

```
Projet_TheNorthFace/
├── data/
│   └── raw/
│       └── sample-data.csv                 # product descriptions
├── docs/
│   ├── 02-The_North_Face_ecommerce.ipynb   # project statement
├── notebooks/
│   └── Projet-TheNorthFace_GM.ipynb        # main notebook
├── reports/
│   └── figures/                            # wordclouds & data visualization
└── README.md
```

## Data

- **Source**: [Product item data (Kaggle)](https://www.kaggle.com/datasets/cclark/product-item-data)
- **Granularity**: one row = one product
- **Columns**: `id` (product identifier), `description` (marketing text, contains HTML tags)
- **Volume**: 500 product descriptions

## Approach

1. **Loading & text cleaning** - stripping HTML tags, HTML entities, digits and punctuation
2. **NLP preprocessing (spaCy)** - lowercasing, stop-word removal, lemmatisation,
   dropping tokens of 2 characters or less
3. **TF-IDF vectorisation** - `max_features=600`, `min_df=2`
4. **Part 1 - Product clustering (DBSCAN)** - density-based grouping with cosine
   distance, no preset number of clusters, outliers labelled `-1`; quality assessed
   with the silhouette score and interpreted via a wordcloud per cluster
5. **Part 2 - Recommendation system** - `find_similar_items()` returns 5 similar
   products from the same cluster, falling back to cosine similarity for outliers;
   interactive lookup via `input()`
6. **Part 3 - Topic extraction (LSA / TruncatedSVD)** - 15 latent topics, each
   product associated with a mix of themes, dominant topic retained, one wordcloud per topic

## Key findings

| Step | Key finding |
|---|---|
| DBSCAN clustering | ~10 coherent clusters with very few outliers, using cosine distance and no preset cluster count. |
| Cluster interpretation | Wordclouds reveal clear product families (technical base layers, jackets, bags, etc.). |
| Recommendation engine | Same-cluster products give ready-to-use "you may also like" suggestions; cosine fallback handles isolated products cleanly. |
| Topic modeling (LSA) | TruncatedSVD surfaces transversal latent themes; unlike clustering, a product can belong to several topics. |
| Complementarity | Clustering powers recommendations; topic modeling can enrich the site's category system. |

> **Bottom line for The North Face**: cluster-based recommendations are directly
> usable on product pages, while LSA topic modeling offers a complementary, multi-theme
> view that could enrich catalogue navigation.

## Future improvements

- Tune the `eps` and `min_samples` parameters of DBSCAN
- Benchmark DBSCAN against KMeans
- Replace TF-IDF with embeddings (Word2Vec, sentence-transformers) to capture meaning
  beyond exact word matches

## Author

**Geoffrey MADALINSKI** - Certification CDSD (RNCP35288) - JEDHA

---
