# Organisation temporelle du contenu musical dans MireDo

<badge>Principe d'organisation du modèle</badge>

Ce document décrit la logique propre à MireDo pour organiser les données temporelles d'une partition dans le fichier natif. Il ne définit pas la grammaire de la notation Tonic Sol-fa et ne remplace pas les règles musicales de [[../../02 - Notation Tonic Sol-fa/05 - Rythme et durée]].

L'objectif est de définir comment le contenu est rangé et relié dans le modèle du fichier : partition, mesures, voix, unités, subdivisions et événements.

## 1. Hiérarchie générale

Le contenu musical temporel suit cette hiérarchie :

~~~text
Partition
└── Mesures communes
    └── Mesure
        └── Voix
            └── Unités natives
                └── Sous-unités (subdivisions)
                    └── Événements
~~~

Cette organisation décrit l'emboîtement des données dans MireDo. Elle ne signifie pas que chaque niveau doit nécessairement être matérialisé par un objet JSON indépendant : les propriétés et la forme exacte de sérialisation restent à définir.

## 2. La partition

La partition constitue le conteneur global du contenu musical.

Elle porte le contexte commun nécessaire à l'interprétation de ses mesures et de ses voix : notamment la signature rythmique, la référence tonale, le tempo et les informations générales de la partition.

Les données communes ne doivent pas être répétées dans chaque voix lorsqu'elles s'appliquent à toute la partition.

## 3. Les mesures : une chronologie commune

Les mesures appartiennent à la partition et sont communes à toutes les voix.

Une mesure est donc déclarée une seule fois dans la chronologie de la partition. Les contenus des différentes voix sont rattachés à cette même mesure.

Conséquences :

- la mesure numéro N est le même intervalle musical pour toutes les voix ;
- une voix ne possède pas sa propre numérotation indépendante des mesures ;
- les limites de mesure sont communes ;
- les contenus des voix peuvent être différents, mais ils se situent dans le même cadre temporel ;
- une mesure ne doit pas être dupliquée une fois par voix.

La structure commune évite qu'une voix soit décalée dans sa numérotation ou qu'une même position de partition désigne accidentellement des mesures différentes.

## 3.1 Indexation des mesures et point d'ancrage

La chronologie de la partition possède un **point d'ancrage d'indice 0**, qui représente l'origine temporelle de la partition, avant le début de la première mesure.

Les mesures effectives sont ensuite indexées de **1 à n**, dans leur ordre chronologique :

- **0** : point d'ancrage initial ; ce n'est pas une mesure ;
- **1** : première mesure ;
- **2** : deuxième mesure ;
- **…**
- **n** : dernière mesure de la partition.

Le point d'ancrage 0 sert de référence à l'origine de la chronologie. Il ne contient pas une mesure et ne compte pas dans le nombre de mesures. Une partition qui contient n mesures possède donc n mesures numérotées de 1 à n, en plus de son ancrage initial.

Cette indexation est commune à toutes les voix : il n'existe pas de mesure 1 propre à la Soprano et une autre mesure 1 propre à la Basse.

## 4. Les voix à l'intérieur d'une mesure

Chaque mesure contient les données temporelles de chacune des voix concernées.

Une voix conserve son identité stable dans la partition. Son nom, sa référence de portée et les événements qu'elle joue sont des informations distinctes.

Dans une mesure donnée, chaque voix possède son propre contenu rythmique. Les événements d'une voix ne sont pas mélangés à ceux d'une autre voix ; leur synchronisation résulte de leur rattachement à la même mesure et de leurs positions temporelles respectives.

Une voix peut contenir des notes, des silences et des prolongations. Une portion silencieuse dans une voix n'implique pas que les autres voix soient silencieuses au même moment.

## 5. Les unités natives dans une voix

À l'intérieur de chaque mesure et de chaque voix, le contenu est organisé en unités natives Tonic Sol-fa.

Une unité native est le niveau temporel principal utilisé par le modèle. Sa durée réelle dépend de la signature rythmique, conformément aux règles musicales documentées séparément.

Pour le modèle MireDo :

- les unités appartiennent au contenu d'une voix dans une mesure ;
- elles se succèdent dans l'ordre de la mesure ;
- chacune représente un intervalle temporel complet ;
- les subdivisions et événements qu'elle contient ne peuvent pas dépasser ses limites ;
- l'ensemble des unités d'une voix doit couvrir le cadre temporel de la mesure, selon les règles de complétude applicables.

L'unité native n'est pas une sous-unité et ne doit pas être confondue avec la noire de référence utilisée pour exprimer le tempo.

## 5.1 Indexation des unités dans une mesure

Dans chaque mesure, les unités natives sont indexées localement de **1 à n**, où **n est le nombre d'unités natives que contient cette mesure** selon sa signature et la disposition retenue.

- **1** : première unité de la mesure ;
- **2** : deuxième unité ;
- **…**
- **n** : dernière unité de la mesure.

Cette numérotation recommence à 1 au début de chaque nouvelle mesure. Elle est locale à la mesure : l'unité 1 de la mesure 2 est distincte de l'unité 1 de la mesure 1.

Le nombre n n'est pas une constante universelle : il dépend de la structure de la mesure considérée. Les unités sont présentes dans le contenu de chaque voix, mais elles correspondent aux mêmes intervalles temporels pour toutes les voix de cette mesure.

## 6. Les sous-unités : subdivisions internes

Une unité peut être organisée en sous-unités, c'est-à-dire en portions temporelles plus petites.

Dans le modèle MireDo, le niveau « sous-unité » sert à organiser la répartition temporelle à l'intérieur d'une unité. Il ne constitue pas une nouvelle unité native et ne modifie pas la durée totale de celle-ci.

Les sous-unités permettent de situer les événements à des positions exactes. Elles peuvent correspondre à une répartition égale ou participer à une répartition dont les durées sont inégales.

La documentation musicale Tonic Sol-fa décrit les signes et conventions qui peuvent conduire à ces répartitions : division explicite, répartition implicite, triolet, sextolet et portions silencieuses. Le modèle MireDo doit représenter le résultat temporel de ces règles sans confondre la structure de données avec les signes de la notation source.

Le modèle temporel utilise des fractions exactes relatives à l'unité native. Tout entier positif N peut servir de dénominateur pour représenter une division en N positions ; aucune liste fermée de dénominateurs n'est imposée. Les règles détaillées figurent dans [[../../02 - Notation Tonic Sol-fa/05 - Rythme et durée]].

## 6.1 Repérage fractionnaire des sous-unités

Les sous-unités ne sont pas repérées par une numérotation globale qui se poursuivrait d'une unité à l'autre. Elles sont situées **à l'intérieur de leur unité native**, au moyen des fractions exactes déjà définies dans le modèle temporel.

Pour une division d'une unité en N positions égales, les positions sont :

`0/N, 1/N, 2/N, …, (N-1)/N`.

- `0/N` est l'ancrage du début de l'unité ;
- `1/N` est le début de la deuxième portion ;
- `2/N` est le début de la troisième portion ;
- etc. ;
- `N/N` est la frontière de fin de l'unité, et non une nouvelle sous-unité.

N est un entier strictement positif et n'est pas limité à une liste prédéfinie. Le même principe permet de représenter les divisions en 2, 3, 4, 5, 6, 7 ou tout autre nombre entier positif de portions.

Pour des durées inégales, les positions sont toujours des fractions exactes rapportées à l'unité. Un dénominateur commun permet de représenter exactement les débuts des segments. Les fractions servent donc à situer les événements dans l'unité ; elles ne constituent pas des numéros de sous-unités indépendants.

Le dénominateur et les fractions sont locaux à l'unité considérée. Une position `1/3` dans une unité signifie un tiers de cette unité, quelle que soit la mesure dans laquelle elle se trouve.

## 7. Les événements

Les événements sont les éléments qui occupent les positions temporelles dans une unité ou ses subdivisions.

Le socle du modèle distingue trois catégories :

- **Note :** événement portant une hauteur et produisant une attaque.
- **Silence :** portion de temps sans hauteur ni attaque.
- **Prolongation :** segment temporel qui prolonge une note précédente sans créer une nouvelle attaque.

Une prolongation reste rattachée à la note qu'elle prolonge. La durée totale de la note comprend ses segments de prolongation, tandis que la conservation des segments permet de préserver l'écriture source.

Le code numérique d'un événement, sa position temporelle et sa durée sont des informations différentes. L'échelle entière des codes est décrite dans [[../../02 - Notation Tonic Sol-fa/06 - Échelle numérique des événements]] ; les positions et durées sont décrites dans [[../../02 - Notation Tonic Sol-fa/05 - Rythme et durée]].

## 8. Exemple conceptuel d'organisation

Exemple abstrait d'une mesure contenant deux voix. Dans la première unité de la Soprano, les événements commencent aux positions fractionnaires indiquées :

~~~text
Partition
└── Mesure commune
    ├── Voix Soprano
    │   ├── Unité 1
    │   │   ├── Position 0/3 → Note
    │   │   ├── Position 1/3 → Silence
    │   │   └── Position 2/3 → Note
    │   └── Unité 2
    │       └── Événements de la voix
    └── Voix Basse
        ├── Unité 1
        │   ├── Position 0/2 → Note
        │   └── Position 1/2 → Prolongation de cette note
        └── Unité 2
            └── Événements de la voix
~~~

Les fractions indiquent des positions relatives au début de l'unité native ; elles ne sont pas des numéros de sous-unités. Ainsi, `1/3` désigne le début de la deuxième portion d'une division en trois, et `1/2` le début de la deuxième portion d'une division en deux. La prolongation reste liée à la note précédente et ne crée pas une nouvelle attaque.

Cet exemple illustre uniquement les relations entre les niveaux et le repérage fractionnaire. Il ne fixe ni le nombre d'unités d'une mesure donnée, ni les propriétés JSON à utiliser.

## 9. Ce qui relève de cette organisation et ce qui n'en relève pas

Cette hiérarchie décrit l'organisation interne des données temporelles du fichier. Elle ne doit pas être confondue avec :

- la syntaxe écrite Tonic Sol-fa (barre de mesure, séparateurs, signes de division et de prolongation) ;
- les règles musicales qui déterminent la durée d'une note, d'un silence ou d'une prolongation ;
- la mise en page graphique des portées et des systèmes ;
- le choix de saisie compacte ou explicite dans l'éditeur ;
- les noms définitifs des propriétés JSON.

La signature rythmique et la disposition de notation restent distinctes. De même, le regroupement visuel ou notationnel des unités ne crée pas une durée supplémentaire et ne doit pas dupliquer les événements.

## 10. Principes à préserver dans le futur fichier .mrd

1. Une chronologie de mesures commune à toute la partition.
2. Une seule occurrence de chaque mesure dans cette chronologie.
3. Les contenus des voix rangés dans la mesure commune correspondante.
4. Les unités natives rangées dans chaque contenu de voix.
5. Les sous-unités rattachées à leur unité native.
6. Les événements rattachés à leur position dans l'unité.
7. Les notes, silences et prolongations distingués sans les confondre.
8. Les positions et durées représentées exactement, sans nombres flottants.
9. Les informations musicales séparées des préférences de mise en page.
10. Aucune propriété ou clé JSON définitive n'est imposée par ce document.

Ce document fixe donc une logique d'organisation du modèle MireDo. Il prépare la définition du schéma du fichier sans anticiper les noms de champs ni trancher les questions de sérialisation encore ouvertes.
