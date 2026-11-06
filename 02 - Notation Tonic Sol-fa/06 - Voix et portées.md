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
- Le crochet est affiché par défaut. L'utilisateur peut toutefois choisir de le masquer.

Cette présentation s'applique à l'ensemble des voix de la partition.

### Crochet, barre initiale et continuité entre les systèmes

Le crochet et les barres verticales de début et de fin de système sont des éléments distincts.

Lorsque le crochet est masqué :

- Si le système commence normalement sur le premier temps de la mesure, une barre verticale initiale remplace le crochet.
- Si le système commence par une anacrouse, c'est-à-dire sans attaque sur le premier temps, aucune barre verticale initiale supplémentaire n'est ajoutée. Le séparateur musical réellement nécessaire au début du système est conservé.
- Si le système reprend au milieu d'une mesure, aucune barre initiale supplémentaire n'est ajoutée. Le séparateur qui précédait la première unité reprise (`:`, `!` ou `||`, selon l'écriture) reste visible.
- Chaque ligne de système se termine toujours par une barre verticale de fermeture, même lorsque le retour à la ligne intervient au milieu d'une mesure.

La barre de fermeture d'une ligne ne remplace pas le séparateur musical du début de la ligne suivante. Si le séparateur suivant est `||`, la ligne précédente se ferme par une barre simple et la double barre reste au début de la ligne suivante. La mise en page ne doit ni supprimer ce séparateur, ni le remplacer automatiquement par une barre initiale.

Exemple schématique lorsque le crochet est masqué :

```text
|d:d:d.|
.r|d:d:d|
```

Le début `.r` reste écrit comme tel ; aucune barre initiale supplémentaire ne le précède.

## 5. Principes à respecter

- Le nom d'une voix est libre et indépendant de sa référence de portée.
- La structure SATB est proposée par défaut, mais reste personnalisable.
- Chaque voix possède sa propre référence de portée.
- En mode Sol-fa, la sélection numérique est la représentation destinée à l'utilisateur.
- En mode avancé, les clés peuvent être présentées avec leur notation classique.
- MireDo doit conserver une séparation entre le nom de la voix, sa référence de portée et sa hauteur de registre. Ces propriétés ne doivent pas être confondues.
- Pour une partition à plusieurs voix, les barres de mesure traversent toutes les portées et le crochet de système est visible par défaut, avec une option pour le masquer ; les règles de barre initiale, de séparateur conservé et de fermeture de ligne restent applicables lorsque le crochet est masqué.

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

## 7. Paroles et couplets

Les paroles peuvent être communes à l'ensemble vocal ou propres à une ou plusieurs voix.

### 7.1 Paroles communes et paroles propres aux voix

- **Paroles communes** : un même texte est partagé par les voix concernées. Il n'est pas nécessaire de le dupliquer sous chaque portée.
- **Paroles propres aux voix** : chaque voix concernée possède son propre texte, qui peut être différent de celui des autres voix.
- Lorsque toutes les voix ont des paroles distinctes, il n'y a pas de texte général commun à l'ensemble vocal.
- Une même partition peut combiner des paroles communes pour certaines voix et des paroles spécifiques pour d'autres, lorsque le passage le demande.

### 7.2 Organisation des couplets

Une œuvre peut comporter plusieurs couplets associés à une même musique. Les couplets sont identifiés séparément (couplet 1, couplet 2, couplet 3, etc.).

La musique n'a pas à être dupliquée pour enregistrer les différents textes. Les paroles de chaque couplet restent associées à la structure musicale correspondante.

### 7.3 Modes de présentation des couplets

MireDo propose trois modes de présentation :

1. **Tous les couplets sous les notes** : chaque couplet est affiché directement sous les notes auxquelles ses syllabes correspondent. Chaque ligne de paroles est identifiée par le numéro du couplet.
2. **Premier couplet sous les notes, tous les couplets sous la partition** : le premier couplet est affiché sous les notes ; l'ensemble des textes est également présenté en dessous de la partition, hors des portées. Le premier couplet peut donc apparaître dans les deux emplacements.
3. **Mode mixte** : tous les couplets sont affichés sous les notes et tous les couplets sont également présentés en dessous de la partition.

Le choix du mode concerne la présentation des paroles ; il ne modifie pas la musique ni l'identité des couplets.

### 7.4 Indépendance des deux présentations

Les paroles affichées sous les notes et celles présentées en dessous de la partition sont deux représentations éditoriales indépendantes.

En particulier, lorsque le premier couplet apparaît aux deux endroits, les deux textes sont édités séparément. MireDo ne doit pas supposer qu'il peut reconstruire automatiquement le texte continu à partir des paroles découpées en syllabes et alignées sous les notes. Si l'utilisateur souhaite les deux présentations, il renseigne chacune d'elles.

### 7.5 Niveau d'organisation des paroles et mélismes

Les paroles restent organisées au niveau des unités musicales. Il n'est pas nécessaire de créer une structure de paroles détaillée sous chaque note.

En revanche, une indication de mélisme peut être portée directement par les notes concernées : elle permet de montrer immédiatement au lecteur que plusieurs notes successives correspondent à une même syllabe. Cette indication est propre à la voix concernée et ne modifie ni la hauteur ni la durée des notes.

### 7.6 Paroles lors des reprises et répétitions

Une reprise musicale ne signifie pas nécessairement que les paroles doivent être répétées à l'identique.

Une même section musicale peut être chantée plusieurs fois avec des paroles différentes selon l'occurrence de la reprise. MireDo doit donc permettre d'associer un texte différent à une occurrence donnée de la section, sans obliger à dupliquer les notes ou la structure musicale.

Cette possibilité s'applique aussi bien aux paroles communes qu'aux paroles propres à une voix, selon les voix concernées.

## 8. Principes à respecter pour les paroles

- Les paroles peuvent être communes ou propres à chaque voix.
- Une œuvre peut contenir plusieurs couplets associés à une même musique.
- Les trois modes de présentation des couplets sont pris en charge : tous sous les notes ; premier sous les notes et tous sous la partition ; tous aux deux emplacements.
- Les paroles sous les notes et les textes sous la partition sont édités indépendamment.
- Les paroles restent organisées au niveau des unités musicales ; les indications de mélisme peuvent être portées au niveau des notes.
- Une occurrence de reprise peut avoir des paroles différentes d'une autre occurrence de la même musique.
- Les choix de paroles et de présentation ne doivent pas obliger à dupliquer la structure musicale.
