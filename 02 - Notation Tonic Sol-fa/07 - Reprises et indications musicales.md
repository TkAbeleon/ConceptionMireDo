# Reprises et indications musicales — Tonic Sol-fa

Cette page consigne les conventions de reprise et les indications musicales à prendre en charge dans MireDo. **Leur signification et leur comportement musical restent les mêmes qu'en solfège et en notation musicale habituelle.** MireDo ne doit pas inventer de nouvelles règles musicales : il doit prendre en charge ces conventions et les représenter fidèlement. Seule la manière de noter certaines reprises peut différer en Tonic Sol-fa, notamment par l'emploi d'indications textuelles comme D.C. et D.S. plutôt que par les barres de reprise classiques.

## 1. Répétitions et reprises en Tonic Sol-fa

La notation Tonic Sol-fa concernée ici utilise des indications textuelles de renvoi pour exprimer les reprises. Elle ne repose pas, par défaut, sur les barres de reprise graphiques utilisées dans la notation musicale classique.

MireDo doit donc distinguer :
- les barres de mesure et les doubles barres, qui conservent leurs fonctions propres ;
- les instructions de reprise, qui déterminent un retour ou un saut dans le déroulement musical.

Les barres de reprise classiques ne doivent pas être ajoutées automatiquement comme mécanisme de répétition par défaut pour cette notation Sol-fa.

## 2. Instructions de retour

### Da Capo : D.C.

`D.C.` signifie *Da Capo* : reprendre depuis le début du morceau ou de la partition, selon le contexte musical défini.

### Dal Segno : D.S.

`D.S.` signifie *Dal Segno* : revenir au signe Segno placé à un endroit précis de la partition.

La notation de conception utilise des repères identifiables, par exemple `S_1`, `S_2`, etc. Une instruction telle que `D.S._1` désigne le retour au repère `S_1`.

Le signe graphique traditionnel du Segno peut être représenté dans la partition ; les identifiants `S_1`, `S_2`, etc. permettent de distinguer plusieurs repères dans le modèle et dans la syntaxe de MireDo.

La graphie exacte de saisie de ces instructions reste à confirmer. Les formes ci-dessus décrivent leur sens et leur association, sans imposer définitivement une grammaire.

## 3. Fins et sauts conditionnels

MireDo doit également prendre en charge les indications complémentaires utilisées avec les retours :

- **Fine** : marque le point auquel l'exécution doit se terminer lorsqu'une instruction de reprise demande de s'arrêter à Fine.
- **Coda** : identifie le passage final vers lequel l'exécution peut être dirigée.
- **To Coda** : indique le point à partir duquel l'exécution doit sauter vers la Coda, lorsque l'instruction de reprise le prévoit.

Combinaisons musicales à prendre en charge :
- `D.C. al Fine` : retour au début, puis arrêt à Fine.
- `D.S. al Fine` : retour au Segno, puis arrêt à Fine.
- `D.S. al Coda` : retour au Segno, puis saut vers la Coda au point indiqué.

Ces indications ne sont pas de simples éléments décoratifs : elles participent à la logique de parcours et d'exécution de la partition.

## 4. Modélisation du parcours musical

Le modèle de MireDo devra pouvoir représenter :
- plusieurs repères Segno distincts, chacun doté d'un identifiant ;
- une instruction de retour associée à un repère précis ;
- les points Fine et Coda ;
- les instructions To Coda ;
- les conditions de déclenchement et l'ordre des sauts au cours de l'exécution.

Le moteur de lecture devra interpréter ces indications sans confondre l'ordre de lecture avec l'ordre linéaire des mesures dans le document.

Les règles détaillées de parcours, notamment en présence de plusieurs retours ou de plusieurs Coda, restent à spécifier. Elles devront respecter les conventions habituelles du solfège ; le travail restant porte sur leur représentation et leur interprétation dans MireDo, pas sur la redéfinition de leur sens musical.

## 5. Nuances, tempo et indications d'exécution

Les nuances, les indications de tempo, les changements de tempo, les articulations, le point d'orgue et les autres indications d'exécution conservent exactement les mêmes significations, règles et comportements qu'en solfège et en notation musicale habituelle. Leur utilisation en Tonic Sol-fa ne change pas leur principe musical. MireDo ne doit pas leur attribuer une sémantique musicale nouvelle.

Cela inclut explicitement les articulations classiques — staccato, legato, accent, tenuto et autres indications équivalentes. Elles sont prises en charge selon les conventions habituelles du solfège, sans qu'il soit nécessaire de définir une règle musicale spécifique à MireDo. La conception de MireDo porte sur leur représentation, leur édition et leur rendu, non sur la réinvention de leur signification.

Exemples d'indications à prendre en charge :

- **Nuances** : piano, forte, pianissimo, fortissimo, crescendo, diminuendo, etc.
- **Changements de tempo** : accelerando, ritardando, rallentando, a tempo, etc.
- **Indications d'exécution** : ritenuto, rubato et autres indications usuelles.
- **Prolongation et expression** : point d'orgue.
- **Articulations** : staccato, legato, accents et autres signes usuels.

MireDo doit pouvoir conserver ces indications dans son modèle musical, les afficher conformément aux conventions graphiques et les transmettre au moteur de lecture ou aux exports lorsqu'une interprétation sonore est prévue.

Les ornements, les trémolos, les répétitions rapides ainsi que les notes de grâce (notamment appoggiatures et acciaccaturas) relèvent du même principe : leur signification, leur durée, leur placement et leur comportement suivent les conventions classiques du solfège. Leur usage en Tonic Sol-fa peut être rare ; il n'est donc pas nécessaire de fixer ici une syntaxe Sol-fa détaillée. Leur traitement technique (saisie, édition, représentation et interprétation) sera précisé ultérieurement dans la conception de MireDo.

Leur syntaxe de saisie, leurs paramètres éventuels (par exemple une valeur de tempo) et les détails de leur rendu restent à spécifier dans la conception.

## 6. Organisation des informations supplémentaires dans MireDo

### 6.1 Catégorie générale

**Décision validée :** dans l'interface de MireDo, ces éléments sont regroupés sous une catégorie générale unique intitulée **Informations supplémentaires**.

Les familles ci-dessous servent à organiser les éléments à l'intérieur de cette catégorie. Elles ne deviennent pas chacune une catégorie principale indépendante.

### 6.2 Principe de référence

**Décision validée :** MireDo reprend les conventions musicales établies en solfège et en notation musicale classique. Il n'est pas nécessaire de redéfinir ces règles pour Tonic Sol-fa.

**Décision validée :** pour la saisie, l'édition, l'organisation des palettes, les propriétés, le placement et le rendu, MireDo reproduit le fonctionnement des logiciels de notation de référence, en prenant notamment MuseScore comme référence principale et les autres logiciels reconnus comme références complémentaires.

Cela signifie que MireDo doit reprendre les familles d'éléments et leurs comportements usuels, plutôt que concevoir une organisation ou une sémantique musicale nouvelle. Les détails propres à l'interface de MireDo pourront être adaptés, sans modifier le sens musical conventionnel des indications.

### 6.3 Familles d'informations supplémentaires

Le regroupement couvre notamment les familles suivantes, conformément aux fonctions proposées par les logiciels de notation de référence :

- **Nuances et dynamique :** piano, forte, pianissimo, fortissimo, mezzo-piano, mezzo-forte et autres niveaux dynamiques.
- **Évolutions de dynamique :** crescendo, diminuendo et leurs représentations progressives.
- **Tempo et indications de mouvement :** indication métronomique, changements de tempo, accelerando, ritardando, rallentando, a tempo, ritenuto, rubato, etc.
- **Articulations et accents :** staccato, staccatissimo, legato, accent, marcato, tenuto et autres signes conventionnels.
- **Ornements :** trilles, mordants, gruppettos et autres ornements.
- **Notes de grâce :** appoggiatures, acciaccaturas et autres notes d'ornement.
- **Trémolos et répétitions rapides :** signes et indications conventionnels correspondants.
- **Arpèges et glissandos :** indications de jeu et de liaison entre hauteurs.
- **Pauses et respirations :** point d'orgue, césure, respiration et indications apparentées.
- **Liaisons et lignes musicales :** liaison d'expression, liaison de prolongation, lignes d'octave, lignes de pédale, soufflets et autres lignes à portée définie.
- **Techniques de jeu :** indications propres à l'exécution instrumentale ou vocale, selon les conventions du logiciel de référence.
- **Reprises et navigation :** D.C., D.S., Segno, Fine, Coda, To Coda, fins alternatives et autres repères de parcours.
- **Repères et textes musicaux :** lettres de répétition, repères de répétition, textes attachés à une portée ou à un système et indications éditoriales musicales.
- **Symboles harmoniques :** chiffrages et symboles d'accords, lorsqu'ils sont proposés dans l'organisation des éléments de notation.

Cette liste constitue le périmètre fonctionnel des familles à prendre en charge. Elle ne fixe pas encore l'inventaire exhaustif de chaque symbole, de chaque variante ou de chaque propriété.

### 6.4 Niveaux d'association dans la partition

**Décision validée :** pour une indication ponctuelle, l'unité musicale constitue le niveau de précision maximal d'association dans le modèle de MireDo. Une indication ponctuelle est donc rattachée à l'unité concernée, même si un logiciel de notation classique peut proposer un ancrage plus fin à une note.

Les indications dont le fonctionnement conventionnel porte sur une durée ou un passage doivent toutefois conserver leur étendue : par exemple, un crescendo ou une ligne musicale possède un début et une fin. Les repères de reprise et de navigation doivent être associés aux éléments structurels concernés.

Ces associations permettent de conserver le comportement musical attendu sans réduire une indication étendue ou structurelle à un simple événement ponctuel.

### 6.5 Comportement et rendu

MireDo reprend, pour chaque famille, les comportements conventionnels des logiciels de référence :

- ajout depuis une palette ou un mécanisme de saisie équivalent ;
- association à l'unité, à une étendue ou à un repère structurel selon la nature de l'indication ;
- modification et suppression de l'indication ;
- affichage du symbole, du texte ou de la ligne conformément aux conventions graphiques ;
- conservation de ses paramètres lorsqu'elle en possède ;
- effet sur la lecture sonore lorsqu'il s'agit d'une indication ayant un effet d'interprétation ;
- prise en compte dans les exports qui prennent en charge l'information concernée.

Une indication visuelle et son effet musical ne doivent pas être confondus : un texte simplement affiché ne doit pas produire automatiquement un effet sonore si, dans le logiciel de référence, il s'agit d'un texte sans fonction d'interprétation.

### 6.6 Limites de cette décision

Les décisions ci-dessus valident l'organisation générale, les familles fonctionnelles, le principe de reprise des conventions existantes et les niveaux généraux d'association. Elles ne définissent pas encore :

- le catalogue exhaustif des symboles et variantes ;
- les palettes et leur organisation détaillée dans l'interface ;
- les propriétés et paramètres précis de chaque élément ;
- les règles techniques de stockage dans le fichier `.mrd` ;
- les détails de placement, de collision et de rendu ;
- les paramètres exacts de lecture sonore et les limites de chaque export.

Ces points seront conçus en s'appuyant sur les logiciels de référence, sans réinventer les conventions musicales.

## 7. Points restant à préciser

- La graphie exacte des instructions D.C. et D.S. dans la syntaxe Tonic Sol-fa de MireDo.
- La forme de saisie et de rendu des repères Segno identifiés (`S_1`, `S_2`, etc.).
- La syntaxe exacte des indications Fine, Coda et To Coda.
- Les règles de parcours en présence de plusieurs retours, fins ou Coda.
- La représentation détaillée des nuances, indications de tempo, articulations et points d'orgue.
- Les paramètres et effets précis de ces indications sur la lecture sonore et les exports.

Aucune syntaxe non validée ne doit être présentée comme une convention Tonic Sol-fa officielle.

## 8. Clôture du cadrage fonctionnel

**Statut : cadrage fonctionnel général validé et clôturé le 2026-11-06.**

Les décisions suivantes sont considérées comme acquises pour la conception de MireDo :

- toutes les indications concernées sont regroupées dans la catégorie générale « Informations supplémentaires » ;
- les familles fonctionnelles recensées dans la section 6.3 constituent le périmètre de référence ;
- leur sens et leur comportement musical suivent les conventions du solfège et des logiciels de notation de référence ; MireDo ne crée pas de règles musicales nouvelles ;
- MuseScore est la référence principale pour reprendre l'organisation et le fonctionnement des outils, avec les autres logiciels reconnus comme références complémentaires ;
- une indication ponctuelle est associée au niveau de l'unité musicale ; une indication étendue conserve son début et sa fin ; une indication de navigation ou de reprise conserve ses repères structurels ;
- la représentation graphique, l'édition et l'effet sur la lecture sont traités conformément au type d'indication et aux conventions des logiciels de référence.

**La discussion sur le cadrage fonctionnel général des informations supplémentaires est donc clôturée.** Les travaux ultérieurs porteront uniquement sur les détails nécessaires à leur réalisation : inventaire précis des symboles, propriétés, interface, stockage, placement graphique, lecture sonore et exports. Ces travaux ne doivent pas rouvrir les décisions fonctionnelles ci-dessus sans nouvelle demande explicite.
