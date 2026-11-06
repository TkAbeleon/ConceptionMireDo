# Format de fichier MireDo — Dossier de conception

<badge>À concevoir</badge> Le format natif de MireDo n'est pas encore défini. L'extension `.mrd` est envisagée, mais ni l'encodage final ni la structure du fichier ne sont arrêtés.

Ce dossier étudie la proposition d'un conteneur JSON, la compare aux règles musicales déjà validées et prépare la définition progressive du format.

## Documents

- [[01 - Analyse de la proposition JSON]] — compatibilité de la proposition initiale avec les règles Tonic Sol-fa et problèmes à résoudre.
- [[02 - Exigences du format]] — propriétés que le futur format doit respecter.
- [[03 - Modèle logique initial]] — première organisation des données, explicitement provisoire et précisée par les décisions de conception confirmées.
- [[04 - Questions ouvertes]] — décisions nécessaires avant de stabiliser un schéma.
- [[05 - Organisation temporelle du contenu musical]] — hiérarchie MireDo : mesures communes, voix, unités natives, sous-unités et événements.

## État actuel de la conception temporelle

La documentation Tonic Sol-fa distingue désormais la division binaire explicite (point puis virgule pour subdiviser une moitié), la répartition implicite égale des notes et des prolongations en l'absence de signe de division, ainsi que les groupes non binaires déjà définis : le triolet répartit une unité en trois positions égales et le sextolet en six positions égales. Dans la répartition implicite, les éléments comptés remplissent toute l'unité : aucun silence ne peut y être inséré. Voir [[../../02 - Notation Tonic Sol-fa/05 - Rythme et durée]].

La hiérarchie d'organisation du fichier est également explicitée dans [[05 - Organisation temporelle du contenu musical]] : les mesures sont communes à la partition, les voix sont rattachées à chaque mesure, puis leur contenu est organisé en unités natives, sous-unités et événements. Cette hiérarchie relève du modèle MireDo et ne constitue pas une règle de syntaxe Tonic Sol-fa.

Deux références complémentaires sont désormais validées :

- **Structure des durées :** fractions exactes exprimées par rapport à l'unité native Tonic Sol-fa délimitée par `:`.
- **Définition du tempo :** noire par minute (`♩ = valeur`), avec un tempo initial dans le contexte musical et les changements associés à leur position dans la chronologie commune.

La noire n'est donc pas l'unité qui structure les subdivisions Sol-fa ; l'unité native Sol-fa ne remplace pas la référence conventionnelle du tempo.

## Périmètre

Le format devra pouvoir représenter une partition, pas seulement une suite de notes. Il devra tenir compte des voix, de la hauteur, du rythme, des mesures, du tempo, des paroles, des accords, des indications musicales, des reprises et des informations nécessaires à la mise en page.

Le format ne doit toutefois pas inventer de convention musicale. Il enregistre les choix du compositeur et les règles déjà définies.

## Statuts utilisés

- **Validé** — règle musicale ou décision de conception déjà confirmée.
- **Proposition** — solution technique recommandée pour discussion.
- **À clarifier** — une décision utilisateur ou une règle musicale manque.
- **Non décidé** — aucune solution n'est retenue.

## Références

- [[02 - Notation Tonic Sol-fa/00 - Index de la notation|Règles musicales de MireDo]] — source de vérité.
- [[03 - Suivi de conception/Journal des décisions|Journal des décisions]] — décisions confirmées.
- [[03 - Suivi de conception/Questions ouvertes|Questions ouvertes générales]].
- Studio de référence : https://github.com/TkAbeleon/miredo-solfa-studio

Le format `.mrd` textuel actuellement utilisé par le Studio est une syntaxe de démonstration provisoire. Il sert de référence pratique pour certains cas, mais ne constitue pas la spécification du futur fichier natif.
