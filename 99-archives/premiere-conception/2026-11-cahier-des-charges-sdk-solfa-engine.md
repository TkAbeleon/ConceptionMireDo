# Première conception — SDK Solfa Engine

> **Document historique — novembre 2026**
>
> Ce document résume la première proposition de conception technique du projet, initialement enregistrée à la racine sous le nom `sp_cifications_techniques_et_cahier_des_charges.md`.
> Il est conservé comme trace historique et ne constitue pas la spécification actuelle de MireDo.

## 1. Intention initiale

La première proposition envisageait un SDK open source, modulaire et performant pour analyser, convertir, stocker et générer de la musique écrite en Tonic Sol-fa.

Le moteur devait isoler la sémantique musicale des représentations visuelles et audio.

## 2. Objectifs envisagés

- Parser des chaînes Tonic Sol-fa et des formats structurés.
- Définir un format pivot JSON, puis une représentation binaire éventuelle (MessagePack ou Protobuf).
- Gérer le temps musical, les mesures et les anacrouses.
- Gérer plusieurs voix, notamment des configurations SATB ou personnalisées.
- Calculer des hauteurs MIDI selon un contexte tonal.
- Transposer les partitions.
- Aligner les paroles avec les événements musicaux.
- Exporter vers MIDI, MusicXML, JSON et formats binaires.
- Préserver l'indépendance du moteur vis-à-vis des frameworks graphiques.

## 3. Architecture envisagée

Le schéma initial séparait :
1. les sources textuelles, binaires et les bases de données ;
2. un moteur central (parser, sérialiseur, calcul temporel et MIDI) ;
3. les sorties graphiques, MIDI et MusicXML.

## 4. Modèle de données envisagé

La proposition utilisait un objet pivot avec :
- des métadonnées de partition ;
- une configuration des voix ;
- des voix contenant des mesures ;
- des mesures contenant des directions et des événements ;
- des événements de type note ou silence, avec position, durée, hauteur MIDI éventuelle, paroles et articulations.

Le document initial contenait également un exemple JSON de partition chorale SATB.

## 5. Pistes techniques évoquées

- Python / TypeScript et modèles typés ;
- JSON lisible pour l'échange ;
- MessagePack ou Protobuf pour le stockage binaire ;
- PostgreSQL JSONB pour le stockage backend ;
- export MIDI et MusicXML.

## 6. Pourquoi ce document est archivé

Cette première proposition mélangeait plusieurs domaines : notation, hauteur, rythme, clefs, voix, stockage, architecture et export.

La conception actuelle de MireDo reprend ces sujets progressivement. Les éléments de cette première proposition ne sont donc pas automatiquement validés. Ils doivent être réexaminés et intégrés uniquement après discussion.

Pour connaître les décisions actuelles, consulter le [[../../README|README MireDo]] et les documents du vault.
