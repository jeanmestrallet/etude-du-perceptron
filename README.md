# Du perceptron binaire aux réseaux de neurones

**Géométrie des solutions trouvées par les algorithmes locaux**

Projet personnel de Jean Mestrallet (ENS Paris-Saclay, M1 de physique), 2026.

Quand un algorithme d'apprentissage trouve une solution, laquelle trouve-t-il ? Ce projet étudie cette question sur le perceptron binaire, puis sur un réseau de neurones à poids continus. Il montre que, dans les deux cas, les algorithmes locaux ne trouvent pas une solution quelconque : ils sont attirés vers les régions larges de l'espace des solutions.

Le rapport complet est dans [`rapport.pdf`](rapport.pdf).

## Contenu

| Partie | Sujet | Notebook |
|---|---|---|
| I | Seuil algorithmique d'une recherche locale sur le perceptron binaire | `notebooks/1_perceptron_binaire.ipynb` |
| II | Calcul de Gardner (méthode des répliques) | analytique, voir le rapport |
| III | Entropie locale : voisinage des solutions trouvées par l'algorithme | `notebooks/1_perceptron_binaire.ipynb` |
| IV | Taille de batch et platitude des minima d'un réseau entraîné par SGD (MNIST, Fashion-MNIST) | `notebooks/2_reseau_de_neurones.ipynb` |

## Principaux résultats

- **Partie I** : une descente locale cesse de trouver des solutions bien avant leur disparition. Le seuil algorithmique mesuré (environ 0,4 à 0,5) est nettement inférieur au seuil d'existence α_c ≈ 0,833.
- **Partie III** : à N = 22, les solutions trouvées par l'algorithme ont en moyenne environ 15 % de solutions voisines de plus que des solutions tirées au hasard. Ce biais n'apparaît que lorsque le problème devient contraint.
- **Partie IV** : à perte d'entraînement égale, les entraînements à petits batchs aboutissent dans des minima plus plats, y compris avec une perturbation proportionnelle à la taille des poids. Cette différence ne se traduit pas par une différence mesurable de précision sur les données de test.

Ces résultats restent limités par les petites tailles étudiées et, pour la partie IV, par un seul entraînement par taille de batch.

## Installation

Python 3, avec :

```
pip install numpy matplotlib torch scikit-learn tqdm jupyter
```

Les jeux de données MNIST et Fashion-MNIST sont téléchargés automatiquement par `sklearn.datasets.fetch_openml` à la première exécution.

## Reproduire les résultats

Ouvrir chaque notebook et exécuter toutes les cellules dans l'ordre. Certains calculs sont longs, en particulier l'énumération exhaustive des solutions (partie III) et l'entraînement des grands batchs jusqu'au seuil de perte (partie IV), qui peut prendre plusieurs heures sur un ordinateur portable.

## Références principales

- E. Gardner, *The space of interactions in neural network models*, J. Phys. A 21, 257 (1988).
- W. Krauth et M. Mézard, *Storage capacity of memory networks with binary couplings*, J. Phys. France 50, 3057 (1989).
- C. Baldassi et al., *Subdominant dense clusters allow for simple learning and high computational performance in neural networks with discrete synapses*, Phys. Rev. Lett. 115, 128101 (2015).
- N. S. Keskar et al., *On large-batch training for deep learning: generalization gap and sharp minima*, ICLR (2017).
