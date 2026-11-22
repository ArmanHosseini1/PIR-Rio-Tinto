# PIR-Rio-Tonto

Projet de Recherche et d'Innovation de 5A à l'INSA Toulouse, réalisé par Arman Hosseini et Guillaume Staub. Ce projet portait sur la comparaison de différentes méthodes de clustering par pixel d'images de la mine de Rio Tinto en Espagne. Les images étaient des images multispectrales et hyperspectrales issues de satellites SENTINEL-2 et EnMAP. Il a été mené conjointement avec nos tuteurs de l'ONERA Sophie Fabre et Kareth Leon-Lopez.

Nous avons comparé plusieurs architectures : K-means sur l'information issue de chaque pixel, K-means appliqué dans l'espace latent suite au passage séparé de chaque pixel dans un encodeur, K-means appliqué dans l'espace latent suite au passage de patchs de pixels dans un encodeur convolutionnel 2D, Deep Embedded Clustering simple sur les patchs de pixels.
