# Voix et portées — MireDo

## 1. Structure des voix

MireDo propose par défaut une structure chorale SATB :

- S : Soprano ;
- A : Alto ;
- T : Ténor ;
- B : Basse.

Cette structure est une valeur par défaut, pas une obligation. Le compositeur peut choisir une autre structure, ajouter des voix et leur donner librement un nom : lettre, nom de registre ou appellation personnalisée (par exemple `S`, `Voix 1`, etc.).

Le nombre de voix n'est donc pas limité à quatre.

## 2. Référence de portée en mode Tonic Sol-fa

En mode Tonic Sol-fa, l'utilisateur peut choisir une référence numérique plutôt que devoir connaître les noms des clés de la notation classique.

La correspondance de base est :

- `0` : clé de Sol ;
- `-1` : clé de Fa ;
- les autres valeurs entières (`+1`, `+2`, `-2`, etc.) représentent les autres positions de référence selon la même logique numérique.

Chaque voix possède sa propre référence de portée. L'utilisateur Sol-fa peut ainsi configurer ses voix sans avoir à maîtriser la terminologie des clés du solfège classique.

## 3. Notation classique pour les utilisateurs avancés

Les utilisateurs qui connaissent la notation classique peuvent choisir directement les clés avec leur dénomination musicale (Sol, Fa, Ut/Do et leurs positions).

Cette représentation classique est une possibilité avancée ; elle ne doit pas être imposée aux utilisateurs qui travaillent uniquement en Tonic Sol-fa.

## 4. Présentation d'une partition à plusieurs voix

Lorsque la partition comporte plusieurs voix :

- Les portées sont disposées les unes sous les autres.
- Les barres de mesure sont alignées et se prolongent verticalement à travers l'ensemble des portées, comme dans une partition classique.
- Un crochet relie les portées au début de chaque ligne de système, comme en solfège classique.
- Ce crochet est affiché par défaut. L'utilisateur peut toutefois choisir de le masquer.

Cette présentation s'applique à l'ensemble des voix de la partition.

## 5. Principes à respecter

- Le nom d'une voix est libre et indépendant de sa référence de portée.
- La structure SATB est proposée par défaut, mais reste personnalisable.
- Chaque voix possède sa propre référence de portée.
- En mode Sol-fa, la sélection numérique est la représentation destinée à l'utilisateur.
- En mode avancé, les clés peuvent être présentées avec leur notation classique.
- MireDo doit conserver une séparation entre le nom de la voix, sa référence de portée et sa hauteur de registre. Ces propriétés ne doivent pas être confondues.
- Pour une partition à plusieurs voix, les barres de mesure traversent toutes les portées et le crochet de système est visible par défaut, avec une option pour le masquer.

## 6. Mise en page : systèmes, retours à la ligne et pages

La mise en page suit les conventions habituelles des logiciels de notation musicale, avec les comportements par défaut suivants :

### Retours à la ligne

- Par défaut, une mesure entière qui ne tient pas dans la ligne est reportée au système suivant. MireDo ne coupe donc pas automatiquement une mesure pour la faire tenir dans l'espace restant.
- Le compositeur peut toutefois imposer manuellement un retour à la ligne à un emplacement précis, y compris au milieu d'une mesure.
- Les portées d'un même système restent alignées et les mesures des différentes voix restent synchronisées.

### Sauts de page

MireDo prend également en charge les sauts de page :
- saut automatique lorsque la mise en page nécessite une nouvelle page ;
- possibilité d'insérer un saut de page manuel pour contrôler la présentation de la partition.

Ces règles concernent la mise en page du document et ne modifient ni la structure musicale ni la durée des mesures. La syntaxe des commandes de mise en page sera précisée dans la conception technique.

## 7. Placement des paroles dans une partition à plusieurs voix

Les paroles sont écrites une seule fois pour l'ensemble vocal, et non répétées sous chaque portée.

Deux présentations sont proposées :

### Présentation par défaut : paroles sous toutes les portées

Toutes les portées de la partition sont regroupées au-dessus de la ligne de paroles. Les paroles sont placées une seule fois sous l'ensemble des portées, quelle que soit la structure vocale choisie (SATB ou autre).

### Présentation alternative : paroles entre deux groupes de portées

Les paroles peuvent être placées entre deux groupes de portées. Dans une partition SATB, les portées S et A forment le groupe supérieur ; les portées T et B forment le groupe inférieur. Les paroles sont écrites une seule fois entre ces deux groupes.

Cette deuxième présentation reprend la disposition des barres utilisée en solfège classique :
- au début du système, la barre verticale initiale est longue et relie les portées ;
- au niveau de la ligne de paroles, la barre de mesure ne traverse pas l'espace réservé aux paroles entre les deux groupes de portées. Les portées du groupe supérieur et celles du groupe inférieur restent chacune délimitées selon cette disposition.

Cette présentation alternative n'est pas limitée à SATB : les groupes de portées peuvent être adaptés à la structure vocale de la partition.

Dans les deux présentations, les paroles restent uniques et sont alignées avec les notes auxquelles elles correspondent.

### Paroles indépendantes pour une voix

Dans certains passages chorals, une voix peut avoir un texte différent ou avancer indépendamment des autres voix (comme cela peut se présenter dans le *Hallelujah* de Haendel). Dans ce cas, les paroles propres à cette voix sont placées directement sous sa portée.

Cette disposition peut être utilisée ponctuellement pour une ou plusieurs voix concernées, tandis que les autres voix conservent leur disposition de paroles commune. Elle ne constitue pas le mode général par défaut : elle répond aux besoins du passage musical.
