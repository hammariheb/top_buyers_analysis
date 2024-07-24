# Analyse des Top Acheteurs
## Description du Projet
Ce projet a pour objectif d'identifier les top acheteurs d'une entreprise en utilisant une analyse exploratoire des données et un modèle RFM personnalisé (Récence, Fréquence, Montant et Nombre de produits). 
Le projet inclut plusieurs étapes allant du nettoyage des données à la visualisation des tendances d'achat, en passant par l'analyse des corrélations et la mise en place d'un modèle pondéré RFM.

## Structure des Fichiers
product.csv: Contient les informations sur les produits.

coupon.csv: Contient les informations sur les coupons utilisés par les clients.

order.csv: Contient les informations sur les commandes passées par les clients.
## Étapes de l'Analyse
### Nettoyage des Données:

Importation des fichiers CSV en spécifiant le séparateur afin de lire correctement les fichiers.

Traitement des valeurs manquantes.

Traitement des doublons.

Traitement du type de quelques colonnes.

### Analyse Exploratoire des Données (EDA):

1. Visualisation des Statuts de Commande:

La première visualisation est un diagramme à barres qui montre les deux statuts de commandes : "Seller_paid" (commande confirmée et acheteur payé) et "cancelled" (commande annulée).

2. Quantification et Exploration des Critères des Acheteurs:
   
Pour comprendre les tendances d'achat et détecter les anomalies potentielles, j'ai créé un dataframe regroupant les informations suivantes par acheteur :

Montant total d'achat, 
Nombre de commandes, 
Moyenne de la commande, 
Nombre de produits achetés par commande, 
Nombre de coupons utilisés, 

J'ai ensuite visualisé ces critères côte à côte avec des boxplots pour observer la dispersion des données et les tendances associées.

3. Analyse des Boxplots:
   
Les boxplots révèlent une grande variation des données, en particulier pour le montant d'achat et la moyenne de commande par client, ce qui est confirmé par des écarts types respectifs de 80 et 23. Cela implique une divergence significative dans les comportements d'achat des clients. Bien que l'IQR (Intervalle Interquartile) des différents critères soit relativement faible (par exemple, 75% des montants d'achat sont en dessous de 77 euros), le montant maximal payé par un client a atteint environ 5190 euros.

5. Matrice de Corrélation:

Pour explorer les relations entre les différents critères, j'ai créé une matrice de corrélation :

Montant total d'achat et nombre de commandes : 0.8 - Forte corrélation positive, indiquant qu'à mesure que le nombre de commandes augmente, le montant total d'achat tend à augmenter également.
Nombre de commandes et nombre de produits achetés par commande : 0.77 - Forte corrélation positive, indiquant que lorsque le nombre de commandes augmente, le nombre de produits achetés augmente également.
Nombre de commandes et moyenne de la commande : -0.1 - Faible corrélation négative, suggérant que la moyenne de la commande n'est pas fortement influencée par le nombre de commandes.
Nombre de produits et moyenne de la commande : -0.077 - Faible corrélation négative, indiquant que la moyenne de la commande n'est pas fortement influencée par le nombre de produits.

Les corrélations fortes (0.8 et 0.77) montrent que le nombre de commandes est un bon indicateur à la fois du montant total des achats et du nombre de produits achetés. Ces relations peuvent être utilisées pour prédire le comportement d'achat des clients et pour segmenter les clients selon leur valeur.

5. Visualisations avec lmplot:
   
J'ai utilisé la fonction lmplot de seaborn pour visualiser les relations entre différents critères. Une illustration intéressante montre une relation entre la moyenne de commande par client et le nombre de produits achetés. La majorité des clients semblent s'intéresser aux produits moins chers, ce qui est confirmé par les moyennes de commande les plus basses. De plus, cette population achète un plus grand nombre de produits par rapport aux clients ayant une moyenne de dépense supérieure.

Un autre graphique montre que la majorité des clients ayant dépensé des montants élevés n'utilisent pas particulièrement les coupons. Cela pourrait indiquer qu'il serait bénéfique d'explorer les raisons potentielles de ce comportement.

6. Analyse des Catégories de Produits:

Pour identifier les catégories de produits les plus vendus, j'ai créé un diagramme en secteurs pour les 20 produits les plus vendus. On remarque que près de 30% des produits sont des couches jetables, 10.6% des produits sont des pyjamas et vêtements de nuit, et le reste est réparti de manière presque équitable entre 8.8% et 7%.

### Calcul du RFPM score afin de distinguer les tops acheteurs

Dans cette partie de l'analyse, j'ai mis en place un modèle RFPM pondéré pour évaluer la valeur des clients en fonction de leur comportement d'achat. Le modèle RFPM (Récence, Fréquence, Montant et nombre de produits) est une technique de segmentation client qui permet d'identifier les clients les plus précieux en se basant sur 4 critères principaux :

Récence (R) : Temps écoulé depuis la dernière commande du client. Les clients ayant effectué des achats récemment sont généralement plus susceptibles de refaire un achat.

Fréquence (F) : Nombre total de commandes passées par le client. Les clients qui achètent plus fréquemment sont souvent plus fidèles.

Montant (M) : Valeur totale des achats effectués par le client. Les clients dépensant plus d'argent sont considérés comme plus précieux.

PS: j'ai ajouté à cela le nombre de produits (P) étant donné que le nombre de produits acheté est une métrique importante pour l'entreprise.

#### Pourquoi le Modèle RFPM ?
Le modèle RFPM est utilisé pour:

1. Identifier les meilleurs clients :

 En combinant les scores de récence, de fréquence, de montant et de nombre de produit, j'ai pu donc déterminé quels clients sont les plus précieux pour l'entreprise.
2. Segmenter les clients : 

Cela permet de créer des segments de clients basés sur leur comportement d'achat et de cibler ces segments avec des stratégies marketing spécifiques.
3. Prédire le comportement futur des clients : 

En comprenant les comportements passés, nous pouvons mieux anticiper les actions futures des clients.
4. Pondération des Critères:

 En combinant les scores de récence, de fréquence, de montant et de nombre de produit, j'ai pu donc déterminé quels clients sont les plus précieux pour l'entreprise.
3. Segmenter les clients : 
Cela permet de créer des segments de clients basés sur leur comportement d'achat et de cibler ces segments avec des stratégies marketing spécifiques.
4. Prédire le comportement futur des clients : 
En comprenant les comportements passés, nous pouvons mieux anticiper les actions futures des clients.
5. Pondération des Critères:

Pour affiner notre modèle RFM, nous avons attribué des poids spécifiques à chaque critère, ainsi qu'au nombre de produits achetés :

Montant (M) : Pondéré à 0.4

Fréquence (F) : Pondéré à 0.3

Récence (R) : Pondéré à 0.2

Nombre de produits (P) : Pondéré à 0.1

Ces pondérations permettent de donner plus d'importance aux critères que nous jugeons plus influents dans l'évaluation de la valeur des clients.

#### Analyse des Top 5% des Clients
J'ai sélectionné les top 5% des clients en fonction de leur score RFPM pondéré. Pour ces clients, j'ai effectué les analyses suivantes :

1. Violin Plot :

Représente la distribution des montants d'achat, du nombre de commandes et du nombre de produits pour les top 5% des clients.
On remarque que la grosse concenration du montant d'achat varie approximativement de 100 à 400 euros par client tandis que le nombre de commande varie approximativement de 5 à 20 commandes par client.

2. Histogrammes avec Densité :

C'est une illustration de la distribution des montants d'achat, du nombre de commandes et du nombre de produits pour les top 5% des clients 
avec la densité des données pour mieux comprendre les tendances au sein de ce segment de clients.
Ces visualisations nous aident à identifier les caractéristiques communes des clients les plus précieux et à mieux comprendre leurs comportements d'achat.

## Conclusion
Ce projet démontre l'importance d'une analyse approfondie des données clients pour identifier les comportements d'achat, segmenter les clients et optimiser les stratégies marketing. En utilisant des techniques de visualisation avancées et un modèle RFPM pondéré, nous avons pu obtenir des insights précieux sur les clients les plus précieux de l'entreprise. Ces insights peuvent être utilisés pour prendre des décisions stratégiques et améliorer la performance globale de l'entreprise.
