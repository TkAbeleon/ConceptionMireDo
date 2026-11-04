# Modèle logique initial du fichier MireDo

<badge>Proposition</badge> Ce document présente une première organisation des données à discuter. Ce n'est ni un schéma JSON final, ni une spécification normative.

## 1. Organisation générale recommandée

Le fichier pourrait s'organiser autour des blocs suivants :

```text
Fichier MireDo
├── format et version
├── metadata
├── musical_context
│   ├── notation_system
│   ├── reference_tone
│   ├── time_signature
│   ├── disposition
│   └── tempo_initial
├── voices
│   ├── id
│   ├── name
│   └── staff_reference
├── measures
│   ├── mesure commune
│   ├── données de chaque voix
│   └── indications et barres
├── tempo_changes
├── lyrics
├── annotations
└── layout
```

Les blocs sont séparés conceptuellement afin de ne pas mélanger les règles musicales, les voix et les préférences de rendu. Le tempo initial appartient au contexte temporel de la partition ; les changements ultérieurs sont positionnés dans la chronologie commune.

## 2. Exemple JSON exploratoire

L'exemple suivant reprend l'intention générale de la proposition initiale, mais corrige plusieurs ambiguïtés :

- une entrée de `measures` correspond à une seule mesure ;
- les données des voix sont réunies dans la même mesure ;
- la référence tonale est `D`, sans être mélangée à l'étiquette visuelle « Do = » ;
- la référence de portée est distincte du nom de la voix ;
- les notes graves sont écrites avec le suffixe numérique `_1` ;
- le regroupement usuel du 4/4 utilise `!`.

```json
{
  "format": "miredo",
  "format_version": "0.1.0-draft",
  "metadata": {
    "title": "Misaora an'i Jehovah",
    "composer": "RAKOTONDRATSIMBA Vola",
    "description": "Exemple exploratoire de partition polyphonique"
  },
  "musical_context": {
    "notation_system": "tonic-sol-fa",
    "reference_tone": "D",
    "time_signature": "4/4",
    "disposition": [2, 2],
    "initial_tempo": {
      "unit": "quarter_note",
      "beats_per_minute": 80
    }
  },
  "voices": [
    {
      "id": "soprano",
      "name": "Soprano",
      "staff_reference": 0
    },
    {
      "id": "bass",
      "name": "Basse",
      "staff_reference": -1
    }
  ],
  "measures": [
    {
      "id": "m1",
      "number": 1,
      "voices": {
        "soprano": {
          "notation": "d:r!m:f"
        },
        "bass": {
          "notation": "d_1:-!d_1:-"
        }
      }
    },
    {
      "id": "m2",
      "number": 2,
      "voices": {
        "soprano": {
          "notation": "s:-!m:-"
        },
        "bass": {
          "notation": "d_1:-!d_1:-"
        }
      }
    }
  ],
  "tempo_changes": [
    {
      "position": {
        "measure_id": "m2",
        "offset": {
          "numerator": 0,
          "denominator": 1
        }
      },
      "unit": "quarter_note",
      "beats_per_minute": 100
    }
  ],
  "lyrics": {
    "common": [],
    "by_voice": {}
  },
  "annotations": [],
  "layout": {
    "brace_visible": true,
    "lyrics_position": "below"
  }
}
```

Cet exemple est uniquement illustratif : il ne fixe pas la structure définitive des positions, ni le schéma de sérialisation. Il montre cependant que le tempo initial et les changements de tempo sont distincts de la hiérarchie des unités Sol-fa.

## 3. Ce que cet exemple démontre

### Mesure commune

Les mesures sont déclarées une seule fois. Les données de Soprano et de Basse sont rattachées à la même mesure par leur identifiant de voix. Cela réduit les risques de décalage entre voix et évite de répéter la numérotation dans chaque piste.

### Référence tonale

`reference_tone` contient uniquement la référence musicale, par exemple `D` ou `Ab`. Le libellé visible « Do = » est une préférence de présentation et non la valeur musicale elle-même.

Aucun mode majeur ou mineur n'est déduit automatiquement de cette référence.

### Référence de portée

`staff_reference` est indépendante du nom. La valeur `-1` de la Basse reprend la convention de référence de portée actuellement décrite dans la conception. Le lien exact entre référence et hauteur jouée reste un sujet distinct.

### Fragments de notation

`notation` est, pour cet exemple, une chaîne Sol-fa écrite sans les barres extérieures de mesure : la mesure JSON fournit déjà cette frontière.

Cette approche est simple et permet de réutiliser progressivement le travail du Studio. Elle implique néanmoins que les subdivisions, les notes et les séparateurs contenus dans cette chaîne continuent à être analysés par un parseur.

Le maintien de la chaîne écrite comme source de vérité, ou son remplacement par une liste d'événements structurés, n'est pas encore décidé.

## 4. Deux références temporelles distinctes

Le modèle utilise deux références qui répondent à des besoins différents. Elles ne doivent pas être confondues ni fusionnées dans un seul champ.

### 4.1 Unité native Tonic Sol-fa : structure des durées

L'unité native est l'unité principale délimitée par `:`. Sa valeur dépend du dénominateur de la signature rythmique, conformément aux conventions documentées dans [[../../02 - Notation Tonic Sol-fa/05 - Rythme et durée]].

Les fractions exactes des subdivisions et des événements sont exprimées relativement à cette unité native. La hiérarchie mesure → voix → unité → subdivision → événement reste donc fidèle à l'organisation de la notation Sol-fa.

### 4.2 Noire : référence conventionnelle du tempo

La noire sert de référence fixe pour exprimer la vitesse :

- `♩ = 80` signifie 80 noires par minute ;
- le tempo initial est enregistré dans le contexte musical de la partition ;
- un changement de tempo est enregistré à sa position précise dans la chronologie commune ;
- toutes les indications de tempo utilisent la même référence de noire par minute.

La noire n'est donc pas l'unité qui structure les subdivisions Sol-fa. Elle sert à exprimer le tempo et à convertir les durées vers les conventions d'autres logiciels.

### 4.3 Exemple d'indépendance

En 6/8, une unité native Sol-fa vaut une croche selon les conventions décrites. Si le tempo est indiqué `♩ = 80`, la vitesse reste définie comme 80 noires par minute. La relation entre l'unité native et la noire est calculée à partir de la signature ; elle ne change pas la référence de tempo.

Un changement de signature et un changement de tempo restent deux données distinctes, même lorsqu'ils apparaissent à la même position musicale.

## 5. Attention : signatures variables

La proposition initiale utilise successivement 4/4, 3/4 et 2/4.

L'exemple JSON ci-dessus conserve une signature 4/4 commune parce que c'est le cas actuellement représenté par les règles de conception générales et le Studio.

Une future version du modèle pourrait prévoir une surcharge de signature au niveau d'une mesure ou d'une section. Ce champ ne doit cependant pas être activé comme comportement musical qu'après décision explicite dans [[04 - Questions ouvertes]] et mise à jour des règles de rythme.

Si les signatures variables sont validées, la mesure qui change de signature devra porter une seule valeur commune à toutes les voix, jamais une valeur indépendante dans chaque voix.

## 6. Éléments volontairement non spécifiés dans cet exemple

L'exemple ne fixe pas encore :

- la forme complète des subdivisions comme événements structurés ;
- la position des doubles barres au milieu d'une mesure ;
- les changements de référence tonale à une position précise ;
- les indications de transition ;
- les paroles alignées sur les attaques ;
- les accords et degrés harmoniques ;
- les reprises et indications de performance ;
- les retours de systèmes et sauts de page ;
- la stratégie de sauvegarde sans perte.

Ces éléments sont identifiés dans [[02 - Exigences du format]] et [[04 - Questions ouvertes]].

## 7. Utilisation du Studio comme référence

Le Studio contient déjà un modèle d'exécution `Score` qui distingue :

- `Header` : contexte global de la partition ;
- `Voice` : voix et mesures ;
- `Unit` : jetons écrits, slots rythmiques et séparateur ;
- `NoteInfo` : hauteur et durée calculées ;
- `structure`, `chords`, `lyrics` et `breaks` : annotations et mise en page.

Ce modèle est utile pour identifier les besoins, mais il n'est pas encore un modèle de fichier natif : les Maps, identifiants internes, diagnostics et données calculées devront être examinés avant de décider ce qui est sérialisé.

## 8. Décisions de conception confirmées le 2026-11-04

### 8.1 Hiérarchie temporelle

Le contenu rythmique conserve une organisation hiérarchique explicite :

```text
Partition
└── Mesure commune
    └── Voix dans la mesure
        └── Unité native Sol-fa
            └── Subdivision
                └── Événement
```

Cette hiérarchie est préférée à une représentation initiale qui aplatirait immédiatement toute la partition en une seule liste chronologique de notes.

### 8.2 Durées exactes et référence structurelle

Les durées sont représentées par des fractions exactes, exprimées relativement à l'unité native Tonic Sol-fa délimitée par `:`. La valeur de cette unité dépend de la signature rythmique.

La noire n'est pas l'unité structurelle des subdivisions Sol-fa.

### 8.3 Référence conventionnelle du tempo

La noire est la référence conventionnelle de toutes les indications de tempo. Le tempo initial appartient au contexte musical de la partition. Les changements de tempo sont enregistrés à une position précise dans la chronologie commune.

La signature rythmique et le tempo sont deux paramètres distincts.

### 8.4 Notes et prolongations

Une note dispose d'une durée totale calculée, incluant ses éventuelles prolongations. En parallèle, la structure conserve les segments d'origine qui composent cette prolongation.

La durée totale sert aux calculs et à la synchronisation ; les segments préservent l'écriture source. Ces informations doivent rester cohérentes et ne sont pas deux durées indépendantes modifiables séparément.

### 8.5 Périmètre du socle rythmique

Le premier modèle se concentre sur les unités, subdivisions, notes, silences, groupes rythmiques et prolongations.

Les indications supplémentaires telles que D.C., D.S., nuances, crescendo/diminuendo et articulations sont reportées à une étape ultérieure. Le tempo initial et ses changements font exception : ils sont nécessaires au contexte temporel de la partition et font partie du modèle de base.

### 8.6 Points encore ouverts

- La nécessité et la forme d'identifiants stables pour les événements.
- La forme finale de sérialisation et le schéma JSON.
- La possibilité de changer de signature et de disposition au cours d'une partition.
- La représentation détaillée des positions temporelles dans le schéma définitif.

Ces points restent dans [[04 - Questions ouvertes]].
