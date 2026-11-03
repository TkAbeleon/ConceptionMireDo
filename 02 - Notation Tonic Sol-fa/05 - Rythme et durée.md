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

Les symboles de subdivision s'appliquent à l'intérieur d'une unité délimitée par `:`.

### Division binaire : `.`

Le point divise une unité en deux parties égales. La subdivision peut être répétée pour obtenir des parts plus petites :

- `.` : division en deux, soit deux parts de 1/2 unité.
- `..` : division en quatre, soit quatre parts de 1/4 unité.

Une subdivision peut être vide : elle représente alors un silence. Il est donc possible de commencer une mesure par un silence, sans devoir commencer obligatoirement par une note.

Exemples fournis :
- `.d:d.d|d:d:d|`
- `.d|d:d`

Dans ces exemples, le début `.d` montre une première subdivision silencieuse, suivie de la note `d`. Ces exemples sont conservés tels quels comme formes de notation communiquées par l'utilisateur.

La durée d'une note qui n'est suivie d'aucun signe de prolongation est déterminée par la place qu'elle occupe dans la subdivision. Elle n'est pas automatiquement égale à une unité entière : ce n'est pas le séparateur `:` à lui seul qui fixe sa durée.

Autre exemple confirmé :
- `|d.:::|` : la note `d` occupe la première moitié de l'unité (une croche si l'unité vaut un temps de noire) ; la seconde moitié et les unités restantes sont silencieuses.

### Plusieurs notes dans une même unité

Lorsque plusieurs notes sont écrites directement dans une unité, sans séparateur entre elles, la durée de cette unité est répartie également entre ces notes.

Exemples de principe :
- `:dd:` : deux notes se partagent l'unité en deux parts égales.
- `:ddd:` : trois notes se partagent l'unité en trois parts égales.
- `:dddd:` : quatre notes se partagent l'unité en quatre parts égales.
- `:dddddd:` : six notes se partagent l'unité en six parts égales.

Cette règle de lecture compacte est retenue pour la saisie décrite. Elle ne signifie pas que la notation Sol-fa traditionnelle définit une règle générale pour toute division possible.

### Triolets et sextolets

Les écritures avec séparateurs peuvent être utilisées, par exemple :
- Triolet : `:d.d.d:`.
- Sextolet : `:,,.,,:` (notation fournie comme exemple par l'utilisateur).

Ces écritures peuvent être visuellement lourdes. Pour le rendu de la partition, un groupe peut être présenté sans séparateurs entre les notes et identifié par une courbe au-dessus, comme dans la notation musicale usuelle. La forme de rendu n'est pas nécessairement la syntaxe de saisie ni la structure interne.

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

Une subdivision ou une partie d'unité qui ne contient ni note ni signe de prolongation est silencieuse. Il faut distinguer :
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
- La lecture précise de certains exemples de prolongation ou de silence à l'intérieur d'un triolet, notamment `|d.-.d:|`, `:d-d:` et `:d..d:`.
- La convention de saisie et de rendu des divisions qui ne sont pas définies par la notation Sol-fa.
- Les symboles précis et la syntaxe de saisie des nuances, du point d'orgue et des autres indications musicales.
- Les autres signatures et regroupements qui n'ont pas encore été explicitement validés.

Les exemples encore ouverts ne doivent pas être utilisés pour déduire automatiquement une règle générale.
