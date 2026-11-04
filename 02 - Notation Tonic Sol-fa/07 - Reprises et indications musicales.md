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

Leur syntaxe de saisie, leurs paramètres éventuels (par exemple une valeur de tempo) et les détails de leur rendu restent à spécifier dans la conception.

## 6. Points restant à préciser

- La graphie exacte des instructions D.C. et D.S. dans la syntaxe Tonic Sol-fa de MireDo.
- La forme de saisie et de rendu des repères Segno identifiés (`S_1`, `S_2`, etc.).
- La syntaxe exacte des indications Fine, Coda et To Coda.
- Les règles de parcours en présence de plusieurs retours, fins ou Coda.
- La représentation détaillée des nuances, indications de tempo, articulations et points d'orgue.
- Les paramètres et effets précis de ces indications sur la lecture sonore et les exports.

Aucune syntaxe non validée ne doit être présentée comme une convention Tonic Sol-fa officielle.
