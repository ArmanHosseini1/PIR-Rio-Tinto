# Self-Supervised Clustering of Multispectral & Hyperspectral Satellite Imagery (Rio Tinto)

> 🇬🇧 [English Version](#-english) | 🇫🇷 [Version Française](#-français)

---

## 🇬🇧 English

### Overview
Final-year Research & Innovation Project (**PIR**, 5th year at **INSA Toulouse**), conducted by **Arman Hosseini** and **Guillaume Staub**, in collaboration with **ONERA** supervisors **Sophie Fabre** and **Kareth Leon-Lopez**.

This project explores **self-supervised learning** for pixel-wise clustering of soil and vegetation on the polluted **Rio Tinto mining site (Spain)**, with the goal of achieving accurate land-cover clustering without manual annotations.

### Data & Preprocessing
We leveraged two passive optical satellite imagery sources:
* **SENTINEL-2B** (multispectral imagery)
* **EnMAP** (hyperspectral imagery)

After preprocessing, a dedicated masking pipeline was applied to separate **vegetation**, **soil**, and **other** surfaces prior to clustering.

> **Note on Data:** Raw satellite imagery files (`.tif`, `.img`, `.hdr`) are excluded from this repository due to size and confidentiality constraints.

### Methods Compared
1. **Baseline K-Means:** Applied directly to raw pixel spectral features.
2. **Pixel-by-Pixel Autoencoder (AE PbP) + K-Means:** K-Means applied in the latent space after encoding each pixel independently.
3. **2D Convolutional Autoencoder (AE Conv2D) + K-Means:** K-Means applied in the latent space after encoding spatial pixel patches through a 2D convolutional encoder.
4. **Deep Embedded Clustering (DEC):** Joint optimization of image reconstruction and clustering on pixel patches.

### Quantitative Results

#### SENTINEL-2 Results (10k pixels sample)

| Metric / Class | K-Means | K-Means on AE PbP Latent Space (`dim=4, epochs=25`) | K-Means on AE Conv2D Latent Space (`dim=4, epochs=20`) | AE Conv2D + DEC (`dim=16, ae=25, clust=3`) |
| :--- | :---: | :---: | :---: | :---: |
| **Silhouette — Vegetation (k = 5)** | 0.33 | **0.34** | 0.25 | 0.17 |
| **Silhouette — Soil (k = 15)** | **0.25** | 0.22 | 0.022 | -0.092 |
| **Silhouette — Other (k = 5)** | **0.32** | 0.30 | 0.18 | -0.051 |
| **ARI — Partial Vegetation** | 0.4418 | 0.5466 | **0.5488** | 0.4362 |

#### EnMAP Results (max 10k pixels sample)

| Metric / Class | K-Means | K-Means on AE PbP Latent Space (`dim=16, epochs=25`) | K-Means on AE Conv2D Latent Space (`dim=16, epochs=20`) | AE Conv2D + DEC (`dim=64, ae=25, clust=3`) |
| :--- | :---: | :---: | :---: | :---: |
| **Silhouette — Vegetation (k = 6)** | **0.30** | 0.28 | 0.15 | -0.022 |
| **Silhouette — Soil (k = 15)** | **0.22** | 0.20 | 0.007 | -0.15 |
| **Silhouette — Other (k = 6)** | **0.51** | 0.46 | 0.17 | 0.011 |

### Key Takeaways
* While standard **K-Means** achieves the highest Silhouette scores on raw spectral features, it is less accurate for actual class identification.
* When evaluated against partial ground truth on SENTINEL-2 vegetation (**ARI**), **Autoencoder-based latent clustering methods clearly outperform K-Means** (`0.5488` and `0.5466` vs. `0.4418`).
* The **DEC** model underperformed, likely due to an overly simple architecture for joint reconstruction and clustering.
* **Conclusion:** A **hybrid approach** (learning a compact latent representation with an Autoencoder before applying classical clustering) proves to be the most robust solution.

---

## 🇫🇷 Français

### Présentation du projet
Projet d'Initiation à la Recherche et d'Innovation (**PIR** de 5A à l'**INSA Toulouse**), réalisé par **Arman Hosseini** et **Guillaume Staub**, en collaboration avec nos tuteurs de l'**ONERA** **Sophie Fabre** et **Kareth Leon-Lopez**.

Ce projet explore l'**apprentissage auto-supervisé** pour le clustering par pixel des sols et de la végétation sur le site minier pollué de **Rio Tinto (Espagne)**, avec pour objectif d'obtenir un clustering pertinent malgré l'absence d'annotations manuelles.

### Données et pré-traitement
Nous avons exploité deux sources d'imagerie optique passive :
* **SENTINEL-2B** (imagerie multispectrale)
* **EnMAP** (imagerie hyperspectrale)

Après une phase de pré-traitement, un masquage spécifique a été appliqué afin de séparer la **végétation**, les **sols** et les **autres** surfaces avant le clustering.

> **Note sur les données :** Les images satellites brutes (`.tif`, `.img`, `.hdr`) ne sont pas incluses dans ce dépôt pour des raisons de volume et de confidentialité.

### Méthodes comparées
1. **K-Means classique :** Appliqué directement sur les valeurs spectrales brutes de chaque pixel.
2. **Auto-encodeur pixel-par-pixel (AE PbP) + K-Means :** K-Means appliqué dans l'espace latent après encodage individuel de chaque pixel.
3. **Auto-encodeur Convolutif 2D (AE Conv2D) + K-Means :** K-Means appliqué dans l'espace latent après encodage de patchs de pixels par un encodeur convolutionnel 2D.
4. **Deep Embedded Clustering (DEC) :** Optimisation conjointe de la reconstruction d'image et du clustering sur des patchs de pixels.

### Principaux enseignements
* Bien que le **K-Means simple** obtienne les meilleurs scores Silhouette, il s'avère moins précis pour l'identification réelle des classes.
* En comparaison avec une vérité terrain partielle sur la végétation de l'image SENTINEL-2 (**ARI**), **les méthodes utilisant un Auto-encodeur surpassent nettement le K-Means** (`0.5488` et `0.5466` contre `0.4418`).
* Le modèle **DEC** a sous-performé, probablement en raison d'une architecture trop simple.
* **Conclusion :** L'**approche hybride** (utiliser un Auto-encodeur pour projeter les données dans un espace latent avant d'appliquer un clustering classique) constitue la solution la plus robuste.
