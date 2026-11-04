# Questions ouvertes

Cette page centralise les questions qui nécessitent une décision explicite. Elles ne sont pas toutes prioritaires : les points secondaires peuvent rester ouverts jusqu'à ce qu'un besoin concret apparaisse pendant la conception, l'implémentation ou les tests.

## Notation des altérations

- [ ] Définir les formes descendantes usuelles pour chacun des sept degrés.
- [ ] Décider si les variantes `te`, `ta`, `to` sont toutes acceptées par le parseur.
- [ ] Décider si la variante saisie doit être conservée à l'identique dans les exports.

## Octaves

- [ ] Fixer la plage numérique autorisée pour les déplacements d'octave.
- [ ] Définir les règles lexicales pour éviter les ambiguïtés de parsing.
- [ ] Choisir les rendus typographiques disponibles (exposants/indices, apostrophes/virgules).
- [ ] Déterminer comment le contexte musical associe l'octave de référence implicite à une hauteur absolue.
- [ ] Décider du traitement de suffixes particuliers comme `0` uniquement si un besoin concret se présente.

## Référence tonale

- [ ] Définir la structure permettant d'exprimer la référence et le centre tonal.
- [ ] Définir le traitement d'un changement de référence ou de tonalité au cours d'une partition.
- [ ] Déterminer comment conserver la graphie initiale lors d'une transposition.

## Modèle interne

- [ ] Définir les propriétés et types exacts du modèle d'exécution qui porteront la graphie originale, la coordonnée chromatique entière et les contextes nécessaires.
- [ ] Définir la conversion technique entre référence tonale, graphie Sol-fa, octave et coordonnée numérique, en conformité avec les règles déjà validées.

## Format natif `.mrd`

Les questions spécifiques au format de fichier sont suivies dans [[04 - Architecture/Format de fichier MireDo/04 - Questions ouvertes]]. Elles couvrent notamment le choix du conteneur JSON, la source de vérité, l'organisation des mesures et des voix, les signatures variables et la conservation sans perte de la notation écrite.

## Priorisation

Les questions ci-dessus ne doivent pas bloquer les décisions fondamentales. Traiter d'abord les règles nécessaires au fonctionnement principal de MireDo ; reporter les détails et cas limites jusqu'à ce qu'ils deviennent pertinents pour une implémentation ou un test concret.
