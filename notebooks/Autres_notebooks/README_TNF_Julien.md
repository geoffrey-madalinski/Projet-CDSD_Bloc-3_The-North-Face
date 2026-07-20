![The North Face](tnf_logo.png)

# The North Face — Recommandation produits & Topic Modeling

Projet réalisé dans le cadre du bloc 3 de la certification CDSD (Jedha).

---

## Contexte

The North Face veut booster ses ventes en ligne en améliorant l'expérience sur son site. Deux pistes identifiées : une section "vous aimerez aussi" sur chaque page produit, et une meilleure structuration du catalogue via extraction automatique de thèmes.

---

## Ce que j'ai fait

**Partie 1 — Clustering**

Nettoyage HTML des descriptions produits, preprocessing NLP avec spaCy (lemmatisation, stop words), vectorisation TF-IDF. Clustering DBSCAN avec distance cosine pour regrouper les produits aux descriptions similaires. Wordclouds par cluster pour interpréter les résultats.

**Partie 2 — Système de recommandation**

Fonction `find_similar_items(item_id)` qui retourne 5 produits appartenant au même cluster que le produit sélectionné. Interface simple avec `input()` pour tester les suggestions.

**Partie 3 — Topic Modeling (LSA)**

TruncatedSVD pour extraire les thèmes latents du catalogue. Wordclouds par topic pour visualiser et interpréter chaque thème.

---

## Stack

- Python — Pandas, Matplotlib, WordCloud
- spaCy (`en_core_web_sm`) — preprocessing NLP
- Scikit-learn — TfidfVectorizer, DBSCAN, TruncatedSVD

---

## Structure

```
The_North_Face/
├── data/
│   └── raw/
│       └── sample-data.csv     # 500 descriptions produits
├── docs/
│   └── 02-The_North_Face_ecommerce.ipynb
├── notebooks/
│   └── northface.ipynb
├── reports/
│   └── figures/
└── README.md
```

---

Julien CHARLIER — [(Github : Atomik31)](https://github.com/Atomik31)
