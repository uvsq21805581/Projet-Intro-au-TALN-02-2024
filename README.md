# DEFT2013 Tâche 2 :

SISARITH Elisabeth - STUCKY Nicolas

## Description de la tâche

	1 ou 2 exemples de documents (avec leur identifiant)

## Statistiques corpus

	Nombre de document de train/dev/test
	Répartition des étiquettes dans chacun des sous-ensemble

## Méthodes proposées

### Run1: baseline (méthode de référence)

	Description de la méthode:
	- descripteurs utilisés
	- classifieur utilisé

### Run2: Naive Bayes Multinomial (sans normalisation)

    - Les descripteurs utilisés sont les vecteurs TF-IDF des recettes.
    - Le classifieur utilisé est un classifieur de Bayes naïf multinomial.

### Run3: Naive Bayes Multinomial (avec normalisation)

    - Les descripteurs utilisés sont les vecteurs TF-IDF des recettes normalisés.
    - Le classifieur utilisé est un classifieur de Bayes naïf multinomial.

### Run4: Forêt d’arbres de décision (Random Forest)

    - Les descripteurs utilisés sont les vecteurs TF-IDF des recettes.
    - Le classifieur utilisé est un classifieur de forêt aléatoire.

### Run5: Réseau de neurones

    - Le descripteur utilisé est la représentation vectorielle des recettes obtenue à l'aide de 'CountVectorizer()'.
    - Le classifieur utilisé est un réseau de neurones défini par la classe 'RecipeClassifier'.

### Run6: SVC

    - Les descripteurs utilisés sont les vecteurs TF-IDF des recettes.
    - Le classifieur utilisé est un classifieur SVM.

## Résultats

| Run      | f1 Score |
| -------- | --------:|
| baseline |  15,2 |
| METH 2   |  0.63 |
| METH 3   |  0.69 |
| METH 4   |  0.76 |
| METH 5   |  0.57 |
| METH 6   |  0.86 |

### Analyse de résultats

    - Naive Bayes Multinomial
	
        Avec la normalisation des recettes, nous pouvons voir que la f-mesure est légèrement améliorée, passant de 0.63 à 0.69. Ces deux modèles sont plus performants que l'aléatoire, mais il y a une marge d'amélioration possible.

        L'erreur principale des deux modèles est qu'ils ont tendance à prédire "Plat principal" pour les entrées.

        La normalisation permet de couvrir quasiment tous les desserts, cependant, nous remarquons aussi qu'il y a un peu plus de faux positifs pour ce type. Ce défaut est également visible pour les entrées de manière plus atténué, tout comme la petite amélioration du rappel des entrées. 

    - Forêt d’arbres de décision

        La f-mesure étant de 0.76, il y a encore une fois une amélioration de classification.

        Tout comme les Naive Bayes Multinominaux, le modèle Forêt d’arbres de décision prédit les entrées en plat, mais le fait un peu moins.

    - Réseau de neurones

        Avec son f1-score de 0.57, le modèle de réseau de neurones est relativement peu performant, bien que meilleur que l'aléatoire.

        Ce modèle ne parvient pas à prédire une entrée, ce qui explique la précision de 1 (il n'y a aucune erreur dans les prédictions d'entrées puisqu'il n'y a pas eu d'entrées prédites). 

        Il semblerait que la principale difficulté pour les modèles est de prédire s'il s'agit d'une entrée ou d'un plat. Pour les desserts, les modèles font assez peu d'erreurs.

    - SVC

    Le modèle SVC est celui qui obtient le meilleur f1-score, qui est de 0.86.

    Celui-ci parvient à mettre plus d'entrée dans le bon type. Cette amélioration du rappel s'accompagne d'une légère augmentation de faux positifs aux entrées, ce qui fait baissé sa précision.
