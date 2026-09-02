## Projet de recherche : Reconstruction d'ordre temporel dans des séquences vidéo altérées

# Objectif:

L'objectif principal de ce travail est de développer un algorithme capable de reconstituer la vidéo d'origine à partir d'une séquence mélangée . Cette ambition s'étend au-delà de la simple reconstruction, car l'algorithme doit être conçu dans une optique générale, permettant son application à d'autres vidéos présentant des altérations similaires.

# Enjeux:

Élaborer des mécanismes de détection et de correction des altérations introduites, qu'elles soient dues au mélange des images ou à l'ajout d'éléments étrangers. 

La conception de l'algorithme devra intégrer des éléments de traitement d'image, de séquençage vidéo, et potentiellement d'apprentissage automatique pour identifier les altérations.

# Types d’altérations:

- **Réarrangement des Images**
- **Insertion d'Images Étrangères**

# Plan de Recherche:

Pour aborder les différentes parties de la problématique on fera :

- Une revue littéraire pour contextualiser les défis rencontrés et les solutions envisagés jusqu’à présent
- Selection de méthodes et algorithmes
- Évaluation des résultats ( Performances, capacité d’adaptation à d’autres scénarios )

# Tâches clés:

- Détection des objets clés ( images vs video )
- Suivi d'objets
- Regroupement sémantique
- Modélisation de la temporalité
- Optimisation
- Restauration

# Approche 0.0 :

→ Division de la video en images

1. **Détection de visage et extraction de boîtes englobantes :**
    - Utilisation de cascades de Haar pré-entrainées pour la détection de visages.
2. **Tri spatial :**
    - Trier les boîtes englobantes en fonction de leurs caractéristiques spatiales. Cela peut impliquer un tri basé sur la position des centres des boîtes englobantes, les coins ou d'autres attributs spatiaux.
3. **Ordonnancement:**
    - Combinez l'information de tri spatial avec les résultats de la correspondance des caractéristiques pour établir l'ordre correct des images. Cette étape peut impliquer l'affinement de l'ordre en fonction de la cohérence temporelle et des trajectoires d'objets.

# Approche 0.1:

→ **Capture des images à partir de la vidéo :**

1. **Détection du visage et extraction de la boîte englobante :**
    - Utilisation de cascades de Haar pré-entrainées pour la détection du visage.
2. **Tri spatial :**
    - Triez les boîtes englobantes en fonction de leurs caractéristiques spatiales. Cela peut impliquer un tri basé sur la position des centres, des coins ou d'autres attributs spatiaux des boîtes englobantes.
3. **Ordonnancement :**
    - Combinez les informations de tri spatial avec les résultats de la correspondance de caractéristiques pour établir l'ordre correct des images. Cette étape pourrait impliquer un affinement de l'ordre en fonction de la cohérence temporelle et des trajectoires des objets.

# Approche 1:

1. **Détection d'objets et extraction de boîtes englobantes :**
    - Utilisation d'un algorithme de détection d'objets pour identifier et extraire des boîtes englobantes autour des objets ou des régions d'intérêt dans chaque image.
2. **Extraction de caractéristiques des boîtes englobantes :**
    - Extraction des caractéristiques du contenu à l'intérieur de chaque boîte englobante. Cela pourrait inclure des histogrammes de couleurs, des caractéristiques de texture ou des caractéristiques profondes extraites d'un réseau neuronal pré-entraîné.
3. **Correspondance de caractéristiques :**
    - Application de techniques de correspondance de caractéristiques entre les images consécutives pour identifier les similitudes et faire correspondre les objets entre les images. Cela aide à établir des relations temporelles.
4. **Tri spatial :**
    - Triez les boîtes englobantes en fonction de leurs caractéristiques spatiales. Cela implique un tri basé sur la position des centres des boîtes englobantes.
5. Reconstitution de la vidéo:
    - Reconstruction de la vidéo en fonction de leurs caractéristiques spatiales.

# Approche 2.0:

→ **Capture des images à partir de la vidéo :**

1. **Suivi d'objets :** À chaque image suivante, utilisez le tracker pour prédire la nouvelle position des boîtes englobantes en se basant sur les informations de la frame précédente. Cela se fait en mettant à jour les positions des boîtes englobantes en fonction du mouvement apparent de l'objet.
2. **Tri spatial et ordonnancement temporel :** Une fois toutes les images traitées, triez les objets suivis en fonction de leurs positions spatiales (par exemple, les coordonnées du centre de la boîte englobante) et établissez l'ordre temporel des objets pour reconstruire le mouvement global dans la vidéo.

# Approche 2.1:

→ Division de la video en images

1. **Suivi d'objets :** À chaque image suivante, utilisez le tracker pour prédire la nouvelle position des boîtes englobantes en se basant sur les informations de la frame précédente. Cela se fait en mettant à jour les positions des boîtes englobantes en fonction du mouvement apparent de l'objet.
2. **Tri spatial et ordonnancement temporel :** Une fois toutes les images traitées, triez les objets suivis en fonction de leurs positions spatiales (par exemple, les coordonnées du centre de la boîte englobante) et établissez l'ordre temporel des objets pour reconstruire le mouvement global dans la vidéo.

## Evaluation des approches et résultats:

Les résultats ont été évalué suivant leur capacité à restituer la vidéo demandée mais aussi à s'adapter à de nouvelles vidéos qui auraient suivi le même traitement. Le fichier Test.ipynb dans le dossiers approches connexes permet de générer les fichiers visuels de test.

# **Approche 0.0 :**

**Avantages :**

- **Simplicité de Prétraitement :** La division de la vidéo en images simplifie le processus de prétraitement, permettant un accès facile aux images individuelles
- Flexibilité de traitement: plus e contrôle sur le paramétrage des images.
- **Utilisation de Cascades de Haar :** Les cascades de Haar sont rapides et efficaces pour la détection de visages, ce qui peut convenir à des applications simples.

**Inconvénients :**

- **Limitation de la Détection de Visage :** La détection de visage peut être limitée pour des scénarios avec des objets variés. Donc approche optimale pour cette vidéo mais pas généralisable pour d’autres de contextes différent:

# **Approche 0.1 :**

**Avantages :**

- **Prétraitement simple :** Partage les avantages de la simplicité de la division de la vidéo en images.
- **Utilisation de Cascades de Haar :** La détection de visage via les cascades de Haar offre une méthode rapide et accessible.

**Inconvénients :**

- **Prétraitement non flexible :** on n’a pas l’accès au nombre de Strides au cadres capturés
- **Limitations de la Détection de Visage :** Les mêmes limitations que l'approche 0.0 en termes de détection de visage limitée.
- **Sensibilité à la Qualité de la Vidéo :** Sensible à la qualité et à la résolution de la vidéo, pouvant affecter la détection.

Conclusion Approche 0 : Il est mieux de diviser a video en images avant de les traiter, La partie Object détection doit être plus généralisable 

# **Approche 1 :**

**Avantages :**

- **Diversité d'Objets :** La détection d'objets avec YOLO permet de traiter une variété d'objets.
- **Utilisation de Caractéristiques :** L'extraction de caractéristiques offre une meilleure compréhension du contenu des boîtes englobantes.

**Inconvénients :**

- **Calcul Intensif :** Les algorithmes de détection d'objets peuvent être plus intensifs en calcul.

# **Approche 2:**

**Avantages :**

- **Suivi d'Objets :** Le suivi d'objets permet de conserver la continuité spatiale et temporelle des objets dans la vidéo.
- **Réduction du Bruit :** Le suivi peut aider à réduire le bruit en éliminant les détections incorrectes.

**Inconvénients :**

- **Défis de Suivi :** Le suivi peut rencontrer des défis dans des scénarios avec des mouvements rapides ou des changements drastiques L’algorithme marche bien tant qu’on est dans la meme scene mais des que l’arrière-petit-enfant plan change le suivi n’est plus valide.

Approche 2.0 vs 2.1: Pour le tracking il est toujours mieux d’avoir les images au lieu de traiter la videos en frames

# **Conclusion et perspectives:**

L'approche 1, qui utilise la détection d'objets et l'extraction de caractéristiques, semble offrir une meilleure adaptabilité à une variété de scénarios grâce à la diversité d'objets traités. Cependant, le choix de l'approche dépend des spécificités de la tâche et des compromis entre la complexité de traitement et la robustesse aux variations de scénarios. Pour ce qui est des points d’améliorations, on pourrait:

- Combiner entre la détection et des algorithmes plus robustes de tracking
- **Adapter à d'autres Types d’altérations**
- Ordonnancement dans le temps
- Estimation de la trajectoire
