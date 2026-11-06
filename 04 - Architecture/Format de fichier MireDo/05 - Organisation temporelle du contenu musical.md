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

## 6. Les sous-unités : subdivisions internes

Une unité peut être organisée en sous-unités, c'est-à-dire en portions temporelles plus petites.

Dans le modèle MireDo, le niveau « sous-unité » sert à organiser la répartition temporelle à l'intérieur d'une unité. Il ne constitue pas une nouvelle unité native et ne modifie pas la durée totale de celle-ci.

Les sous-unités permettent de situer les événements à des positions exactes. Elles peuvent correspondre à une répartition égale ou participer à une répartition dont les durées sont inégales.

La documentation musicale Tonic Sol-fa décrit les signes et conventions qui peuvent conduire à ces répartitions : division explicite, répartition implicite, triolet, sextolet et portions silencieuses. Le modèle MireDo doit représenter le résultat temporel de ces règles sans confondre la structure de données avec les signes de la notation source.

Le modèle temporel utilise des fractions exactes relatives à l'unité native. Tout entier positif N peut servir de dénominateur pour représenter une division en N positions ; aucune liste fermée de dénominateurs n'est imposée. Les règles détaillées figurent dans [[../../02 - Notation Tonic Sol-fa/05 - Rythme et durée]].

## 7. Les événements

Les événements sont les éléments qui occupent les positions temporelles dans une unité ou ses subdivisions.

Le socle du modèle distingue trois catégories :

- **Note :** événement portant une hauteur et produisant une attaque.
- **Silence :** portion de temps sans hauteur ni attaque.
- **Prolongation :** segment temporel qui prolonge une note précédente sans créer une nouvelle attaque.

Une prolongation reste rattachée à la note qu'elle prolonge. La durée totale de la note comprend ses segments de prolongation, tandis que la conservation des segments permet de préserver l'écriture source.

Le code numérique d'un événement, sa position temporelle et sa durée sont des informations différentes. L'échelle entière des codes est décrite dans [[../../02 - Notation Tonic Sol-fa/06 - Échelle numérique des événements]] ; les positions et durées sont décrites dans [[../../02 - Notation Tonic Sol-fa/05 - Rythme et durée]].

## 8. Exemple conceptuel d'organisation

Exemple abstrait d'une mesure contenant deux voix :

~~~text
Partition
└── Mesure commune
    ├── Voix Soprano
    │   ├── Unité 1
    │   │   ├── Sous-unité 1 → Note
    │   │   ├── Sous-unité 2 → Silence
    │   │   └── Sous-unité 3 → Note
    │   └── Unité 2
    │       └── Événements de la voix
    └── Voix Basse
        ├── Unité 1
        │   ├── Sous-unité 1 → Note
        │   └── Sous-unité 2 → Prolongation de cette note
        └── Unité 2
            └── Événements de la voix
~~~

Cet exemple illustre uniquement les relations entre les niveaux. Il ne fixe ni le nombre d'unités d'une mesure donnée, ni le nombre de sous-unités, ni les propriétés JSON à utiliser.

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
