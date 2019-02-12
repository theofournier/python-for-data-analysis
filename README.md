# python-for-data-analysis


# Contexte

Dans le cadre du cours Python for Data Analysis, il est demandé de faire une analyse d'un dataset.
L'analyse consiste à visualiser, préparer et modéliser les données ainsi qu'une optimisation des performances des modèles.


## Base de données
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
La cible à prédire est donc un code de classe.
Les données en entrées sont déjà préparés pour appliquer un modèle de machine learning.

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


	Précision sur le jeu de test avec un k-nn utilisant la distance Euclidienne comme metric obtenu par les créateurs :

		 k =  1 : 97.74
		 k =  2 : 97.37
		 k =  3 : 97.80
		 k =  4 : 97.66
		 k =  5 : 97.60
		 k =  6 : 97.57
		 k =  7 : 97.54
		 k =  8 : 97.54
		 k =  9 : 97.46
		 k = 10 : 97.48
		 k = 11 : 97.34