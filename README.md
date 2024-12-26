## PROJET DE PREDICTION DE COUT DE SINISTRE EN SERVANT DES IMAGES ET DES INFORMATIONS SUR LE VEHICULE ACCIDENTE.

Il s'agit de connaitre le coût de sinistre à allouer à un client en dommage matériel subit par son véhicule.
C'est un projet qui allie à la fois Deep Learning avec les reseaux de neuronnes convolutionnels, Machine Learning, LLM et plus.
Nous avons utlisés plusieurs approches, mais celle alliant ces differentes solutions était la meilleurs.

L'idéal était d'executer le projet dans un environnement virtuel, mais nos contraintes machines et le fait de se deplacer à chaques 
dans differentes environnements et differents serveurs avec chacunes ces exigeances nous conduisait à toujours manipuler différents notebook.

Nous avons été amené à travailler avec des CPU et aussi sur des plateformes comme vastai qui proposaient des GPU propices à nos contraintes.
Pour aller à bout de ce projet, il a été question de mettre en place plusieurs notebook que nous tenterons d'expliquer et de donner leurs utilités en quelques lignes.

### Processus_projet_Tout.ipynb

Ce notebook a permis de faire tous les travaux de traitements de données. C'est d'ici que provient le fichier global.csv qui contient les donnees propres. 
Certes le code continue pour certaines manipulations et certains textes, mais c'est un toute son importance une fois qu'on obtient tous ce fichier.
Dans chaque enregistrement, on des lignes qui contiennent les adresses des images de la voiture accidentée, les informations sur le véhicule et le cout de sinistre.
On aurait pu effectuer tout le traitement ici, mais la tache suivante etait d'associer à chaque adresse l'image qui lui correspondait. Et en le faisant, arriver à un certzin nombre de lignes, le noyau redemarrait pour un probleme de performances machines. Alors, fallait scincder le fichier en plusieurs morceaux(des blocs de 100 lignes) et effecter
l'operation. Le Noyau ne s'interropait plus, mais pour 100 lignes, le traitement beaucoup trop chronophrage. Alors, nous étions dans l'obligation de penser à une solution palliative, l'utilisation des GPU.

### GPU.ipynb

Comme son nom l'indique, les traitements dans ce fichier ont bénéficiés des performances des grandes unités de calcul à savoir les GPU. 
- L'une des premières choses à faire étaient d'associer les vraies images à leur adresses, ce qui necessitait beaucoup de ressources. 
- Ensuite, on a utilisé des CNN, en l'occurence un Resnet18 pour extraire les caractéristiques dans les images et aussi un MiniLM pour extraire les caractéristiques dans le texte et avoir des données tabulaires auxquelles on ajoute les informations sur le vehicule qui representent quelques colonnes. Ces caractéristiques étaient des données matricielles qui représentaient les images et textes d'origines. Le MiniLM fait aussi des extractions dans le texte selon sa compréhension contextuelles.
- Enfin, on passe les données obetenues dans un modèle de machine Learning.


- Pourquoi penser à cette approche ?
On le fait parce qu'on a à la fois des données structurées (informations sur le véhicule) et non structurées(Images). Alors comment tirer partie de toutes ces informations ?
Utiliser directement un modèle de Deep Learning sur les images reste possible, mais la contre partie est la perte d'information importante comme les valeurs neuves et vénales du véhicule, la marque du vehicule, le nombre de place... quand on sait qu'elle sont tres déterminante pour estimer le coût d'un sinistre. Naturellement les performances n'étaient pas bonnes et oxillaient autour des 30% en terme de accuracy.
Pour certaines raisons, on passe d'une regression à une classification, on vous épargnera de certains détails.
- Apres toutes ces transformations on obtient des données avec plusieurs colonnes, plus de 3000 exactement qui ne sont que des données numériques. Ce qui va constituer le 
fichier FINAL.csv sur lequel on fera tout ce qui est approche machine Learning.

### TRAIN.ipynb

Apres avoir obtenu, le fichier FINAL.csv avec toutes les donnees traitees, on se retrouve apres pres de 3000 colonnes. Alors on pense utiliser une technique de reduction de dimensionnalité qui est en l'occurence une ACP.
Ensuite, apres l'ACP, on a des colonnes reduites sur lesquelles on pourra implémenté tous nos modèles de machines learning afin de faire des prédictions. 
Les notebooks Train-Copy1.ipynb et Train-Copy2.ipynb sont en quelque sorte des brouillons de  TRAIN.ipynb.
Comme je l'ai signifié plus haut, nous avons effectué une classification à 4 groupes globalement. 

### TRAIN-TEXTE1
C'est exactement pareil que TRAIN.ipynb, mais juste qu'on décidé d'eliminer certaines colonnes descriptives de l'accident. Mais son impacte n'était pas vraiment significatif.

### TRAIN-2_CLASSES.ipynb et TRAIN-2_CLASSES.ipynb
Ici, c'est exactement tout le projet, sauf que nous sommes passé à deux classes, raisons qu'on expliquera pas ici,mais elle a donnée des performances plus meilleures.
