### PROJET DE PREDICTION DE COUT DE SINISTRE EN SERVANT DES IMAGES ET DES INFORMATIONS SUR LE VEHICULE ACCIDENTE.

Il s'agit de connaitre le cout de sinistre à allouer à un client en dommage matériel subit par son véhicule.
C'est un projet qui allie à la fois Deep Learning avec les reseaux de neuronnes convolutionnels, Machine Learning, LLM et plus.
Nous avons utlisés plusieurs approches, mais celle alliant ces differentes solutions était la meilleurs.

L'idéal était d'execute le projet dans un environnement virtuel, mais nos contraintes machines et les faites de se deplacer à chaques 
que differentes environnements et differents serveurs avec chacunes ces exigeances nous conduisait à toujours manipuler differents notebook.

Nous avons amene été à travailler avec des CPU et aussi sur des plateformes comme vastai qui proposaient des GPU propices à notre travail.
Pour aller à bout de ce projet, nous avons mis en place plusieurs notebook que nous tenterons d'expliquer et de donner l'utilité en quelques lignes.

### Processus_projet_Tout.ipynb

Ce notebook a permis de faire tous les travaux de traitements de données. C'est d'ici que provient le fichier global.csv qui contient les donnees propres. 
Certes le code continue pour certaines manipulations et certains textes, mais c'est un toute son importance une fois qu'on obtient tous ce fichier.
Dans chaque enregistrement, on des lignes qui contiennent les adresses des images de la voiture accidentée, les informations sur le véhicule et le cout de sinistre.
On aurait pu effectuer tout le traitement ici, mais la tache suivante etait d'associer à chaque adresse l'image qui lui correspondait. Et en le faisant, arriver à un certzin nombre de lignes, le noyau redemarrait pour un probleme de performances machines. Alors, fallait scincder le fichier en plusieurs morceaux(des blocs de 100 lignes) et effecter
l'operation. Le Noyau ne s'interropait plus, mais pour 100 lignes, le traitement beaucoup trop chronophrage. Alors, nous étions dans l'obligation de penser à une solution palliative, l'utilisation des GPU.
