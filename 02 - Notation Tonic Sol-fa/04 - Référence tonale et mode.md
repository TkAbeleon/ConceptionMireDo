# Référence tonale et mode majeur / mineur

## Principe

<badge color="success">Validé</badge> L'interprétation des degrés dépend du contexte tonal choisi et déclaré dans la partition. MireDo ne doit pas imposer une représentation unique du mode mineur.

## Exemples de représentation

### Exemple : La mineur (Am)

Une partition peut utiliser Do majeur comme référence et considérer `l` comme centre tonal (tonique) dans le contexte de La mineur.

Dans cette représentation, les syllabes Sol-fa ne sont pas modifiées simplement parce que le morceau est mineur.

### Autre référence possible

Une partition peut choisir une autre référence tonale, par exemple Sol, et employer les degrés correspondants selon ce choix.

Le choix dépend de la manière dont le compositeur a construit et déclaré la partition.

## Conséquence pour MireDo

Le moteur doit distinguer :
- la référence tonale utilisée pour interpréter les degrés ;
- le mode ou contexte tonal de la pièce ;
- la syllabe Sol-fa écrite ;
- la hauteur absolue calculée.

Le mode mineur ne doit pas déclencher à lui seul une réécriture automatique des syllabes.

## Bécarre et altérations

Selon la convention décrite, il n'existe pas de signe autonome de bécarre dans l'écriture Sol-fa. Les syllabes et formes altérées sont employées directement.

## Questions ouvertes

- Quelle structure de métadonnées permettra d'exprimer sans ambiguïté la référence tonale et le centre tonal ?
- Comment décrire une partition dont la référence change en cours de morceau ?
- Comment représenter les changements de contexte tonal sans perdre la graphie originale ?
