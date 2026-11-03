# Cahier des Charges & Spécifications Techniques : SDK Solfa Engine

## 1. Présentation du Projet et Objectifs

### 1.1 Contexte et Description Générale

Le projet **Solfa Engine** est une bibliothèque logicielle (SDK) open-source performante et modulaire, conçue pour l'analyse, la conversion, le stockage et la génération de musique écrite en **notation Solfa (Tonic Sol-fa)**.

La notation Solfa est un système de notation musicale largement utilisé (notamment au sein des chorales africaines, malgaches, britanniques, etc.) qui s'appuie sur des lettres (`d`, `r`, `m`, `f`, `s`, `l`, `t`) et des séparateurs rythmiques (`:`, `.`, `,`, `|`) à la place de la portée traditionnelle.

Le SDK fait office de **moteur pivot** : il isole la sémantique musicale pure de toute représentation visuelle ou audio spécifique.

### 1.2 Objectifs Stratégiques

1. **Pérenniser et Normaliser la notation Solfa** à travers une structure de données orientée objet et fortement typée.

2. **Fournir un format d'échange ouvert (Pivot)** garantissant l'interopérabilité entre applications, formats historiques (`.drm`, `.nto`) et standards de l'industrie musicale (`MusicXML`, `MIDI`).

3. **Optimiser les performances** pour les applications mobiles et desktop à l'aide d'un stockage hybride (JSON lisible / Protobuf ou MessagePack binaire / PostgreSQL JSONB).

4. **Offrir un moteur de rendu abstrait** traduisant les structures de données atomiques en représentations graphiques ou textuelles à la volée.

## 2. Exigences Fonctionnelles et Non-Fonctionnelles

### 2.1 Exigences Fonctionnelles (Functional Requirements)

* **Ingestion / Parsing :**

  * Conversion des chaînes et formats textuels Solfa en modèle orienté objet interne.

  * Ingestion du format pivot JSON (`.solfa.json`).

  * Ingestion des formats binaires optimisés (MessagePack / Protobuf).

* **Gestion du Temps et du Rythme :**

  * Support complet des métriques simples et composées ($2/4$, $3/4$, $4/4$, $6/8$, $9/8$, $12/8$, etc.).

  * Gestion autonome des anacrouses (Mesure 0 / Pickup measure) avec calcul en mémoire vive des temps absolus négatifs pour la synchronisation audio/défilement.

  * Calcul dynamique du temps absolu ($T_{global}$) sans écriture redondante dans le fichier de stockage.

* **Configuration Flexible des Voix (SATB et Formats Personnalisés) :**

  * Configuration explicite de l'ordre d'affichage, de la clef (`treble`/sol, `bass`/fa, `alto`, etc.) et du décalage d'octave (`octave_shift`) par voix (ex. Soprano: 0, Clef de Sol ; Ténor: -1, Clef de Fa).

  * Support de configurations non-SATB (chœur d'hommes, chœur d'enfants, duos, trios, musique instrumentale).

* **Transposition et Tonalités :**

  * Calcul déterministe des notes MIDI absolues selon la tonalité spécifiée ($Do = \text{Tonalité de référence}$) et le décalage d'octave propre à chaque voix.

  * Transposition dynamique à la volée.

* **Support Polyphonique et Textes :**

  * Support multi-voix indépendantes.

  * Alignement déterministe syllabe-par-syllabe sur les événements musicaux.

  * Prise en charge des articulations (points d'orgue/fermata, accents, staccato) et des nuances (dynamics, tempo).

* **Exporteurs :**

  * Export vers **MusicXML** (pour édition dans MuseScore, Finale, Sibelius).

  * Export vers **MIDI** (pour synthèse et restitution audio).

  * Export vers **JSON Pivot** et **Formats Binaires**.

### 2.2 Exigences Non-Fonctionnelles (Non-Functional Requirements)

* **Architecture DRY (Don't Repeat Yourself) :** Aucune redondance de données dérivables (pas de `global_time` en dur).

* **Performance et Compacité :**

  * Temps de sérialisation / désérialisation binaire ultra-rapide sur terminaux mobiles.

  * Faible empreinte mémoire vive lors du traitement de pièces polyphoniques de grande envergure.

* **Maintenabilité et Typage :** Modèle entièrement modélisé par des types stricts (TypeScript / Python Dataclasses / Protobuf Schemas).

* **Indépendance de la Vue :** Le moteur ne dépend d'aucun framework graphique (React, Flutter, Qt).

## 3. Architecture Technique et Flux de Données

```
 +------------------+     +-------------------+     +------------------+
 |  Fichiers Texte  |     |  Formats Binaires |     |   Bases de DTO   |
 |  (.solfa, .nto)  |     | (MessagePack/PB)  |     | (PostgreSQL JSONB)|
 +--------+---------+     +---------+---------+     +--------+---------+
          |                         |                        |
          +------------------+      |      +-----------------+
                             v      v      v
                   +-------------------------------+
                   |       MOTEUR CORE (SDK)       |
                   |   - Parser / Serializer       |
                   |   - Engine Temporel & MIDI    |
                   |   - Calculations & Transpos  |
                   +---------------+---------------+
                                   |
         +-------------------------+-------------------------+
         |                         |                         |
         v                         v                         v
+------------------+      +------------------+      +------------------+
|  Rendu Graphique |      |   Export MIDI    |      | Export MusicXML  |
|  (UI Renderer)   |      |  (Audio Player)  |      |   (Éditeurs)     |
+------------------+      +------------------+      +------------------+

```

### 3.1 Stratégie de Stockage Hybride

1. **Format d'Échange Public (`.solfa.json`) :** JSON structuré, hautement lisible, optimisé pour l'inspection humaine et le contrôle de version sous Git.

2. **Format de Stockage Application / Mobile :** Encodage binaire direct via **MessagePack** ou **Protobuf** pour éliminer le surcoût de parsing textuel.

3. **Format Backend Database :** Colonnes `JSONB` native sous **PostgreSQL**, permettant d'indexer et de requêter directement les éléments internes de la partition via SQL.

## 4. Spécification Complète du Schéma JSON Pivot

Le format d'échange officiel est structuré selon le schéma JSON Schema ci-dessous.

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "SolfaScorePivot",
  "type": "object",
  "required": ["metadata", "content"],
  "properties": {
    "metadata": {
      "type": "object",
      "required": ["title", "key", "time_signature", "tempo", "voices_config"],
      "properties": {
        "title": { "type": "string" },
        "subtitle": { "type": "string" },
        "composer": { "type": "string" },
        "arranger": { "type": "string" },
        "lyricist": { "type": "string" },
        "key": { 
          "type": "string",
          "pattern": "^[A-G](b|#)?(m|min|minor)?$"
        },
        "time_signature": { 
          "type": "string",
          "pattern": "^[0-9]+/[0-9]+$"
        },
        "tempo": { "type": "integer", "minimum": 20, "maximum": 300 },
        "voices_config": {
          "type": "array",
          "items": {
            "type": "object",
            "required": ["id", "name", "clef", "octave_shift", "display_order"],
            "properties": {
              "id": { "type": "string" },
              "name": { "type": "string" },
              "clef": { 
                "type": "string", 
                "enum": ["treble", "bass", "alto", "tenor"] 
              },
              "octave_shift": { "type": "integer", "default": 0 },
              "display_order": { "type": "integer" }
            }
          }
        }
      }
    },
    "content": {
      "type": "object",
      "required": ["voices"],
      "properties": {
        "voices": {
          "type": "array",
          "items": { "$ref": "#/definitions/Voice" }
        }
      }
    }
  },
  "definitions": {
    "Voice": {
      "type": "object",
      "required": ["id", "name", "clef", "octave_shift", "measures"],
      "properties": {
        "id": { "type": "string" },
        "name": { "type": "string" },
        "clef": { "type": "string", "enum": ["treble", "bass", "alto", "tenor"] },
        "octave_shift": { "type": "integer", "default": 0 },
        "measures": {
          "type": "array",
          "items": { "$ref": "#/definitions/Measure" }
        }
      }
    },
    "Measure": {
      "type": "object",
      "required": ["number", "total_duration", "events"],
      "properties": {
        "number": { "type": "integer", "minimum": 0 },
        "is_pickup": { "type": "boolean", "default": false },
        "total_duration": { "type": "number", "minimum": 0 },
        "left_barline": { 
          "type": "string", 
          "enum": ["standard", "double", "repeat_start"], 
          "default": "standard" 
        },
        "right_barline": { 
          "type": "string", 
          "enum": ["standard", "double", "repeat_end", "final"], 
          "default": "standard" 
        },
        "ending": { "type": "integer" },
        "directions": {
          "type": "array",
          "items": { "$ref": "#/definitions/Direction" }
        },
        "events": {
          "type": "array",
          "items": { "$ref": "#/definitions/Event" }
        }
      }
    },
    "Direction": {
      "type": "object",
      "required": ["time_in_measure", "type", "value"],
      "properties": {
        "time_in_measure": { "type": "number", "minimum": 0 },
        "type": { "type": "string", "enum": ["dynamic", "tempo_modifier", "text"] },
        "value": { "type": "string" }
      }
    },
    "Event": {
      "type": "object",
      "required": ["type", "time_in_measure", "duration"],
      "properties": {
        "type": { "type": "string", "enum": ["note", "rest"] },
        "time_in_measure": { "type": "number", "minimum": 0 },
        "duration": { "type": "number", "minimum": 0 },
        "note": { "type": "integer", "minimum": 0, "maximum": 127 },
        "syllabe": { "type": "string" },
        "lyric_part": { "type": "string" },
        "articulations": {
          "type": "array",
          "items": { 
            "type": "string", 
            "enum": ["accent", "staccato", "fermata", "tenuto"] 
          }
        }
      }
    }
  }
}
```

## 5. Exemple Concret d'Instance JSON Validée

Voici une instance type avec la configuration personnalisée des voix SATB (Soprano et Alto en Clef de Sol / Octave 0, Ténor et Basse en Clef de Fa / Octave -1) :

```json
{
  "metadata": {
    "title": "Faneva ESPA",
    "composer": "A. Raolijaona",
    "arranger": "Tsiky Ny Antsa",
    "key": "Eb",
    "time_signature": "4/4",
    "tempo": 125,
    "voices_config": [
      { "id": "S", "name": "Soprano", "clef": "treble", "octave_shift": 0, "display_order": 1 },
      { "id": "A", "name": "Alto", "clef": "treble", "octave_shift": 0, "display_order": 2 },
      { "id": "T", "name": "Tenor", "clef": "bass", "octave_shift": -1, "display_order": 3 },
      { "id": "B", "name": "Basse", "clef": "bass", "octave_shift": -1, "display_order": 4 }
    ]
  },
  "content": {
    "voices": [
      {
        "id": "S",
        "name": "Soprano",
        "clef": "treble",
        "octave_shift": 0,
        "measures": [
          {
            "number": 0,
            "is_pickup": true,
            "total_duration": 0.5,
            "left_barline": "standard",
            "right_barline": "standard",
            "directions": [],
            "events": [
              {
                "type": "note",
                "time_in_measure": 0.0,
                "note": 58,
                "duration": 0.5,
                "syllabe": "Sol",
                "lyric_part": "Amp-"
              }
            ]
          },
          {
            "number": 1,
            "is_pickup": false,
            "total_duration": 4.0,
            "left_barline": "standard",
            "right_barline": "standard",
            "directions": [
              {
                "time_in_measure": 0.0,
                "type": "dynamic",
                "value": "mf"
              }
            ],
            "events": [
              {
                "type": "note",
                "time_in_measure": 0.0,
                "note": 63,
                "duration": 1.0,
                "syllabe": "Do",
                "lyric_part": "i-"
              },
              {
                "type": "note",
                "time_in_measure": 1.0,
                "note": 63,
                "duration": 0.5,
                "syllabe": "Do",
                "articulations": ["accent"],
                "lyric_part": "di-"
              },
              {
                "type": "rest",
                "time_in_measure": 3.5,
                "duration": 0.5
              }
            ]
          }
        ]
      },
      {
        "id": "T",
        "name": "Tenor",
        "clef": "bass",
        "octave_shift": -1,
        "measures": [
          {
            "number": 0,
            "is_pickup": true,
            "total_duration": 0.5,
            "left_barline": "standard",
            "right_barline": "standard",
            "directions": [],
            "events": [
              {
                "type": "note",
                "time_in_measure": 0.0,
                "note": 46,
                "duration": 0.5,
                "syllabe": "Sol",
                "lyric_part": "Amp-"
              }
            ]
          }
        ]
      }
    ]
  }
}
```

## 6. Prochaines Étapes d'Implémentation

1. **Implémentation du Modèle de Données** (Classes/Interfaces dans la technologie hôte avec prise en compte de `clef` et `octave_shift`).

2. **Développement du Calculateur Temporel et MIDI** (Calcul automatique des notes MIDI absolues en combinant la tonalité globale et `octave_shift`).

3. **Module de Rendu Texte** (Génération dynamique de chaînes Solfa visuelles selon l'ordre d'affichage des voix).

4. **Module d'Exportation MIDI/MusicXML**.