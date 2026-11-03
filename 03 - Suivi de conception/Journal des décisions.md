# Journal des décisions

Ce journal conserve les décisions de conception confirmées. Les propositions non confirmées sont consignées dans [[Questions ouvertes]].

## 2026-11-03 — Identité du projet

- **Décision :** le projet porte le nom MireDo.
- **Décision :** l'extension native envisagée est `.mrd`.
- **Statut :** validé par l'utilisateur.

## 2026-11-03 — Alphabet fondamental Tonic Sol-fa

- **Décision :** utiliser la convention anglicisée `d r m f s l t`.
- **Statut :** validé.

## 2026-11-03 — Altération ascendante

- **Décision :** ajouter `i` au degré pour indiquer une élévation d'un demi-ton (ex. `d → di`, `f → fi`).
- **Statut :** validé.

## 2026-11-03 — Altération descendante

- **Décision :** employer une voyelle parmi `a`, `e`, `o` selon la syllabe et l'usage.
- **Précision :** `te`, `ta`, `to` sont des variantes possibles pour le degré `t` abaissé.
- **Statut :** principe validé ; table complète non définie.

## 2026-11-03 — Pas de signe autonome de bécarre

- **Décision :** ne pas introduire de symbole séparé de bécarre dans la notation Sol-fa décrite.
- **Statut :** validé.

## 2026-11-03 — Déplacement d'octave numérique

- **Décision :** les exemples `d1`, `d2`, `d_1`, `s_2`, `di_1` et `di1` expriment respectivement les déplacements d'octave indiqués dans la note dédiée.
- **Décision :** appliquer aussi cette syntaxe aux syllabes altérées.
- **Décision :** une note sans suffixe (ex. `d`) se trouve dans l'octave de référence ; `d1` indique un déplacement d'une octave vers l'aigu, `d2` de deux octaves vers l'aigu et `d_1` d'une octave vers le grave.
- **Précision :** cette référence est implicite dans l'écriture. Sa correspondance avec une hauteur absolue reste à déterminer dans le contexte musical.
- **Statut :** validé.

## 2026-11-03 — Désignation de la tonalité de référence

- **Décision :** désigner la tonalité de référence avec les lettres latines usuelles `A B C D E F G`.
- **Décision :** les altérations de la référence peuvent être indiquées avec `b` ou `#`.
- **Préférence par défaut :** privilégier le bémol (`b`) lorsqu'un choix d'orthographe est nécessaire.
- **Exemple :** avec la référence `Ab`, le degré Sol-fa `d` correspond à La bémol.
- **Statut :** validé.

## 2026-11-03 — Liberté du compositeur sur la gamme et le centre tonal

- **Décision :** la tonalité de référence déclarée ne détermine pas à elle seule la gamme ni le mode du morceau.
- **Décision :** le compositeur choisit librement l'organisation musicale et les syllabes Sol-fa qu'il écrit.
- **Décision :** MireDo interprète la notation selon la référence déclarée, sans déduire ni imposer automatiquement un mode majeur ou mineur.
- **Décision :** MireDo ne corrige pas une écriture jugée inhabituelle et ne demande pas au compositeur de justifier son choix de référence.
- **Exemple :** un morceau en La mineur peut être écrit avec `C` comme référence (`d = C`) et `l` comme tonique.
- **Exemple :** un morceau réellement en Ré bémol peut être écrit avec `Db` comme référence (`d d d m`) ou avec `C` comme référence et une écriture adaptée par le compositeur (`di di di f`). MireDo accepte les deux écritures.
- **Statut :** validé.

## 2026-11-03 — Conservation de l'orthographe

- **Décision :** une équivalence de hauteur sonore ne doit pas entraîner la normalisation automatique de la graphie Sol-fa.
- **Exemples :** `mi` et `f` peuvent être équivalents en hauteur sans être la même graphie ; `ti_1` ne doit pas être automatiquement remplacé par `d`.
- **Statut :** principe validé pour la conception actuelle.

## 2026-11-03 — Système de notation choisi par partition

- **Décision :** chaque partition déclare son propre système de notation.
- **Décision :** MireDo prend en charge des systèmes de notation existants et leurs règles établies ; il n'invente pas de nouvelles règles de notation.
- **Décision :** Sol-fa est le système utilisé par défaut lorsqu'aucun autre système n'est sélectionné. D'autres systèmes déjà définis, par exemple le solfège, peuvent être sélectionnés pour une partition.
- **Précision :** les règles d'un système ne doivent pas être imposées à un autre système.
- **Statut :** validé.
