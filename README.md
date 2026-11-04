# MireDo — Conception

> **MireDo** est un projet en cours de conception autour de la notation musicale Tonic Sol-fa.
> Ce dépôt est le carnet de conception vivant du projet : il rassemble les décisions validées,
> les hypothèses, les questions ouvertes et les spécifications progressivement stabilisées.

## État du projet

**Statut :** Conception en cours

La conception avance par domaines. Une règle discutée n'est pas automatiquement une règle définitive :
chaque document doit distinguer les éléments **validés**, **provisoires** et **à clarifier**.

## Démarrer dans le vault

- [[01 - Vision/00 - Vue d'ensemble|Vue d'ensemble du projet]]
- [[01 - Vision/01 - Périmètre de conception|Périmètre et méthode de conception]]
- [[02 - Notation Tonic Sol-fa/00 - Index de la notation|Notation Tonic Sol-fa]]
- [[04 - Architecture/00 - Index de l'architecture|Architecture et formats de fichier]]
- [[03 - Suivi de conception/Journal des décisions|Journal des décisions]]
- [[03 - Suivi de conception/Questions ouvertes|Questions ouvertes]]
- [[99 - Archives/Index des archives|Archives des premières conceptions]]

## Organisation du dépôt

| Dossier | Rôle |
|---|---|
| `01 - Vision/` | Vision, objectifs et périmètre de MireDo |
| `02 - Notation Tonic Sol-fa/` | Règles musicales et représentation des notes |
| `03 - Suivi de conception/` | Décisions, questions ouvertes et historique |
| `04 - Architecture/` | Architecture logicielle et formats ; dossier initial du format MireDo ouvert |
| `05 - Modèle de données/` | Modèles internes et formats d'échange — à alimenter |
| `06 - Références/` | Sources, conventions et documents de référence — à alimenter |
| `99 - Archives/` | Anciennes versions et documents conservés comme historique |

## État des domaines

| Domaine | État | Document |
|---|---|---|
| Hauteur et degrés Tonic Sol-fa | Règles de base définies | [[02 - Notation Tonic Sol-fa/01 - Hauteur et degrés]] |
| Représentation numérique des hauteurs | Axe entier ℤ et références de portée validés | [[02 - Notation Tonic Sol-fa/05 - Représentation numérique des hauteurs]] |
| Altérations chromatiques | Règles partielles validées | [[02 - Notation Tonic Sol-fa/02 - Altérations chromatiques]] |
| Octaves | Convention numérique définie, rendu à préciser | [[02 - Notation Tonic Sol-fa/03 - Octaves et représentation]] |
| Référence tonale et mode majeur/mineur | Principe de dépendance à la partition validé | [[02 - Notation Tonic Sol-fa/04 - Référence tonale et mode]] |
| Architecture et SDK | À reprendre après stabilisation des règles musicales | — |
| Format natif `.mrd` | Dossier de conception initial créé ; JSON étudié, schéma non validé | [[04 - Architecture/Format de fichier MireDo/00 - Index]] |

## Principes de travail

1. **Ne pas confondre conception initiale et spécification validée.** Les premiers documents sont conservés dans les archives.
2. **Ne pas inventer de conventions.** Une règle non confirmée est marquée comme question ouverte.
3. **Séparer la notation écrite de la hauteur sonore calculée.** Une équivalence de hauteur ne doit pas effacer une orthographe Sol-fa.
4. **Concevoir par domaine.** La hauteur et la notation sont étudiées indépendamment du rythme, des clefs et du rendu complet.
5. **Garder une trace des décisions.** Toute modification importante est ajoutée au journal.

## Convention de statut

- **Validé** — Décision explicitement confirmée.
- **Provisoire** — Proposition de travail non définitivement arrêtée.
- **À clarifier** — Information insuffisante ou question en attente.
- **À concevoir** — Sujet identifié, pas encore spécifié.

## Historique récent

- **2026-11-03** — Création de la structure documentaire Obsidian et séparation de la première conception historique.
- **2026-11-03** — Formalisation initiale des conventions Tonic Sol-fa : degrés, altérations, octaves et référence tonale.
- **2026-11-04** — Validation des règles de crochet, de barre initiale, de séparateur conservé et de barre de fermeture des systèmes.
- **2026-11-04** — Validation de l'axe chromatique entier ℤ, de la conversion des graphies par l'éditeur et des références numériques de portée par voix.
- **2026-11-04** — Ouverture du dossier de conception du format natif MireDo ; analyse d'une proposition JSON et définition d'un premier modèle logique provisoire.

## Comment contribuer à la conception

Lorsqu'une nouvelle règle est discutée :

1. Identifier le domaine concerné.
2. Mettre à jour le document de référence correspondant.
3. Ajouter une entrée au [[03 - Suivi de conception/Journal des décisions|journal des décisions]] si une règle est confirmée.
4. Ajouter une entrée dans [[03 - Suivi de conception/Questions ouvertes|questions ouvertes]] si un point reste à trancher.
5. Mettre à jour ce README lorsque l'état global ou l'organisation évolue.

---

**Nom du projet :** MireDo  
**Extension native envisagée :** `.mrd`  
**Nature du dépôt :** documentation de conception compatible Obsidian  
**Statut :** conception évolutive, non figée
