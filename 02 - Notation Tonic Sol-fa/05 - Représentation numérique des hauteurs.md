# Représentation numérique des hauteurs

<badge color="success">Principe validé</badge> La représentation numérique des notes repose sur un axe chromatique entier continu, dont l'ensemble des valeurs est **ℤ**.

Ce document formalise la décision de conception concernant :
- la coordonnée numérique des notes ;
- la référence numérique de portée propre à chaque voix ;
- la séparation entre saisie Sol-fa, interprétation numérique et rendu.

## 1. Axe numérique des notes

La note de référence est associée à la valeur **0**. Chaque demi-ton vers l'aigu ajoute **1** ; chaque demi-ton vers le grave soustrait **1**.

L'ensemble des valeurs possibles est :

**ℤ = { …, -3, -2, -1, 0, 1, 2, 3, … }**

Il n'existe donc aucune borne théorique inférieure ou supérieure : l'axe peut se prolonger vers **−∞** et vers **+∞**.

Les valeurs sont des entiers. La représentation n'utilise pas de fractions pour exprimer les demi-tons.

## 2. Correspondance avec les graphies Sol-fa

L'éditeur interprète les graphies Sol-fa saisies par le compositeur et les convertit en leur équivalent numérique. Le compositeur continue à écrire en notation Sol-fa ; il n'a pas à saisir les valeurs numériques.

Dans la convention de référence, la progression chromatique autour de la référence est notamment :

| Valeur | Graphie |
|---:|---|
| 0 | d |
| 1 | di |
| 2 | r |
| 3 | ri |
| 4 | m |
| 5 | f |
| 6 | fi |
| 7 | s |
| 8 | si |
| 9 | l |
| 10 | te |
| 11 | t |
| 12 | d' |

La progression continue dans les deux directions. Les graphies exactes restent régies par les règles Tonic Sol-fa définies dans [[01 - Hauteur et degrés]] et [[02 - Altérations chromatiques]].

**Important :** cette table illustre la correspondance chromatique de référence ; elle ne remplace pas les règles générales d'altération, d'octave, de référence tonale ou de conservation orthographique.

## 3. Altérations et calcul

Les règles Sol-fa existantes déterminent la conversion :
- i correspond à une élévation de **+1** demi-ton ;
- les formes descendantes utilisant a, e ou o correspondent à une diminution de **−1** demi-ton, selon le degré.

L'éditeur applique ces règles lors de l'interprétation de la saisie. Les autres composants du système utilisent ensuite l'équivalent numérique produit, au lieu de réinterpréter eux-mêmes les graphies.

## 4. Octaves

L'axe numérique étant continu, le passage d'une octave à la suivante ne crée pas une nouvelle classe de valeur : il poursuit le même axe par pas de douze demi-tons.

Ainsi, dans la correspondance chromatique de référence, d vaut 0, et le d de l'octave supérieure vaut 12. Les valeurs négatives permettent de représenter les positions situées sous la référence.

Les suffixes d'octave de la notation écrite (par exemple d1, d_1) restent régis par [[03 - Octaves et représentation]]. Ils servent à exprimer le déplacement d'octave dans la saisie Sol-fa ; l'éditeur en tient compte lors de la conversion numérique.

## 5. Référence de portée propre à chaque voix

Chaque voix possède une référence numérique de portée. Cette valeur détermine le placement de la référence 0 sur sa portée.

La convention de base déjà validée est :

| Référence de portée | Position de référence |
|---:|---|
| 0 | Clé de Sol |
| -1 | Clé de Fa |
| +1, +2, -2, etc. | Autres positions selon la même logique numérique |

Chaque voix définit sa propre référence. Pour la structure SATB par défaut :
- Soprano (S) : 0 ;
- Alto (A) : 0 ;
- Ténor (T) : -1 ;
- Basse (B) : -1.

Pour les autres structures vocales, le compositeur choisit la référence de chaque voix en utilisant les entiers selon cette convention. Le nom de la voix, sa référence de portée et sa tessiture restent trois informations distinctes.

**Ne pas confondre :**
- la coordonnée chromatique d'une note, qui appartient à ℤ ;
- la référence de portée d'une voix, qui est également un entier mais indique le placement de 0 sur cette portée ;
- la référence tonale de la partition, qui permet d'interpréter les degrés Sol-fa en hauteur absolue.

Ces valeurs sont toutes numériques, mais elles n'ont pas la même responsabilité.

## 6. Répartition des responsabilités

Le fonctionnement retenu est le suivant :

1. Le compositeur saisit les graphies Tonic Sol-fa dans l'éditeur.
2. L'éditeur reconnaît les graphies selon les règles Sol-fa déjà définies.
3. L'éditeur calcule et associe à chaque note son équivalent numérique entier.
4. Les autres composants (rendu, calculs et lecture) exploitent cette représentation numérique et les informations contextuelles nécessaires.
5. La graphie originale reste conservée pour l'affichage fidèle et la sérialisation.

Les composants autres que l'éditeur ne doivent pas réimplémenter chacun leur propre interprétation des lettres et des voyelles Sol-fa.

## 7. Préservation de la graphie

La coordonnée numérique représente la position chromatique ; elle ne remplace pas l'identité écrite de la note.

Deux graphies enharmoniques peuvent donc partager une même coordonnée numérique tout en restant distinctes dans la partition. Par exemple, mi et f peuvent correspondre à la même hauteur sonore sans que MireDo remplace l'une par l'autre.

Le modèle doit donc conserver séparément :
- la graphie originale saisie ;
- l'équivalent numérique calculé ;
- les références contextuelles nécessaires à l'interprétation et au placement.

Aucune normalisation enharmonique automatique n'est autorisée.

## 8. Portée de la décision

Cette décision fixe le principe de représentation numérique et la répartition des responsabilités. Elle ne fixe pas encore le schéma JSON final, les noms définitifs des propriétés, ni la stratégie complète de sérialisation du fichier .mrd.

Elle ne modifie pas les règles musicales déjà définies dans les documents consacrés aux degrés, aux altérations, aux octaves, à la référence tonale et aux voix/portées.
