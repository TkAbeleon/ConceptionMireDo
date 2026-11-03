# Questions ouvertes

Cette page centralise les questions qui nécessitent une décision explicite. Une question ne doit pas être considérée comme résolue par une simple proposition dans une discussion.

## Notation des altérations

- [ ] Définir les formes descendantes usuelles pour chacun des sept degrés.
- [ ] Décider si les variantes `te`, `ta`, `to` sont toutes acceptées par le parseur.
- [ ] Décider si la variante saisie doit être conservée à l'identique dans les exports.

## Octaves

- [ ] Expliquer et fixer la référence exacte à partir de laquelle on compte les déplacements d'octave. Les exemples `d1` (une octave plus haut), `d2` (deux octaves plus haut) et `d_1` (une octave plus bas) sont compris, mais la référence n'est pas encore définie.
- [ ] Fixer la plage numérique autorisée.
- [ ] Déterminer si `d0` est accepté ou si l'absence de suffixe a une autre signification.
- [ ] Définir les règles lexicales pour éviter les ambiguïtés de parsing.
- [ ] Choisir les rendus typographiques disponibles (exposants/indices, apostrophes/virgules).

## Référence tonale

- [ ] Définir la structure permettant d'exprimer la référence et le centre tonal.
- [ ] Définir le traitement d'un changement de référence ou de tonalité au cours d'une partition.
- [ ] Déterminer comment conserver la graphie initiale lors d'une transposition.

## Modèle interne

- [ ] Définir une représentation séparant la syllabe écrite, le degré, l'altération, le déplacement d'octave et la hauteur calculée.
- [ ] Décider quelles informations sont nécessaires pour reconstituer exactement la graphie originale.
