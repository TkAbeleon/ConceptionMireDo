# Rythme et durée — Tonic Sol-fa

Cette page formalise les règles rythmiques décrites pour MireDo. Le périmètre actuel porte sur les unités de temps entières ; les subdivisions inférieures au temps et les divisions irrégulières restent à définir.

## Délimitation des mesures : `|`

Le symbole `|` marque le début et la fin d'une mesure. Une mesure complète occupée par une seule note correspond à une ronde lorsque la mesure compte quatre temps (4/4).

## Division de la mesure : `!`

Le symbole `!` sépare les deux moitiés égales d'une mesure lorsque cette division est possible. Il est uniquement structurel : il ne représente ni une note, ni une durée, ni un accent.

Exemples :
- En 4/4, `!` sépare deux groupes de deux temps.
- En 6/4, `!` sépare deux groupes de trois temps.
- Pour des mesures comme 5/4 ou 7/4, qui ne se divisent pas en deux moitiés égales, on utilise directement les séparateurs `:` sans ajouter `!`.

## Séparation des temps : `:`

Le symbole `:` sépare les unités correspondant aux temps. Leur nombre dépend de la signature temporelle.

Exemples :
- `|s:s:s|` en 3/4 : trois noires.
- `|s:s!s:s|` en 4/4 : quatre noires.
- `|s:s:s!s:s:s|` en 6/4 : six noires.
- En 5/4 et 7/4, les cinq ou sept unités sont séparées directement par `:`.

## Prolongation : `-`

Le symbole `-` prolonge obligatoirement une note qui le précède. Chaque tiret ajoute une unité de temps à la durée de cette note. La prolongation peut continuer sur autant d'unités que nécessaire, traverser `!` et se poursuivre sur les mesures suivantes. Une nouvelle note met fin à la prolongation précédente et commence sa propre durée. Un tiret sans note précédente à prolonger est invalide.

Exemples en 4/4 :
- `|d:! :|` : Do noire, un temps.
- `|d:-! :|` : Do blanche, deux temps.
- `|d:-!-:|` : Do blanche pointée, trois temps.
- `|d:-!-:-|` : Do ronde, quatre temps.

Une prolongation peut traverser une barre de mesure : les tirets continuent alors la note initiale dans la mesure suivante.

## Silences implicites

La convention décrite ne possède pas de symbole spécifique pour les silences. Une unité sans note et sans tiret correspond à un silence. Une note commence un son ; un tiret prolonge la note précédente ; une unité vide est silencieuse.

Exemples en 4/4 :
- `|r:-!-:|` : Ré pendant trois temps, puis un silence d'un temps.
- `|d:-!r:|` : Do pendant deux temps, Ré pendant un temps, puis un silence d'un temps. La nouvelle note Ré met fin à la prolongation de Do.

## Périmètre non encore défini

Les demi-temps, subdivisions inférieures au temps, triolets et autres divisions irrégulières ne sont pas traités ici. Ils feront l'objet d'une définition ultérieure.
