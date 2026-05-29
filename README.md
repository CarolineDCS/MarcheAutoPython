# Étude du marché de l'automobile aux Etats-Unis

## Présentation du projet

Dans la peau d'un directeur commercial d'un revendeur automobile souhaitant comprendre le marché aux Etats-Unis, on dispose d'un dataset détaillant plus de 588 000 transactions.

## Les données

Voici la description des champs disponibles :
*	year : Année de vente du véhicule
*	make : La marque du véhicule
*	model : Le modèle du véhicule
*	trim : La version spécifique du modèle
*	body : Le type de carrosserie (ex. : SUV)
*	transmission : Le type de transmission
*	vin : Le numéro de châssis du véhicule - identifiant unique
*	state : L'État dans lequel la vente a été réalisée
*	condition : Une évaluation de l'état du véhicule
*	odometer : Le kilométrage (en km ou en miles ?) parcouru par le véhicule
*	color : La couleur extérieure du véhicule
*	interior : La couleur intérieure du véhicule
*	seller : L'identifiant de l'entité qui vend le véhicule
*	mmr : La cote ou le prix de marche du véhicule
*	sellingprice : Le prix de vente final du véhicule
*	saledate : La date de vente du véhicule

## Nettoyage des données
*	Les chaines de caractères (hormis les dates) ont été converties en minuscules afin d'éviter les redondances.
*	Aucune ligne n'est dupliquée.
*	Gestion des VIN : suppression des lignes inexploitables (décalage de colonnes). Les VIN ne sont pas uniques : un même VIN peut apparaitre plusieurs fois en cas de revente du véhicule.
*	Étude des valeurs manquantes : suppression des ventes non abouties.
*	Stratégie de traitement des valeurs NaN : les champs make, model, trim, body et transmission servent à segmenter le marché, mais ne sont pas toujours indispensables à l'analyse globale. Leur absence gêne surtout les analyses fines. Les valeurs NaN ont donc été conservées.
*  Les champs color et interior influencent la valeur de revente, mais leur imputation serait spéculative. Certaines couleurs étant plus recherchées que d'autres, imputer une couleur arbitrairement pourrait fausser les analyses. Les valeurs manquantes ont donc été conservées.
*	Les champs condition et odometer sont plus importants pour comprendre le prix : ils ont été imputés par groupe (année, marque, modèle) à l'aide de la médiane (validée par test IQR).
*	Gestion des dates : le fuseau horaire n'est pas pris en compte (on retient la date telle que vécue par l'acheteur). Les mois et les années ont été extraits.

## Axes d'analyse du marché

Afin d'obtenir des chiffres normalisés, l'analyse porte sur la marge par rapport au prix de l'argus (exprimée en pourcentage), ainsi que sur l'âge du véhicule au moment de la vente.

### Analyse par marque, carrosserie et état du véhicule
*	La marge est en général négative et faible : l'objectif premier semble être de vendre le véhicule plutôt que de récupérer sa valeur a l'argus.
*	Les marques les plus vendues sont, par ordre décroissant : Ford, Chevrolet, Nissan et Toyota.
*	Les types de carrosserie les plus vendus sont les berlines (Sedan, 44,20 % des ventes) et les SUV (26 %), mais la marge médiane reste négligeable dans les deux cas.
*	Les conditions vont de 0 à 49. Pour faciliter l'analyse, cinq catégories ont été définies (de la pire à la meilleure : condition 0 à condition 4). La corrélation entre marge et l'état du véhicule existe mais reste faible. Sans surprise, les véhicules en meilleur état (conditions 3 et 4) sont les plus vendus et affichent la marge positive la plus élevée. Les véhicules en très mauvais état (condition 0) réalisent 40 % de marge positive (mieux que les conditions 1 et 2) et représentent un volume non négligeable (70 415 ventes, soit plus que la condition 1). Les véhicules de condition 1 sont les moins vendus (45 614 ventes) et affichent la marge médiane la plus faible (-16,54 %).
*	Les véhicules à faible kilométrage se vendent le mieux (hormis ceux sous les 10 000 km). Les véhicules entre 70 000 et 125 000 km conservent toutefois un bon volume de vente. La corrélation entre marge et kilométrage reste faible.
*	L'âge du véhicule influe sur le volume de vente : au-delà de 20 ans, les chances de vente sont très faibles. Les véhicules les plus vendus ont entre 1 et 3 ans.

### Analyse par variables catégorielles (carrosserie, marque, transmission, couleur)
*	Les carrosseries les plus vendues (Sedan et SUV) ne sont pas celles qui offrent la meilleure marge médiane.
*	Les modalités testées (carrosserie, marque, transmission, couleur) ont toutes un effet statistiquement significatif sur le prix de vente.
*	À l'exception de Nissan (présent dans les deux tops 10), la marque n'influe pas de la même façon sur la marge et sur le volume de vente.
*	Les véhicules à transmission automatique affichent une meilleure marge médiane et un volume de vente nettement supérieur.
*	Comme en France, les couleurs sobres (noir, blanc, argent, gris) sont les plus vendues. En revanche, ce ne sont pas les couleurs les plus sobres qui génèrent la meilleure marge médiane.
Analyse croisée : kilométrage et état selon la carrosserie
*	Les véhicules en bonne condition affichent une marge positive. Les véhicules en très mauvais état (condition 0) présentent une faible décote par rapport à la condition 1, et se comportent mieux en volume et en marge que cette dernière catégorie.
*	Le volume de vente est corrélé à la condition, quel que soit le type de carrosserie : meilleure est la condition, plus le volume est élevé.
*	Le prix médian est le plus élevé pour les véhicules en meilleur état. Même les SUV en très mauvais état affichent un prix médian relativement élevé. Une fois encore, ce sont les véhicules de condition 1 qui cumulent le pire prix médian, la marge la plus dégradée et le plus faible volume.
*	Le kilométrage impacte le volume de vente de façon similaire quelle que soit la carrosserie, mais le volume est systématiquement plus élevé pour les berlines.
*	Tant que le kilométrage reste inférieur à 300 000, moins le véhicule a de kilomètres, plus le prix de vente médian est élevé.
*	Les SUV avec le moins de kilomètres affichent le prix médian le plus élevé.
*	Le pic de volume de ventes concerne les berlines avec un kilométrage compris entre 30 000 et 40 000 km.

### Analyse temporelle
*	Les données sur l'année 2014 sont incomplètes, ce qui ne permet pas de conclure sur une éventuelle saisonnalité annuelle.
*	De janvier 2014 à juillet 2015, les meilleures ventes ont eu lieu en janvier et février 2015. Elles chutent en avril 2015, rebondissent en juin, puis retombent au niveau d'avril en juillet 2015.
*	Le chiffre d'affaires suit les mêmes tendances que le volume des ventes.

### Analyse géographique
*	La Californie, la Floride et, dans une moindre mesure, la Pennsylvanie et le Texas tirent le marché vers le haut avec de forts volumes de vente.
*	Les États affichant une marge médiane vraiment mauvaise sont peu nombreux : Hawaii, le Massachusetts, le Maryland et New York.

## Conclusions et limites
<img width="1736" height="525" alt="body_volume" src="https://github.com/user-attachments/assets/97a70f25-40a8-4bc7-b3f2-4cb21d671bde" />
