# Architecture de MireDo — Index

Ce dossier rassemble les travaux de conception technique de MireDo. Il ne définit pas les règles musicales : celles-ci restent dans [[02 - Notation Tonic Sol-fa/00 - Index de la notation|la conception de la notation]].

## Domaines

- [[Format de fichier MireDo/00 - Index|Format de fichier MireDo]] — conception du format natif envisagé, de son modèle de données et de sa sérialisation.
- Architecture logicielle — à documenter lorsque les responsabilités des composants seront suffisamment stabilisées.
- Formats d'échange et conversions — à concevoir séparément du format natif.

## Principe de séparation

La conception doit distinguer :

1. les règles musicales validées ;
2. le modèle logique interne d'une partition ;
3. le format de fichier qui sérialise ce modèle ;
4. les formats d'import/export ;
5. le rendu visuel et les préférences d'affichage.

Une décision de format ne crée pas une nouvelle règle Tonic Sol-fa. Toute règle musicale doit d'abord être confirmée dans le dossier [[02 - Notation Tonic Sol-fa/00 - Index de la notation|Notation Tonic Sol-fa]].
