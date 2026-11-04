# Degrés et symboles d'accords

## Degrés harmoniques

Les degrés d'accords peuvent être indiqués à l'aide de chiffres romains :

- `I` à `VII` représentent les sept degrés.
- Cette indication est facultative.
- Son utilisation suit le principe habituel du solfège et de l'analyse harmonique.

MireDo doit permettre de les saisir et de les afficher sans les rendre obligatoires.

## Deux systèmes d'écriture des symboles d'accords

MireDo prend en charge deux façons facultatives d'écrire les symboles d'accords.

### 1. Notation classique avec les lettres latines

Le compositeur peut utiliser les noms d'accords fondés sur les lettres latines, comme dans les logiciels de notation musicale classiques.

Exemples :

- `Gm7`
- `Cmaj7`
- `F#m`

Cette écriture désigne directement les accords selon les noms de notes classiques.

### 2. Notation Sol-fa relative à la référence Do

Le compositeur peut également écrire les symboles d'accords à partir des degrés Sol-fa, en prenant `Do` comme référence.

Dans ce système, le symbole Sol-fa est interprété relativement à la tonalité de référence déclarée pour la partition.

Exemple : si la référence tonale de la partition est `G`, alors `Do` correspond à `G`. Pour représenter un accord de `Gm7`, le compositeur peut donc écrire `Dom7`.

La notation relative ne doit pas être interprétée comme si `Do` désignait systématiquement la note C : sa hauteur dépend de la référence tonale de la partition.

## Caractère facultatif et édition des accords

Les degrés en chiffres romains et les deux systèmes de symboles d'accords sont facultatifs. Le compositeur choisit de les utiliser ou non.

La création, la génération, la modification et la mise en forme des symboles d'accords doivent suivre les usages des logiciels de notation musicale établis, tels que MuseScore. MireDo doit proposer une expérience d'édition comparable, sans imposer l'affichage des accords dans toutes les partitions.

## Distinction entre symbole d'accord et notes écrites

Un symbole d'accord est une indication harmonique destinée à identifier l'accord. Il ne remplace pas les notes effectivement écrites dans les portées et ne doit pas être confondu avec leur saisie ou leur rendu.

Le symbole peut être présent ou absent indépendamment de l'écriture des notes de la partition.
