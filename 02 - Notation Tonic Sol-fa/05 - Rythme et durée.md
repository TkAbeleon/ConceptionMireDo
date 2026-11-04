# Rythme et durée — Tonic Sol-fa

Cette page consigne les conventions de la notation Tonic Sol-fa discutées pour MireDo. Ces conventions appartiennent à la notation Sol-fa ; MireDo doit les prendre en charge et les représenter fidèlement, sans les présenter comme des règles inventées par la plateforme.

## 1. Structure de la mesure et unités principales

### Délimitation des mesures : `|`

Le symbole `|` marque le début et la fin d'une mesure.

### Division de la mesure : `!`

Le symbole `!` sépare les deux moitiés égales d'une mesure lorsque la structure de celle-ci le prévoit. Il appartient aux conventions de notation Tonic Sol-fa décrites ici : ce n'est ni une note, ni une durée, ni un accent, ni une convention inventée par MireDo.

Exemples :
- En 2/4, il n'y a pas de `!` : `|d:d|`.
- En 3/4, il n'y a pas de `!` : `|d:d:d|`.
- En 4/4, il sépare deux groupes de deux temps : `|d:d!d:d|`.
- En 5/4 et 7/4, il n'y a pas de séparation en deux moitiés égales : on utilise directement les séparateurs `:`, sans `!`.
- En 6/4, il sépare deux groupes de trois temps : `|d:d:d!d:d:d|`.

### Séparation des unités : `:`

Le symbole `:` sépare les unités correspondant aux temps principaux. Leur valeur dépend du dénominateur de la signature.

Exemples :
- `|d:d:d|` en 3/4 : trois unités d'un temps.
- `|d:d:d|` en 3/8 : même organisation que le 3/4, mais chaque unité vaut une croche.
- `|d:d!d:d|` en 4/4 : quatre unités d'un temps.
- `|d:d:d!d:d:d|` en 6/4 : six unités d'un temps.
- `|d:d:d!d:d:d|` en 6/8 : même organisation que le 6/4, mais chaque unité vaut une croche.
- En 5/4 et 7/4, les unités sont séparées directement par `:`, sans `!`.

## 2. Signature rythmique et disposition de la notation

La signature rythmique et la disposition utilisée pour écrire les unités dans la partition sont deux notions distinctes.

La signature indique la mesure choisie par le compositeur. Par exemple, 9/8 et 9/4 sont des signatures possibles. La disposition décrit la manière dont les unités et les groupes sont organisés dans l'écriture.

### Disposition habituelle par défaut

Par défaut, MireDo applique la disposition habituelle du Tonic Sol-fa correspondant à la signature choisie.

Exemple en 9/8 : la disposition habituelle est organisée en trois groupes de trois unités :
`|d:d:d!d:d:d!d:d:d|`.

### Disposition alternative choisie par le compositeur

Le compositeur peut choisir une autre disposition pour l'ensemble de sa partition. Par exemple, il peut choisir la signature 9/8 tout en utilisant une disposition d'écriture inspirée de celle qu'il emploie habituellement en 3/4.

Dans ce cas :
- la signature reste 9/8 ;
- la disposition de notation est celle choisie par le compositeur ;
- ce choix s'applique à toute la partition, sans exception ponctuelle mesure par mesure ;
- le choix de cette disposition ne transforme pas la signature 9/8 en 3/4.

La disposition alternative est donc un choix du compositeur, et non une règle générale du Tonic Sol-fa. Elle est sélectionnée au moment de la création de la partition. Si le compositeur ne fait pas de choix particulier, MireDo conserve la disposition habituelle par défaut.

MireDo ne doit pas confondre la signature de mesure avec la disposition choisie pour l'écriture.

## 3. Subdivisions à l'intérieur d'une unité

Les subdivisions décrites dans cette section se font à l'intérieur d'une unité délimitée par `:`. La division binaire, la répartition implicite et certains groupes non binaires sont documentés séparément.

### Division binaire : point `.` et virgule `,`

Dans la convention décrite ici, le point et la virgule expriment deux étapes successives d'une même logique de division binaire :

1. Le point `.` divise l'unité entière en deux moitiés égales. Chacune vaut `1/2` unité.
2. La virgule `,` divise en deux une moitié déjà obtenue par le point. Chacune des deux nouvelles parts vaut alors `1/4` de l'unité entière.

La virgule ne divise donc pas directement l'unité entière en quatre. Elle subdivise une moitié préalablement créée par le point. La division en quatre résulte de ces deux étapes successives.

Schéma de principe :

```text
Unité entière :       [          1          ]
Après le point :      [    1/2   ][    1/2   ]
Après la virgule :    [1/4][1/4][1/4][1/4]
```

Les signes doivent être lus dans leur position au sein de l'unité. Ils organisent les portions temporelles dans lesquelles les notes, les prolongations ou les silences prennent place ; ils ne sont pas eux-mêmes des événements sonores.

### Exemple détaillé

Exemple complet :

```text
| d,d .d ,d : d.,d ! d,-.d : d.d |
```

Pour expliquer la lecture, considérons les quatre unités de cette mesure en 4/4 séparément. Le séparateur `!` marque la séparation des groupes de la mesure ; il ne crée ni note ni durée supplémentaire.

**Unité 1 : `d,d .d ,d`**

Les quatre notes se partagent l'unité en quatre parts égales. Chaque note dure `1/4` d'unité.

```text
[d: 1/4] [d: 1/4] [d: 1/4] [d: 1/4]
```

**Unité 2 : `d.,d`**

La première note occupe la première moitié de l'unité, soit `1/2`. La portion suivante est un silence de `1/4`, puis la dernière note occupe le dernier `1/4`.

```text
[d: 1/2] [silence: 1/4] [d: 1/4]
```

**Unité 3 : `d,-.d`**

La première note commence sur une portion de `1/4`, puis le signe de prolongation `-` la maintient pendant `1/2` supplémentaire. Sa durée totale est donc `3/4` d'unité. La deuxième note occupe le dernier `1/4`.

```text
[d prolongé : 1/4 + 1/2 = 3/4] [d: 1/4]
```

**Unité 4 : `d.d`**

Le point divise l'unité en deux moitiés égales. Chaque note dure `1/2` unité.

```text
[d: 1/2] [d: 1/2]
```

Ces quatre lectures constituent un exemple de référence pour éviter de confondre les signes de division, les événements sonores et les durées obtenues.

### Silences dans une subdivision binaire

Une portion temporelle qui ne contient ni note ni prolongation est un silence. Il n'est pas nécessaire d'ajouter un symbole autonome de silence : sa position et sa durée sont déterminées par la structure de subdivision.

Exemples confirmés :

- `|d.,d|` : une note de `1/2`, un silence de `1/4`, puis une note de `1/4`.
- `|.d::|` : début de l'unité silencieux, puis note sur la seconde moitié ; l'utilisateur décrit cette figure comme un contretemps.
- `|d,.d:|` : quatre subdivisions égales : Do sur la première, silence sur la deuxième et la troisième, puis Do sur la quatrième.

### Répartition implicite sans signe de division

Lorsqu'une unité ne contient aucun signe de division explicite (`.` ou `,`), sa durée est répartie également entre les éléments qui la composent. Le comptage porte à la fois sur les notes et sur les signes de prolongation `-` :

- chaque note compte pour un élément ;
- chaque signe de prolongation compte également pour un élément ;
- tous les éléments comptés ont la même durée ;
- la somme des durées de ces éléments remplit exactement l'unité.

La durée d'un élément est donc égale à la durée de l'unité divisée par le nombre total de notes et de signes de prolongation présents dans cette unité.

Exemples, pour une unité de durée 1 :

| Écriture | Éléments comptés | Durée de chaque élément | Durée totale des notes |
|---|---:|---:|---|
| `:dd:` | 2 notes | `1/2` | chaque note : `1/2` |
| `:ddd:` | 3 notes | `1/3` | chaque note : `1/3` |
| `:dddd:` | 4 notes | `1/4` | chaque note : `1/4` |
| `:d-d:` | 2 notes + 1 prolongation | `1/3` | première note : `2/3` ; deuxième : `1/3` |
| `:dd-:` | 2 notes + 1 prolongation | `1/3` | première note : `1/3` ; deuxième : `2/3` |
| `:ddddd:` | 5 notes | `1/5` | chaque note : `1/5` |

Dans `:d-d:`, la première note occupe un élément-note puis l'élément-prolongation qui la suit ; elle dure donc `2/3` de l'unité. Dans `:dd-:`, c'est la deuxième note qui est prolongée et dure `2/3` de l'unité.

Cette répartition implicite est distincte de la division explicitement marquée par le point et la virgule. Elle ne doit pas être confondue non plus avec les divisions non binaires dont les conventions restent à préciser.

**Limite concernant les silences :** dans ce mode de répartition implicite, tous les éléments comptés se partagent l'unité et la remplissent. Il n'est donc pas possible d'y insérer une portion silencieuse sans introduire une convention supplémentaire qui n'est pas définie ici. Pour représenter un silence, il faut recourir à une écriture dont la structure de division explicite laisse une portion vide.

La distinction entre saisie compacte et saisie explicite, ainsi que les formes de visualisation proposées par l'éditeur, relève de l'interface. Ces choix ne doivent pas modifier la règle musicale ni créer une logique rythmique interne différente.

### Groupes non binaires : triolet et sextolet

Un groupe non binaire répartit une unité native Sol-fa complète en un nombre déterminé de positions égales. Le groupe ne change pas la durée de l'unité : il en organise seulement la répartition interne.

**Triolet**
- Le triolet comporte trois positions rythmiques égales.
- Les trois positions occupent ensemble exactement une unité native Sol-fa.
- Chaque position représente donc un tiers de cette unité.

**Sextolet**
- Le sextolet comporte six positions rythmiques égales.
- Les six positions occupent ensemble exactement une unité native Sol-fa.
- Chaque position représente donc un sixième de cette unité.
- La forme de notation communiquée pour le sextolet est `:,,.,,:`.

Dans ces groupes, une position occupée par `-` prolonge la note précédente au lieu de produire une nouvelle attaque. Elle compte néanmoins comme une position du groupe et conserve sa part de durée. Le nombre de positions du groupe reste donc trois pour un triolet et six pour un sextolet, même lorsque certaines positions sont des prolongations.

La courbe de groupement couvre le fragment complet du groupe, prolongations comprises, conformément à la règle de portée de la courbe de groupement.

Ces règles définissent la répartition temporelle du triolet et du sextolet dans l'unité Sol-fa. Elles ne doivent pas être interprétées à partir des valeurs de notes du solfège classique : l'unité de référence reste l'unité native Sol-fa.

### Portée de la courbe de groupement

Lorsqu'une courbe est tracée au-dessus d'un groupe rythmique, elle couvre l'intégralité du fragment de notation Sol-fa auquel ce groupement s'applique. Elle ne se limite pas aux seules attaques des notes : les signes de prolongation situés dans le fragment font partie de la portée de la courbe.

La courbe est une indication graphique de groupement. Les parenthèses utilisées dans les exemples explicatifs ci-dessous servent uniquement à montrer visuellement le fragment couvert ; elles ne sont pas des caractères de la notation Sol-fa et ne constituent pas une syntaxe de saisie.

Exemples de portée :

- Fragment explicatif `(d.-.d)` : la courbe couvre tout le fragment `d.-.d`, y compris la prolongation `-`.
- Fragment explicatif `(d.d.d)` : la courbe couvre les trois notes du fragment `d.d.d`.

Cette règle de portée s'applique de la même manière aux courbes des triolets, des sextolets et des autres groupes concernés. Elle décrit ce que la courbe englobe visuellement ; elle ne définit pas à elle seule la syntaxe ni le calcul temporel des divisions non binaires.

Les autres divisions non binaires, au-delà du triolet et du sextolet, restent à définir. Aucun comportement ne doit être déduit automatiquement de la seule présence de plusieurs notes ou de séparateurs. Les règles du triolet et du sextolet ne modifient pas la règle binaire exposée ci-dessus.
 
## 4. Prolongation : `-`

Le symbole `-` prolonge la note qui le précède. La note continue de sonner pendant la durée couverte par la prolongation.

- Une prolongation doit obligatoirement être précédée d'une note.
- Chaque signe de prolongation ajoute la durée de la subdivision dans laquelle il se trouve.
- La prolongation peut traverser `!` et une ou plusieurs barres de mesure.
- Une nouvelle note met fin à la prolongation précédente et commence sa propre durée.
- Un signe `-` sans note précédente à prolonger est invalide.

Exemple de subdivision fourni :
- `:s.-,f:` : Sol occupe une moitié d'unité, sa prolongation occupe un quart d'unité, puis Fa occupe le dernier quart.

Autre exemple fourni :
- `|d:-!-.:|` : Do occupe deux unités, puis une demi-unité supplémentaire.

## 5. Silences implicites

Aucun symbole autonome de silence n'a été défini dans la convention décrite.

Une portion explicitement délimitée qui ne contient ni note ni prolongation est silencieuse. En revanche, la répartition implicite décrite plus haut attribue toute l'unité aux notes et prolongations comptées : elle ne permet pas de représenter une portion silencieuse. Il faut distinguer :
- une note : le son commence ;
- un signe `-` : le son de la note précédente continue ;
- une partie vide : silence.

Exemples :
- `|.d::|` : début de l'unité silencieux, puis note sur la seconde moitié ; l'utilisateur décrit cette figure comme un contretemps.
- `|d,.d:|` : quatre subdivisions égales : Do sur la première, silence sur la deuxième et la troisième, puis Do sur la quatrième.

## 6. Nuances, point d'orgue et autres indications musicales

Les nuances (par exemple piano, forte et leurs variations), le point d'orgue ainsi que les autres indications musicales suivent les conventions du solfège/notation musicale. Il ne s'agit pas de règles propres à MireDo.

MireDo doit permettre de représenter ces indications conformément aux conventions musicales, sans leur attribuer une signification ou une syntaxe spécifique inventée par la plateforme.

Les symboles précis, leur syntaxe de saisie et leurs possibilités de personnalisation restent à détailler dans la documentation dédiée aux indications musicales.

## 7. Limites de la notation Sol-fa

La notation décrite fournit des conventions pour :
- les unités principales ;
- les divisions binaires en deux et en quatre ;
- certains groupes rythmiques usuels, notamment les triolets et les sextolets ;
- les regroupements habituels associés aux signatures évoquées dans cette page.

Elle ne définit pas de règle générale pour toutes les divisions possibles. MireDo ne doit donc pas inventer une convention Sol-fa traditionnelle inexistante ni présenter une extension propre à MireDo comme une règle universelle de la notation Sol-fa.

Pour les divisions non spécifiées, la syntaxe et le rendu restent à décider explicitement.

## 8. Points restant à préciser

Les points suivants ne sont pas encore suffisamment déterminés pour être considérés comme des règles validées :

- La syntaxe exacte des silences dans toutes les subdivisions.
- La lecture détaillée des exemples combinant groupes non binaires, prolongations et silences, notamment `|d.-.d:|` et `:d..d:`, afin de préciser les cas qui ne sont pas couverts par la règle générale des positions égales.
- La convention de saisie et de rendu des divisions qui ne sont pas définies par la notation Sol-fa.
- Les symboles précis et la syntaxe de saisie des nuances, du point d'orgue et des autres indications musicales.
- Les autres signatures et regroupements qui n'ont pas encore été explicitement validés.

Les exemples encore ouverts ne doivent pas être utilisés pour déduire automatiquement une règle générale.


## 9. Doubles barres et changements de tonalité

### Comportement général de la double barre

Par défaut, la double barre conserve son comportement habituel en notation musicale : elle peut notamment marquer la fin d'une phrase musicale ou accompagner un changement de clef ou de mesure.

La double barre n'est pas automatiquement obligatoire à ces endroits. Son utilisation dépend de la partition et des conventions appliquées.

### Particularité de certaines partitions Tonic Sol-fa de FFPM

Dans certaines notations Tonic Sol-fa utilisées par FFPM, la double barre peut également servir à indiquer une prolongation de mesure. Cet usage particulier doit être pris en charge par MireDo comme une fonctionnalité optionnelle, mais ne doit pas être activé comme comportement par défaut.

### Double barre facultative lors d'un changement de tonalité ou d'une fin de phrase

Lors d'un changement de tonalité, le compositeur peut écrire le changement sans double barre ou choisir d'en placer une.

Exemples de formes communiquées :
- Sans double barre : `|:!:changement de tonalité|`.
- Avec double barre : `|:!||changement de tonalité|`.

Une phrase musicale peut également se terminer au milieu d'une mesure. Là encore, la double barre peut être omise ou ajoutée pour rendre la séparation plus visible.

La double barre reste donc une indication facultative dans ces cas : MireDo ne doit pas l'insérer automatiquement à chaque changement de tonalité ni à chaque fin de phrase.

### Indication de transition entre deux tonalités

Lorsqu'une partition passe d'une tonalité à une autre, une indication entre parenthèses peut être placée avant la note écrite dans la nouvelle tonalité.

Exemple communiqué : tonalité initiale C, puis changement vers D :

`|d:d!(l_1)s_1:s_1|`

Dans cet exemple :
- `(l_1)` est une indication facultative de transition ;
- elle représente, dans la tonalité précédente, l'équivalent de la note suivante, laquelle est déjà écrite dans la nouvelle tonalité ;
- elle sert à faciliter la lecture et l'anticipation du changement de tonalité ;
- elle ne remplace pas la note suivante et ne constitue pas une note supplémentaire à jouer ;
- `s_1` est la note écrite après le changement, selon la nouvelle tonalité.

Cette indication entre parenthèses peut être affichée ou omise selon le choix du compositeur. MireDo doit préserver cette distinction et ne pas la traiter comme une note ordinaire.

La syntaxe complète des changements de tonalité et le comportement exact de la double barre dans le cas particulier de la prolongation de mesure restent à préciser.
