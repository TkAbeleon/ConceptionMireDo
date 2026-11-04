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
│   └── tempo
├── voices
│   ├── id
│   ├── name
│   └── staff_reference
├── measures
│   ├── mesure commune
│   ├── données de chaque voix
│   └── indications et barres
├── lyrics
├── annotations
└── layout
```

Les blocs sont séparés conceptuellement afin de ne pas mélanger les règles musicales, les voix et les préférences de rendu.

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
    "disposition": [2, 2]
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

## 4. Attention : signatures variables

La proposition initiale utilise successivement 4/4, 3/4 et 2/4.

L'exemple JSON ci-dessus conserve une signature 4/4 commune parce que c'est le cas actuellement représenté par les règles de conception générales et le Studio.

Une future version du modèle pourrait prévoir une surcharge de signature au niveau d'une mesure ou d'une section. Ce champ ne doit cependant être activé comme comportement musical qu'après décision explicite dans [[04 - Questions ouvertes]] et mise à jour des règles de rythme.

Si les signatures variables sont validées, la mesure qui change de signature devra porter une seule valeur commune à toutes les voix, jamais une valeur indépendante dans chaque voix.

## 5. Éléments volontairement non spécifiés dans cet exemple

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

## 6. Utilisation du Studio comme référence

Le Studio contient déjà un modèle d'exécution `Score` qui distingue :

- `Header` : contexte global de la partition ;
- `Voice` : voix et mesures ;
- `Unit` : jetons écrits, slots rythmiques et séparateur ;
- `NoteInfo` : hauteur et durée calculées ;
- `structure`, `chords`, `lyrics` et `breaks` : annotations et mise en page.

Ce modèle est utile pour identifier les besoins, mais il n'est pas encore un modèle de fichier natif : les Maps, identifiants internes, diagnostics et données calculées devront être examinés avant de décider ce qui est sérialisé.
