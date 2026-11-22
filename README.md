# PIR-Rio-Tonto

Projet de Recherche et d'Innovation de 5A à l'INSA Toulouse, réalisé par Arman Hosseini et Guillaume Staub. Ce projet portait sur la comparaison de différentes méthodes de clustering par pixel d'images de la mine de Rio Tinto en Espagne. Les images étaient des images multispectrales et hyperspectrales issues de satellites SENTINEL-2 et EnMAP. Il a été mené conjointement avec nos tuteurs de l'ONERA Sophie Fabre et Kareth Leon-Lopez.

Nous avons comparé plusieurs architectures : K-means sur l'information issue de chaque pixel, K-means appliqué dans l'espace latent suite au passage séparé de chaque pixel dans un encodeur, K-means appliqué dans l'espace latent suite au passage de patchs de pixels dans un encodeur convolutionnel 2D, Deep Embedded Clustering simple sur les patchs de pixels.

### SENTINEL-2 Results (10k pixels sample)

| Metric / Class | K-means | K-means on AE PbP Latent Space (`dim=4, epochs=25`) | K-means on AE Conv2D Latent Space (`dim=4, epochs=20`) | AE Conv2D + DEC (`dim=16, ae=25, clust=3`) |
| :--- | :---: | :---: | :---: | :---: |
| **Silhouette — Vegetation (k = 5)** | 0.33 | **0.34** | 0.25 | 0.17 |
| **Silhouette — Soil (k = 15)** | **0.25** | 0.22 | 0.022 | -0.092 |
| **Silhouette — Other (k = 5)** | **0.32** | 0.30 | 0.18 | -0.051 |
| **ARI — Partial Vegetation** | 0.4418 | 0.5466 | **0.5488** | 0.4362 |

### EnMAP Results (max 10k pixels sample)

| Metric / Class | K-means | K-means on AE PbP Latent Space (`dim=16, epochs=25`) | K-means on AE Conv2D Latent Space (`dim=16, epochs=20`) | AE Conv2D + DEC (`dim=64, ae=25, clust=3`) |
| :--- | :---: | :---: | :---: | :---: |
| **Silhouette — Vegetation (k = 6)** | **0.30** | 0.28 | 0.15 | -0.022 |
| **Silhouette — Soil (k = 15)** | **0.22** | 0.20 | 0.007 | -0.15 |
| **Silhouette — Other (k = 6)** | **0.51** | 0.46 | 0.17 | 0.011 |
