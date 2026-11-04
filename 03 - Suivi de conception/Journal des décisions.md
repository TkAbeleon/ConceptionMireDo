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

## 2026-11-04 — Représentation numérique des hauteurs et références de portée

- **Décision :** les hauteurs sont représentées sur un axe chromatique entier continu, de valeurs appartenant à ℤ, sans borne théorique inférieure ni supérieure.
- **Décision :** la valeur `0` est la référence ; chaque demi-ton vers l'aigu ajoute `1` et chaque demi-ton vers le grave soustrait `1`.
- **Décision :** l'éditeur interprète les graphies Sol-fa saisies et les convertit en équivalents numériques. Le compositeur continue à saisir les graphies musicales, pas les nombres.
- **Décision :** les autres composants exploitent les valeurs numériques produites par l'éditeur au lieu de réinterpréter chacun les graphies Sol-fa.
- **Décision :** chaque voix possède une référence numérique de portée distincte de son nom et de sa tessiture. `0` correspond à la clé de Sol, `-1` à la clé de Fa ; les autres entiers suivent la même logique de position.
- **Décision :** pour SATB par défaut, S et A utilisent la référence `0`, T et B la référence `-1`.
- **Précision :** la graphie originale reste conservée séparément de l'équivalent numérique ; aucune normalisation enharmonique automatique n'est autorisée.
- **Statut :** validé par l'utilisateur.

## 2026-11-04 — Crochet et délimitation des systèmes

- **Décision :** le crochet reliant les portées est affiché par défaut ; l'utilisateur peut le masquer.
- **Décision :** lorsque le crochet est masqué et que le système commence normalement sur le premier temps, une barre verticale initiale le remplace.
- **Décision :** lorsqu'un système commence par une anacrouse ou au milieu d'une mesure, aucune barre initiale supplémentaire n'est ajoutée ; le séparateur musical correspondant est conservé.
- **Décision :** chaque ligne de système se termine toujours par une barre verticale de fermeture, y compris lorsqu'elle se termine au milieu d'une mesure.
- **Précision :** la barre de fermeture d'une ligne ne remplace pas le séparateur qui ouvre la continuité musicale au début du système suivant.
- **Statut :** validé par l'utilisateur.

## 2026-11-04 — Organisation temporelle du modèle de partition

- **Décision :** le modèle logique conserve une hiérarchie temporelle explicite : partition → mesure commune → voix dans la mesure → unité → subdivision → événement.
- **Décision :** le modèle ne réduit pas dès le départ toute la partition à une simple liste chronologique plate de notes.
- **Décision :** les durées sont représentées par des fractions exactes.
- **Décision :** les fractions de durée sont exprimées par rapport à l'unité native Tonic Sol-fa, c'est-à-dire l'unité principale délimitée par `:`, dont la valeur dépend de la signature rythmique conformément aux conventions documentées.
- **Précision :** la noire n'est pas l'unité structurelle des subdivisions Sol-fa ; elle conserve néanmoins un rôle distinct et essentiel comme référence conventionnelle du tempo.
- **Statut :** validé par l'utilisateur.

## 2026-11-04 — Référence conventionnelle du tempo

- **Décision :** les indications de tempo sont exprimées en noires par minute (♩ = valeur), conformément à la convention musicale usuelle.
- **Décision :** le contexte musical de la partition conserve le tempo initial lorsqu'il est défini.
- **Décision :** tout changement de tempo est associé à une position précise dans la chronologie commune de la partition et conserve la même référence de noire par minute.
- **Précision :** la référence de tempo en noire est indépendante de l'unité native Tonic Sol-fa utilisée pour structurer les mesures, unités et subdivisions.
- **Précision :** un changement de signature rythmique et un changement de tempo sont deux informations distinctes ; ils peuvent se produire au même emplacement, mais ne doivent pas être confondus.
- **Statut :** validé par l'utilisateur.

## 2026-11-04 — Représentation des prolongations dans le modèle

- **Décision :** une note possède une durée totale calculée qui inclut ses prolongations.
- **Décision :** les segments d'origine qui constituent cette prolongation restent également conservés dans la structure de notation.
- **Précision :** cette combinaison permet de disposer d'une durée exploitable par les calculs tout en préservant la manière dont la durée a été écrite dans la notation source.
- **Statut :** validé par l'utilisateur.

## 2026-11-04 — Périmètre du premier modèle rythmique

- **Décision :** le premier modèle se concentre sur les éléments fondamentaux du contenu rythmique : unités, subdivisions, notes, silences, groupes rythmiques et prolongations.
- **Décision :** les indications de performance et d'expression telles que D.C., D.S., nuances, crescendo/diminuendo et articulations ne sont pas intégrées à ce socle initial.
- **Précision :** le tempo fait exception à ce report : le tempo initial et ses changements font partie du contexte temporel nécessaire à l'interprétation de la partition.
- **Précision :** les autres indications pourront être conçues dans une étape ultérieure. Leur exclusion actuelle ne signifie pas qu'elles seront absentes du format natif final.
- **Statut :** périmètre de conception validé par l'utilisateur.

## 2026-11-04 — Clarification de la division binaire Tonic Sol-fa

- **Précision :** le point `.` divise une unité en deux moitiés égales.
- **Précision :** la virgule `,` subdivise en deux une moitié déjà obtenue par le point. Chaque portion ainsi obtenue vaut donc `1/4` de l'unité.
- **Précision :** la division en quatre est le résultat de deux étapes successives ; la virgule ne divise pas directement l'unité entière en quatre.
- **Exemple de référence :** `| d,d .d ,d : d.,d ! d,-.d : d.d |`. La documentation détaille les durées de chaque note, silence et prolongation dans les quatre unités.
- **Périmètre :** cette clarification porte sur la division binaire uniquement. Les divisions non binaires, notamment les triolets et sextolets, seront analysées dans une étape ultérieure et ne doivent pas être déduites de cette règle.
- **Statut :** clarification de la convention Tonic Sol-fa confirmée par l'utilisateur.

## 2026-11-04 — Répartition implicite des notes et prolongations

- **Décision :** lorsqu'une unité ne contient aucun signe de division explicite (`.` ou `,`), sa durée est répartie également entre les notes et les signes de prolongation présents.
- **Décision :** chaque note et chaque signe `-` compte comme un élément de même durée ; la somme de ces éléments remplit exactement l'unité.
- **Exemples :** `:d-d:` contient deux notes et une prolongation, soit trois éléments de `1/3` ; la première note dure `2/3` et la seconde `1/3`. `:dd-:` contient également trois éléments de `1/3` ; la première note dure `1/3` et la seconde `2/3`. `:dddd:` donne quatre notes de `1/4`, et `:ddddd:` cinq notes de `1/5`.
- **Précision :** dans cette répartition implicite, les éléments comptés remplissent toute l'unité ; elle ne permet donc pas d'insérer une portion silencieuse.
- **Orientation d'architecture :** les choix de saisie compacte/explicite et de visualisation relèvent de l'éditeur et ne doivent pas modifier la logique musicale interne. Les modalités d'interface et de stockage des préférences restent à concevoir.
- **Statut :** règle de répartition confirmée par l'utilisateur ; modalités d'interface encore à concevoir.

