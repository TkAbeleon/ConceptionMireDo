# Référence tonale et choix du compositeur

## Principe

<badge color="success">Validé</badge> Chaque partition déclare une tonalité de référence. MireDo interprète les notes Sol-fa par rapport à cette référence, sans imposer au compositeur la tonalité réelle, la gamme ou le centre tonal de son morceau.

La tonalité de référence est désignée avec les lettres latines usuelles : `A B C D E F G`.

## Désignation de la référence

- Les altérations de la tonalité de référence peuvent être indiquées avec `b` (bémol) ou `#` (dièse), comme dans la notation musicale générale.
- La préférence par défaut exprimée pour MireDo est l'emploi du bémol (`b`) lorsqu'un choix d'orthographe est nécessaire.
- Exemple : `Ab` désigne la référence La bémol.
- Dans une partition dont la référence est `Ab`, le degré Sol-fa `d` correspond à la hauteur La bémol.

## Liberté du compositeur

La tonalité de référence ne détermine pas à elle seule la gamme ni le mode du morceau. Le compositeur reste libre d'organiser sa musique et de choisir les syllabes Sol-fa qui représentent les notes qu'il souhaite écrire.

### Exemple : morceau en La mineur avec Do comme référence

Le compositeur peut déclarer `C` comme référence, donc `d = C`, tout en écrivant un morceau en La mineur et en utilisant `l` comme tonique.

MireDo respecte cette écriture. Il ne déduit pas que le morceau est en Do majeur simplement parce que la référence est `C`. Aucun champ obligatoire `Major` ou `Minor` n'est imposé par cette règle.

### Exemple : morceau réellement en Ré bémol, écrit avec Do comme référence

Le compositeur peut choisir la référence habituelle `Db` et écrire, par exemple, `d d d m`.

Il peut aussi décider de déclarer `C` comme référence et d'adapter lui-même son écriture, par exemple `di di di f`.

MireDo accepte cette seconde écriture sans question ni correction automatique. Le choix de la référence et l'adaptation de la notation appartiennent au compositeur.

## Conséquences pour MireDo

- Interpréter les degrés Sol-fa selon la tonalité de référence déclarée.
- Respecter exactement les notes et les altérations écrites par le compositeur.
- Ne pas déduire ni imposer automatiquement une gamme majeure ou mineure.
- Ne pas corriger une écriture parce qu'elle semble inhabituelle ou parce que la référence choisie diffère de la tonalité réelle du morceau.
- Ne pas normaliser automatiquement les graphies enharmoniques.
- Laisser au compositeur la responsabilité de la cohérence musicale de son écriture.

MireDo est un outil de notation et d'interprétation fidèle, pas un correcteur des décisions musicales du compositeur.

## Bécarre et altérations des notes

Selon la convention Sol-fa décrite, il n'existe pas de signe autonome de bécarre. Les syllabes et formes altérées sont employées directement.

**Point à clarifier séparément :** la portée exacte de `b` et `#` dans MireDo : désignent-ils uniquement les altérations de la tonalité de référence, ou doivent-ils également être utilisables dans l'écriture des notes Sol-fa ? Ne pas confondre cette question avec les règles d'altération syllabique.
