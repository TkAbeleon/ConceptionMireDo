# Questions ouvertes

Cette page centralise les questions qui nécessitent une décision explicite. Une question ne doit pas être considérée comme résolue par une simple proposition dans une discussion.

## Notation des altérations

- [ ] Définir les formes descendantes usuelles pour chacun des sept degrés.
- [ ] Décider si les variantes `te`, `ta`, `to` sont toutes acceptées par le parseur.
- [ ] Décider si la variante saisie doit être conservée à l'identique dans les exports.

## Octaves

- [ ] Fixer la plage numérique autorisée pour les déplacements d'octave.
- [ ] Déterminer si `d0` est accepté ou omis.
- [ ] Définir les règles lexicales pour éviter les ambiguïtés de parsing.
- [ ] Choisir les rendus typographiques disponibles (exposants/indices, apostrophes/virgules).
- [ ] Déterminer comment le contexte musical associe l'octave de référence implicite à une hauteur absolue.

## Référence tonale

- [ ] Définir la structure permettant d'exprimer la référence et le centre tonal.
- [ ] Définir le traitement d'un changement de référence ou de tonalité au cours d'une partition.
- [ ] Déterminer comment conserver la graphie initiale lors d'une transposition.

## Modèle interne

- [ ] Définir une représentation séparant la syllabe écrite, le degré, l'altération, le déplacement d'octave et la hauteur calculée.
- [ ] Décider quelles informations sont nécessaires pour reconstituer exactement la graphie originale.
