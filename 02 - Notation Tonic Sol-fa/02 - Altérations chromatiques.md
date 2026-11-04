# Altérations chromatiques

## État des règles

<badge color="success">Principe validé</badge> MireDo accepte les formes d'altération définies par la convention Tonic Sol-fa retenue, y compris les variantes rares.

<badge color="success">Principe validé</badge> Les équivalences de hauteur sont traitées selon le même principe que les équivalences enharmoniques du solfège classique.

## Altération ascendante

L'ajout de la voyelle `i` au symbole du degré indique une élévation d'un demi-ton.

Formes :

- `d` devient `di`
- `r` devient `ri`
- `m` devient `mi`
- `f` devient `fi`
- `s` devient `si`
- `l` devient `li`
- `t` devient `ti`

## Altération descendante

Pour abaisser un degré d'un demi-ton, la convention Tonic Sol-fa utilise les formes vocaliques correspondantes. Plusieurs variantes peuvent exister selon le degré et l'usage.

MireDo doit accepter toutes les formes valides définies par cette convention, y compris celles qui sont peu fréquentes. Il ne faut pas limiter le parseur aux seules formes les plus courantes.

Exemple confirmé :

- `te`, `ta` et `to` sont des variantes acceptées pour le degré `t) abaissé.
- Les autres formes descendantes prévues par la convention sont également acceptées, même si elles sont rarement utilisées.

La liste exhaustive des variantes et leur association à chaque degré doivent rester conformes aux règles du Tonic Sol-fa ; MireDo ne doit pas inventer de nouvelles formes.

## Équivalences de hauteur et enharmonie

Le Tonic Sol-fa est traité selon le même principe que le solfège classique : deux graphies différentes peuvent désigner une même hauteur sonore.

En solfège classique, par exemple :

- C♭ et B peuvent désigner la même hauteur.
- E♯ et F peuvent désigner la même hauteur.

Le même principe s'applique au Tonic Sol-fa. Exemples :

- `de` et `t` peuvent désigner la même hauteur.
- `mi` et `f` peuvent désigner la même hauteur.

Ces équivalences sont des équivalences de hauteur, pas des substitutions orthographiques. Elles dépendent du contexte d'octave : une équivalence située à la limite de l'octave doit conserver le déplacement d'octave correspondant.

MireDo doit donc distinguer :

1. la graphie originale saisie ;
2. le degré Sol-fa et son altération ;
3. la hauteur absolue calculée, octave comprise.

Le calculateur de hauteur peut reconnaître deux graphies comme équivalentes, mais l'éditeur, le parseur et la sérialisation doivent conserver la graphie originale. MireDo ne doit jamais réécrire automatiquement une note en sa forme enharmonique équivalente.

## Formes courantes et formes rares

Toutes les formes valides sont acceptées, mais elles n'ont pas toutes la même fréquence d'utilisation.

Les formes courantes à privilégier dans l'affichage pédagogique, les aides à la saisie et les suggestions sont notamment :

`d`, `di`, `r`, `ri`, `m`, `mi`, `f`, `fi`, `s`, `l`, `te`, `ti`, `to`.

Les autres formes valides restent prises en charge, sans être mises au même niveau de visibilité. Elles peuvent être peu connues des débutants et utilisées seulement dans des contextes particuliers.

Cette préférence d'interface ne constitue pas une restriction grammaticale : une forme rare mais valide doit être analysée et conservée.

## Signes accidentels

Dans la convention Tonic Sol-fa décrite ici, les altérations sont exprimées par les syllabes et leurs variantes. Les symboles autonomes `♮`, `♯` et `♭` ne sont pas introduits comme signes écrits des notes Sol-fa, sauf décision distincte concernant une autre notation.

Les lettres `b` et `#` peuvent être utilisées dans les étiquettes de tonalité conformément aux règles de référence tonale ; cela ne signifie pas qu'elles remplacent les formes syllabiques dans les notes Sol-fa.

## Conséquences pour l'implémentation

- Le parseur reconnaît toutes les graphies valides du Tonic Sol-fa.
- Le moteur de hauteur calcule leur hauteur absolue et détecte les équivalences enharmoniques.
- La graphie d'origine est conservée dans le modèle de données et lors de la sérialisation.
- Aucune normalisation automatique ne remplace une graphie par une autre.
- L'interface privilégie les formes courantes, tout en permettant la saisie et l'affichage des formes rares.
- La validation porte sur la conformité à la convention Sol-fa, pas sur la fréquence d'utilisation d'une forme.

## Points restant à préciser

- Compléter, à partir de la convention de référence, l'inventaire exhaustif des formes descendantes et de leurs variantes.
- Déterminer si les suggestions de saisie doivent proposer les formes rares à la demande ou seulement les accepter lorsqu'elles sont saisies.
- Définir précisément la représentation des équivalences aux limites d'octave dans le modèle de hauteur.
