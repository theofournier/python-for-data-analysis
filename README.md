# python-for-data-analysis


# Contexte

Dans le cadre du cours Python for Data Analysis, il est demandé de faire une analyse d'un dataset.
L'analyse consiste à visualiser, préparer et modéliser les données ainsi qu'une optimisation des performances des modèles.


# Base de données
### Pen-Based Recognition of Handwritten Digits

C'est une collection de 250 caractères par 44 écrivains. 
Pour ceci, ils ont utilisés un écran tactile détecteur de pression de 500 par 500 pixel sur lequel les écrivains ont pu écrire ces caractères.
L'écran renvoie des coordonnées x et y toutes les 100 millisecondes.
Les 10 premiers caractères de chaque écrivains ne sont pas pris en compte.

Sur ces données, ils appliquent une normalisation pour en faire une représentation invariants au translation et distorsions.
Les nouvelles données sont des coordonnées dont les valeurs sont entre 0 et 100. Usuellement, x reste dans cette intervalle car il y a plus de caractères grand que large.

Pour former et tester les classificateurs, il faut représenter les chiffres en tant que vecteurs caractéristiques de longueur constantes.
Ils ont utilisé la technique de rééchantillonnage des points (x_t, y_t).
Ils ont effectué un rééchantillonnage spatial (points régulièrement espacés en longueur d'arc) grâce à une simple interpolation linéaire entre pairs de points.
Les charactères sont ainsi représenté comme une séquence de T points : (x_t, y_t)_{t=1}^T régulièrement espacés dans l'espace en longueur d'arc.

Ainsi le vecteur à une taille de 2*T, 2 fois le nombre de points rééchantillonner.
Ils ont fait un rééchantillonnage spatial avec T=8.

Finalement, le dataset est composé de 16 attributs en entrés de type entiers entre 0 et 100 et de 1 attribut de classe qui le code de classe compris entre 0 et 9.

Nombre d'instance et distribution de classe : 
		Training dataset :  7 494 lignes
			Classe:
				0:  780
				1:  779
				2:  780
				3:  719
				4:  780
				5:  720
				6:  720
				7:  778
				8:  719
				9:  719
		
		Test dataset :  3 498 lignes
			Classe:
				0:  363
				1:  364
				2:  364
				3:  336
				4:  364
				5:  335
				6:  336
				7:  364
				8:  336
				9:  336


# Objectifs
La cible à prédire est donc un code de classe.
Les données en entrées sont déjà préparés pour appliquer un modèle de machine learning.
Les features n’ont pas de signification seules. Elles doivent être traitées ensemble. C’est donc compliqué de faire une visualisation des données compréhensive. Nous allons pouvoir par exemple montrer la répartition de chaque feature.
Le dataset est déjà prêt pour l’utilisation de modèles de machine learning. Il n’y a donc pas de préparation à faire.
Nous allons appliqué différents modèles de machine learning, comme le K-NN, Random Forest et du Deep Learning avec Keras.
Et enfin nous optimiserons les performances grâces à des courbes ROC et des matrices de corrélations.


# Méthodologie

## Importation des données

Nous utilisons la librairie Pandas pour importer nos csv de train et test dans des Data Frame.
Il n'y a aucun NA dans les données et ils sont composé uniquement d'entier.

Nous fusionnons les dataset de train et test pour faire la visualisation des données et ainsi avoir plus de données à traiter.


## Visualisation des données
### Répartition des classes

![Répartition des classes](/img/repartition_des_classes.png)

Nous observons que toutes les classes sont homogénétiquement répartie ce qui permettra d'avoir des résultats plus efficace lors des modèles de prédiction.


### Répartition des valeurs
Ce graphique montre pour chaque features, les valeurs d'entiers sachant qu'ils sont tous compris entre 0 et 100.

![Répartition des valeurs](/img/repartition_des_valeurs.png)
Nous observons une que les valeurs sont en plus grand nombre aux extrêmes ainsi qu'au milieu.


## Modélisation
On sépare les données en features et prédiction.

### K-NN

Dans un premier nous déterminons la meilleur valeur de K voisinage.
![K-NN Meilleurs K](/img/k_nn.png)
Nous trouvons un K=3 pour une précision de 0.978.


### Random Forest
Dans un premier nous déterminons la meilleur valeur de N estimators.
![Random Forest Meilleurs N](/img/random_forest.png)
Nous trouvons un K=56 pour une précision de 0.967.


### Deep Learning
Notre modèle Sequential est composé de deux couches Dense avec activation softmax.
L'erreur est déterminer par un categorical_crossentropy.
On obtient une précision de 0.397


# Conclusion
Grâce à nos observations, nous pouvons en conclure que notre modèle K-NN est performant, et il est proche des résultats obtenus par les créateurs du dataset.

Les données ne permettent pas d’exploration approfondie. Notamment, ils n’est pas possible de supprimer ou d’ajouter des features car elles sont dépendante les unes des autres du caractère du quel ils proviennents.
