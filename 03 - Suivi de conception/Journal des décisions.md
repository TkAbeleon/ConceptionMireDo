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


## 2026-11-04 — Portée des courbes de groupement rythmique

- **Décision :** une courbe de groupement couvre l'intégralité du fragment de notation Sol-fa auquel elle s'applique.
- **Précision :** la courbe englobe également les signes de prolongation présents dans ce fragment ; elle ne s'arrête pas aux seules attaques des notes.
- **Précision :** cette même règle de portée s'applique aux courbes des triolets, sextolets et autres groupes concernés.
- **Précision :** les parenthèses dans les exemples explicatifs servent uniquement à matérialiser le fragment couvert. Elles ne font pas partie de la syntaxe Sol-fa.
- **Exemples :** `(d.-.d)` indique que la courbe couvre tout `d.-.d`, prolongation comprise ; `(d.d.d)` indique que la courbe couvre les trois notes.
- **Périmètre :** cette décision fixe la portée graphique de la courbe, sans prétendre définir la syntaxe ni le calcul temporel des groupes non binaires.
- **Statut :** confirmé par l'utilisateur.


## 2026-11-04 — Durée des triolets et sextolets

- **Décision :** un triolet répartit une unité native Sol-fa complète en trois positions égales.
- **Décision :** un sextolet répartit une unité native Sol-fa complète en six positions égales.
- **Précision :** le groupe ne change pas la durée de l'unité native ; il en répartit les positions internes.
- **Précision :** une position occupée par `-` prolonge la note précédente. Elle compte comme une position du groupe, sans produire une nouvelle attaque.
- **Précision :** la courbe de groupement couvre le fragment complet, prolongations comprises.
- **Statut :** confirmé par l'utilisateur.


## 2026-11-06 — Positions temporelles et divisions de l'unité

- **Décision :** les événements d'une unité native sont repérés par leur position de début, exprimée comme une fraction exacte de cette unité.
- **Décision :** le dénominateur est un entier positif libre N ; aucune liste fermée de dénominateurs n'est imposée. Le modèle peut représenter une division en N parts égales pour tout entier positif.
- **Décision :** pour une division égale en N positions, les débuts sont 0/N, 1/N, ..., (N-1)/N. Ainsi, un triolet utilise 0/3, 1/3, 2/3, et une division en cinq utilise 0/5, 1/5, 2/5, 3/5, 4/5.
- **Précision :** en 4/4, une unité native correspond à une noire ; une division en N partage donc cette noire en N durées égales.
- **Décision :** une unité peut également contenir des segments de durées inégales. Les positions utilisent alors un dénominateur commun permettant de représenter exactement tous les débuts d'événements ; la durée est calculée jusqu'à la position suivante ou jusqu'à la fin de l'unité.
- **Précision :** le dénominateur commun est conservé comme information de division ; 0/3 n'est pas normalisé en 0/1.
- **Précision :** cette liberté appartient au modèle temporel interne de MireDo. Elle ne crée pas automatiquement une syntaxe Tonic Sol-fa pour les divisions dont les conventions de notation source ne sont pas encore documentées.
- **Statut :** modèle temporel validé par l'utilisateur ; la syntaxe de notation source pour les divisions non documentées reste ouverte.

## 2026-11-06 — Organisation des informations supplémentaires

- **Décision :** regrouper les indications musicales complémentaires dans une catégorie générale unique intitulée « Informations supplémentaires » dans MireDo.
- **Décision :** organiser les éléments de cette catégorie en familles fonctionnelles, sans transformer chaque famille en catégorie principale indépendante.
- **Décision :** reprendre les conventions musicales du solfège et de la notation classique ; MireDo ne redéfinit pas leur signification ni leur comportement musical.
- **Décision :** prendre les logiciels de notation reconnus comme références pour l'organisation des palettes, la saisie, l'édition, les propriétés, le placement, le rendu et les effets de lecture. MuseScore constitue la référence principale évoquée.
- **Décision :** pour une indication ponctuelle, l'unité musicale est le niveau de précision maximal de son association dans le modèle MireDo.
- **Précision :** les indications étendues conservent leur début et leur fin ; les indications de reprise et de navigation conservent leurs repères structurels.
- **Précision :** les familles concernées comprennent notamment les nuances et évolutions dynamiques, le tempo et ses évolutions, les articulations, les ornements, les notes de grâce, les trémolos, les arpèges et glissandos, les pauses et respirations, les liaisons et lignes musicales, les techniques de jeu, les reprises et repères de navigation, les textes et repères musicaux ainsi que les symboles harmoniques.
- **Périmètre non fixé :** le catalogue exhaustif, les propriétés de chaque élément, les détails d'interface, le stockage dans le fichier `.mrd`, le placement graphique et les paramètres de lecture/export restent à concevoir à partir des logiciels de référence.
- **Statut :** principes généraux et organisation validés par l'utilisateur ; détails techniques et inventaire exhaustif non définis.

## 2026-11-06 — Clôture du cadrage fonctionnel des informations supplémentaires

- **Décision :** le cadrage fonctionnel général des informations supplémentaires est clôturé.
- **Décisions maintenues :** catégorie générale unique ; familles fonctionnelles recensées ; reprise des conventions musicales et des comportements des logiciels de référence ; MuseScore comme référence principale ; association ponctuelle au niveau de l'unité, étendue conservée pour les indications de durée et repères structurels conservés pour la navigation.
- **Précision :** la clôture concerne les principes fonctionnels généraux. Elle ne signifie pas que chaque symbole, propriété ou détail technique a déjà été spécifié.
- **Travaux ultérieurs autorisés dans ce périmètre :** préciser l'inventaire des éléments, leurs propriétés, leur interface, leur stockage, leur rendu, leur lecture sonore et leur prise en charge par les exports, en appliquant les décisions validées.
- **Règle de continuité :** ces travaux techniques ne rouvrent pas les décisions fonctionnelles clôturées, sauf demande explicite de révision.
- **Statut :** cadrage fonctionnel clôturé par l'utilisateur.
