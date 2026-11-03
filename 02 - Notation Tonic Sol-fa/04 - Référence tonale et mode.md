# Référence tonale et mode majeur / mineur

## Principe

<badge color="success">Validé</badge> L'interprétation des degrés dépend du contexte tonal déclaré dans la partition.

La tonalité est désignée avec les lettres latines usuelles de la musique générale : `A B C D E F G`.

## Désignation de la tonalité

- Les altérations de la tonalité peuvent être indiquées avec `b` (bémol) ou `#` (dièse), comme dans la notation musicale générale.
- La préférence par défaut exprimée pour MireDo est l'emploi du bémol (`b`) lorsque le choix de l'altération est à faire.
- Exemple : `Ab) désigne la tonalité de La bémol.
- Dans une partition Sol-fa déclarée en `Ab`, le degré `d` (Do) correspond à `Ab` en hauteur absolue. Les autres degrés sont interprétés relativement à cette référence.

Le choix d'une tonalité est donc distinct de la syllabe Sol-fa écrite : la tonalité fournit le contexte permettant d'interpréter les degrés.

## Mode majeur / mineur

MireDo ne doit pas imposer une représentation unique du mode mineur. Le mode et le centre tonal doivent être considérés dans le contexte déclaré par la partition.

### Exemple : La mineur (Am)

Une partition peut utiliser Do majeur comme référence et considérer `l` comme centre tonal (tonique) dans le contexte de La mineur.

Dans cette représentation, les syllabes Sol-fa ne sont pas modifiées simplement parce que le morceau est mineur.

## Conséquence pour MireDo

Le moteur doit distinguer :
- la tonalité de référence déclarée (par exemple `Ab`) ;
- le mode ou contexte tonal de la pièce ;
- la syllabe Sol-fa écrite ;
- la hauteur absolue calculée.

Le mode mineur ne doit pas déclencher à lui seul une réécriture automatique des syllabes.

## Bécarre et altérations des notes

Selon la convention Sol-fa décrite, il n'existe pas de signe autonome de bécarre. Les syllabes et formes altérées sont employées directement.

**Point à clarifier ultérieurement :** la portée exacte de `b` et `#` dans MireDo : désignent-ils uniquement les altérations de la tonalité, ou doivent-ils également être utilisables dans l'écriture des notes Sol-fa ? Ne pas confondre cette question avec les règles d'altération syllabique déjà décrites.

## Questions ouvertes

- Quelle structure de métadonnées permettra d'exprimer la tonalité, le mode et le centre tonal ?
- Comment décrire une partition dont la référence change en cours de morceau ?
- Comment représenter les changements de contexte tonal sans perdre la graphie originale ?
