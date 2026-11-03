# Rythme et durée — Tonic Sol-fa

Cette page consigne les règles rythmiques établies pour MireDo à partir de la notation Tonic Sol-fa décrite. Elle distingue les conventions déjà définies, les interprétations retenues pour la saisie et les limites de la notation Sol-fa.

## 1. Structure de la mesure et unités principales

### Délimitation des mesures : `|`

Le symbole `|` marque le début et la fin d'une mesure.

### Division de la mesure : `!`

Le symbole `!` sépare les deux moitiés égales d'une mesure lorsque cette division est possible. Il est structurel : il ne représente ni une note, ni une durée, ni un accent.

- En 4/4, il sépare deux groupes de deux temps.
- En 6/4, il sépare deux groupes de trois temps.
- En 5/4 et 7/4, il n'y a pas de séparation en deux moitiés égales : on utilise directement les séparateurs `:`, sans `!`.

### Séparation des unités : `:`

Le symbole `:` sépare les unités correspondant aux temps principaux. Leur nombre dépend de la signature temporelle.

Exemples :
- `|s:s:s|` en 3/4 : trois unités d'un temps.
- `|s:s!s:s|` en 4/4 : quatre unités d'un temps.
- `|s:s:s!s:s:s|` en 6/4 : six unités d'un temps.
- En 5/4 et 7/4, les unités sont séparées directement par `:`.

## 2. Subdivisions à l'intérieur d'une unité

Les symboles de subdivision s'appliquent à l'intérieur d'une unité délimitée par `:`.

### Division binaire : `.`

Le point divise une unité en deux parties égales. La subdivision peut être répétée pour obtenir des parts plus petites :

- `.` : division en deux, soit deux parts de 1/2 unité.
- `..` : division en quatre, soit quatre parts de 1/4 unité.

La durée d'une note qui n'est suivie d'aucun signe de prolongation est déterminée par la place qu'elle occupe dans la subdivision. Elle n'est pas automatiquement égale à une unité entière : ce n'est pas le séparateur `:` à lui seul qui fixe sa durée.

Exemple confirmé :
- `|d.:::|` : la note `d` occupe la première moitié de l'unité (une croche si l'unité vaut un temps de noire) ; les subdivisions restantes sont silencieuses. Le résultat est une croche suivie d'un silence de croche.

### Plusieurs notes dans une même unité

Lorsque plusieurs notes sont écrites directement dans une unité, sans séparateur entre elles, la durée de cette unité est répartie également entre ces notes.

Exemples de principe :
- `:dd:` : deux notes se partagent l'unité en deux parts égales.
- `:ddd:` : trois notes se partagent l'unité en trois parts égales.
- `:dddd:` : quatre notes se partagent l'unité en quatre parts égales.
- `:dddddd:` : six notes se partagent l'unité en six parts égales.

Cette règle de lecture compacte est retenue pour MireDo. Elle ne signifie pas que la notation Sol-fa traditionnelle définit une règle générale pour toute division possible.

### Triolets et sextolets

Les écritures avec séparateurs peuvent être utilisées, par exemple :
- Triolet : `:d.d.d:`.
- Sextolet : `:,,.,,:` (notation fournie comme exemple par l'utilisateur).

Ces écritures peuvent être visuellement lourdes. Pour le rendu de la partition, un groupe peut être présenté sans séparateurs entre les notes et identifié par une courbe au-dessus, comme dans la notation musicale usuelle. La forme de rendu n'est pas nécessairement la syntaxe de saisie ni la structure interne.

## 3. Prolongation : `-`

Le symbole `-` prolonge la note qui le précède. La note continue de sonner pendant la durée couverte par la prolongation.

- Une prolongation doit obligatoirement être précédée d'une note.
- La durée ajoutée dépend de l'unité ou de la subdivision occupée par le signe de prolongation.
- La prolongation peut traverser `!` et une ou plusieurs barres de mesure.
- Une nouvelle note met fin à la prolongation précédente et commence sa propre durée.
- Un signe `-` sans note précédente à prolonger est invalide.

Exemples déjà décrits pour les unités principales :
- `|d:-! :|` : Do est prolongé sur l'unité suivante.
- `|d:-!-:|` : Do est prolongé sur deux unités supplémentaires selon le découpage écrit.

Exemple de subdivision fourni :
- `|d:-!-.:|` : la durée de Do comprend deux unités, puis une demi-unité supplémentaire.

## 4. Silences implicites

Aucun symbole autonome de silence n'a été défini dans la convention décrite.

Une subdivision ou une partie d'unité qui ne contient ni note ni signe de prolongation est silencieuse. Il faut distinguer :
- une note : le son commence ;
- un signe `-` : le son de la note précédente continue ;
- une partie vide : silence.

Exemples :
- `|.d::|` : début de l'unité silencieux, puis note sur la seconde moitié ; l'utilisateur décrit cette figure comme un contretemps.
- `|d,.d:|` : exemple fourni pour une note, des subdivisions silencieuses, puis une autre note ; son découpage exact reste à confirmer.

## 5. Limites de la notation Sol-fa

La notation décrite fournit des conventions pour :
- les unités principales ;
- les divisions binaires en deux et en quatre ;
- certains groupes rythmiques usuels, notamment les triolets et les sextolets.

Elle ne définit pas de règle générale pour toutes les divisions possibles au-delà de ces conventions. MireDo ne doit donc pas inventer une convention Sol-fa traditionnelle inexistante ni présenter une extension propre à MireDo comme une règle universelle de la notation Sol-fa.

Pour les divisions non spécifiées, la syntaxe et le rendu restent à décider explicitement.

## 6. Questions ouvertes

Les points suivants ne sont pas encore suffisamment déterminés pour être considérés comme des règles validées :

- La syntaxe exacte des silences dans toutes les subdivisions, notamment la lecture complète de `|d,.d:|`.
- La lecture précise de certains exemples de prolongation ou de silence à l'intérieur d'un triolet, notamment `|d.-.d:|`, `:d-d:` et `:d..d:`.
- La convention de saisie et de rendu des divisions qui ne sont pas définies par la notation Sol-fa.

Les exemples encore ouverts ne doivent pas être utilisés pour déduire automatiquement une règle générale.
