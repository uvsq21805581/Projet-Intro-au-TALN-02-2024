# DEFT2013 Tâche 2 :

SISARITH Elisabeth - STUCKY Nicolas

## Description de la tâche

	La tâche que nous souhaitons réaliser est qu'en donnant une recette au modèle, il nous prédisse le type de cette recette.
    Par exemple, si on lui donne les informations de la recette recette_221358.xml (Feuilleté de saumon et de poireau, sauce aux crevettes), le modèle nous renvoie "Plat principal".

## Statistiques corpus

	Pour le train, nous avons pris 80% des recettes du csv de base, et les 20% restant nous ont servi de dev.
    Nous avons ensuite utilisé le csv de test donné pour l'évaluation.
	
    Nous avons gardé les proportions de chaque type dans le train et le dev, c'est-à-dire que s'il y avait 60% de plat dans le document train original, il y aura environ 60% de plat dans le train et le dev.

## Méthodes proposées

### Run1.1: baseline : Aléatoire

	Il n'y a ni descripteur, ni classifieur. La prédiction est totalement aléatoire.

### Run1.2: baseline : Classe majoritaire

    Il n'y a ni descripteur, ni classifieur. On prédit le type que l'on trouve majoritairement dans le train.
    Étant donné que les résultats de la classe majoritaire sont moins bon que ceux de l'aléatoire, nous prendrons ce dernier en baseline.

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
| base 1   |  0.33 |
| base 2   |  0.21 |
| METH 2   |  0.63 |
| METH 3   |  0.69 |
| METH 4   |  0.76 |
| METH 5   |  0.57 |
| METH 6   |  0.86 |

### Analyse de résultats

La précision permet de connaitre la proportion d'erreur dans les positifs que l'on a prédit (une précision de 1 peut signifier que l'on a correctement prédit les éléments de ce type, ou que nous n'en avons trouvé aucun).

Le rappel permet de connaitre la proportion de positif que l'on trouvé (si c'est égal à 1, on a trouvé tous les positifs de ce type, 0 si on en a touvé aucun).

La f-mesure (f1-score) est la combinaison de la précision et du rappel, ce qui nous permet de comparer les différentes méthodes de classification.

### Naive Bayes Multinomial

![NB.png](https://github.com/uvsq21805581/Projet-Intro-au-TALN-02-2024/blob/175d54ba358b6115526857cbd1624eddefbf8ed5/figures/NB.png) ![NB normalise.png](https://github.com/uvsq21805581/Projet-Intro-au-TALN-02-2024/blob/175d54ba358b6115526857cbd1624eddefbf8ed5/figures/NB%20normalise.png)
	
Avec la normalisation des recettes, nous pouvons voir que la f-mesure est légèrement améliorée, passant de 0.63 à 0.69. Ces deux modèles sont plus performants que l'aléatoire, mais il y a une marge d'amélioration possible.

L'erreur principale des deux modèles est qu'ils ont tendance à prédire "Plat principal" pour les entrées.

La normalisation permet de couvrir quasiment tous les desserts, cependant, nous remarquons aussi qu'il y a un peu plus de faux positifs pour ce type. Ce défaut est également visible pour les entrées de manière plus atténué, tout comme la petite amélioration du rappel des entrées. 

#### Forêt d’arbres de décision

![Foret.png](https://github.com/uvsq21805581/Projet-Intro-au-TALN-02-2024/blob/564e98f972a8a8aa55d0b4c595b3a4b90619b343/figures/Foret.png)

La f-mesure étant de 0.76, il y a encore une fois une amélioration de classification.

Tout comme les Naive Bayes Multinominaux, le modèle Forêt d’arbres de décision prédit les entrées en plat, mais le fait un peu moins.

#### Réseau de neurones

![Reseau Neurones.png](https://github.com/uvsq21805581/Projet-Intro-au-TALN-02-2024/blob/564e98f972a8a8aa55d0b4c595b3a4b90619b343/figures/Reseau%20Neurones.png)

Avec son f1-score de 0.57, le modèle de réseau de neurones est relativement peu performant, bien que meilleur que l'aléatoire.

Ce modèle ne parvient pas à prédire une entrée, ce qui explique la précision de 1 (il n'y a aucune erreur dans les prédictions d'entrées puisqu'il n'y a pas eu d'entrées prédites). 

Il semblerait que la principale difficulté pour les modèles est de prédire s'il s'agit d'une entrée ou d'un plat. Pour les desserts, les modèles font assez peu d'erreurs.

En augmentant l'epoch à 100, nous avons réussi à obtenir une f-mesure de 0.84.

#### SVC

![SVC.png](https://github.com/uvsq21805581/Projet-Intro-au-TALN-02-2024/blob/564e98f972a8a8aa55d0b4c595b3a4b90619b343/figures/SVC.png)

Le modèle SVC est celui qui obtient le meilleur f1-score, qui est de 0.86.

Celui-ci parvient à mettre plus d'entrée dans le bon type. Cette amélioration du rappel s'accompagne d'une légère augmentation de faux positifs aux entrées, ce qui fait baissé sa précision.

#### Analyse générale

Nous pouvons observer que ces méthodes, hormis le SVC, ont du mal avec la classification des entrées qu'ils prédissent comme des plats principaux. En ce qui concerne les desserts, ils parviennent à tous les trouver ou presque (le rappel allant de 0.96 à 1), et font assez peu de faux négatifs, mais comme il font un peu plus de faux positifs, leur précision est un peu moins bonne que leur rappel (de 0.87 à 0.97). 

Étant donné que les erreurs viennent principalement de la différenciation des entrées des plats, nous avons essayé de trouver des règles qui pourrait corriger les erreurs du modèle. Ces règles seraient de la forme "si le titre contient mot1, et recette contient mot2 et que la prédiction était 'Plat Principal', alors prédire 'Entrée'". Pour cela, nous avons analysé les erreurs que SVC, notre meilleur modèle, pouvait faire. Cependant, en testant différents mots, nous nous sommes aperçus que des recettes bien prédites seraient changées en erreurs par cette règle.
    
Au final, nous avons donc décidé de ne pas implémenter de règle pour améliorer SVC.