# Catalogue et gestion des informations supplémentaires

Cette page détaille les familles déjà recensées et décrit leur gestion dans les logiciels de notation de référence. MuseScore Studio est la référence principale ; Dorico apporte un complément utile pour l'organisation des outils. Les comportements ci-dessous sont des observations documentées et des exigences fonctionnelles à reprendre, pas une spécification technique du format .mrd.

## 1. Principes communs

### 1.1 Organisation

Dans MireDo, tous les éléments restent regroupés dans une seule catégorie générale : **Informations supplémentaires**. Les familles servent à organiser le catalogue et les outils à l'intérieur de cette catégorie.

MuseScore utilise des palettes spécialisées (Dynamics, Tempo, Articulations, Ornaments, Repeats & jumps, etc.). Dorico utilise des panneaux spécialisés (Tempo, Dynamics, Ornaments, Repeat Structures, Holds and Pauses, Playing Techniques, Lines). MireDo reprend cette logique fonctionnelle sans multiplier les catégories principales.

### 1.2 Ne pas confondre apparence et fonction musicale

Les logiciels de référence distinguent les objets selon leur fonction, même lorsque plusieurs sont affichés sous forme de texte :

- un objet Tempo peut modifier la vitesse de lecture ;
- une nuance peut modifier l'intensité sonore ;
- un symbole d'accord peut déclencher un accompagnement ;
- une instruction D.C. ou D.S. peut modifier le parcours de lecture ;
- un texte générique peut rester une simple annotation.

MireDo doit conserver le type fonctionnel de chaque élément. Le texte affiché ne suffit pas à déterminer son effet sonore. Un texte libre « Allegro » ne devient pas automatiquement un objet Tempo interprétable.

### 1.3 Cycle de gestion

Selon la nature de l'élément, les logiciels de référence permettent de le choisir dans une palette, de l'ajouter à une sélection ou par glisser-déposer, de modifier ses propriétés, de déplacer son ancrage ou ses extrémités, de le supprimer, puis de conserver ses paramètres dans le document. MireDo doit proposer les opérations équivalentes adaptées à chaque famille.

### 1.4 Règle d'association propre à MireDo

La granularité déjà validée pour MireDo prévaut sur les détails internes des logiciels de référence :

- **Ponctuel :** association à l'unité musicale concernée. L'unité est le niveau de précision maximal dans le modèle MireDo, même si MuseScore autorise parfois un ancrage à une note ou à une position plus fine.
- **Étendu :** conservation d'un début, d'une fin et de la portée concernée.
- **Structurel :** association à une mesure, une section, un point de parcours ou un repère identifié.
- **Événement musical lié :** un élément comme une note de grâce conserve sa nature d'événement et son lien avec la note principale ; il ne devient pas une simple annotation.

---

## 2. Nuances et dynamique

**Éléments :** pp, p, mp, mf, f, ff et autres niveaux ; nuances particulières ; combinaisons symbole + texte (poco f, più p, etc.).

**Gestion dans MuseScore :** palette Dynamics ; ajout à une sélection de notes ou par glisser-déposer. Le panneau Properties expose notamment la taille, l'affectation à une voix, le placement et certains réglages d'alignement. Les nuances peuvent être combinées à un texte d'expression tout en conservant des objets fonctionnels distincts.

**À reprendre dans MireDo :** type dynamique explicite, unité d'association, portée (voix ou ensemble de voix), symbole conventionnel, propriétés de placement et effet sur la lecture lorsque pris en charge. Un texte juxtaposé ne doit pas être confondu avec la nuance.

Référence : [MuseScore — Dynamics and hairpins](https://handbook.musescore.org/notation/expressive-markings/dynamics-and-hairpins).

## 3. Évolutions progressives de dynamique

**Éléments :** crescendo, diminuendo/decrescendo, soufflets et lignes textuelles progressives.

**Gestion dans MuseScore :** ces éléments sont des lignes étendues, distinctes des nuances ponctuelles. Elles peuvent être appliquées à une note ou à une plage de notes/mesures. Leurs extrémités définissent la portée ; elles possèdent des propriétés de hauteur, d'ouverture, d'épaisseur, de placement et de lecture. Elles peuvent être reliées à une nuance cible.

**À reprendre dans MireDo :** type de progression, début, fin, portée concernée, représentation (soufflet ou ligne textuelle), paramètres graphiques et effet progressif sur la dynamique. Ne pas réduire un crescendo à un événement ponctuel.

Référence : [MuseScore — Dynamics and hairpins](https://handbook.musescore.org/notation/expressive-markings/dynamics-and-hairpins).

## 4. Tempo et indications de mouvement

**Éléments :** indications métronomiques ; Andante, Allegro, Adagio ; accelerando, ritardando, rallentando, allargando, a tempo, tempo primo, ritenuto, rubato ; modulations métriques et lignes progressives de tempo.

**Gestion dans MuseScore :** les indications métronomiques, verbales et progressives sont des types d'objets distincts. Les objets Tempo peuvent agir sur la lecture. Les lignes progressives ont une plage et un réglage d'effet. Un texte générique ayant l'apparence d'une indication de tempo n'agit pas automatiquement sur le tempo. Dorico propose également un panneau Tempo pour les marques métronomiques, les changements graduels et les équations de tempo.

**À reprendre dans MireDo :** séparer le texte affiché de la valeur de tempo interprétée ; conserver la référence de tempo déjà validée (noires par minute) ; associer un changement ponctuel à son unité et une évolution à son début et sa fin ; appliquer les changements à la chronologie commune sans les confondre avec les changements de signature.

Références : [MuseScore — Tempo markings](https://handbook.musescore.org/text/tempo-markings) ; [Dorico — Operation Manual](https://www.steinberg.help/api/khub/documents/YL~uVcPTrJjjZGd0jr_sxQ/content).

## 5. Articulations et accents

**Éléments :** staccato, staccatissimo, tenuto, accent, marcato et combinaisons d'articulations.

**Gestion dans MuseScore :** palette Articulations ; ajout à une ou plusieurs notes sélectionnées ou par glisser-déposer. Les propriétés incluent le placement. Les styles règlent l'alignement par rapport à la hampe ou à la tête de note et le comportement des articulations combinées. Certaines articulations influencent la durée, l'attaque ou l'intensité en lecture.

**À reprendre dans MireDo :** identité conventionnelle de chaque articulation, association ponctuelle à l'unité, combinaisons conservées, propriétés de placement et effet sonore propre au type lorsque le moteur le prend en charge.

Référence : [MuseScore — Articulations](https://handbook.musescore.org/notation/expressive-markings/articulations).

## 6. Ornements

**Éléments :** trilles courts, mordants, gruppettos et autres ornements ponctuels ; lignes de trille et ornements prolongés.

**Gestion dans MuseScore :** les ornements ponctuels sont appliqués à une note. Leurs propriétés peuvent préciser l'intervalle, la qualité de l'intervalle et les altérations ; le logiciel tient compte du contexte tonal et des altérations de la mesure. Les lignes d'ornement sont des objets étendus avec début et fin ajustables.

**À reprendre dans MireDo :** distinguer ornement ponctuel et ligne d'ornement ; conserver intervalle, altérations, type, association et paramètres de réalisation ; conserver des bornes pour les lignes. La lecture ornementée dépend du type et du moteur.

Référence : [MuseScore — Ornaments](https://handbook.musescore.org/notation/expressive-markings/ornaments).

## 7. Notes de grâce

**Éléments :** appoggiatures, acciaccaturas, notes de grâce avant ou après une note principale et groupes de notes de grâce.

**Gestion dans MuseScore :** les notes de grâce sont de petites notes liées à une note principale. Elles ont leur propre hauteur et leur propre apparence ; leur valeur est prise sur la note principale ou réalisée selon la convention de l'ornement, sans être ajoutée comme durée métrique ordinaire à la mesure.

**À reprendre dans MireDo :** traiter chaque note de grâce comme un événement musical lié à sa note principale ; conserver hauteur, type, ordre et apparence ; ne pas augmenter naïvement la durée métrique totale. La réalisation sonore doit suivre la convention et les capacités du moteur.

Référence : [MuseScore — Grace notes](https://handbook.musescore.org/notation/expressive-markings/grace-notes).

## 8. Trémolos et roulements

**Éléments :** trémolo sur une note, trémolo alterné entre deux notes ou accords, buzz roll et autres répétitions rapides notées.

**Gestion dans MuseScore :** distinction entre trémolo à une note et trémolo entre plusieurs événements. Le nombre de barres indique la subdivision conventionnelle. Certains signes de roulement sont uniquement notatifs et ne possèdent pas d'effet de lecture. Dorico range les trémolos dans Repeat Structures.

**À reprendre dans MireDo :** conserver les événements concernés, la distinction entre trémolo simple et alterné et la subdivision notée. Ne pas supposer qu'un signe graphique implique toujours une lecture sonore ; préserver les signes notatifs même sans effet disponible.

Références : [MuseScore — Tremolos and rolls](https://handbook.musescore.org/notation/expressive-markings/tremolos-and-rolls) ; [Dorico — Operation Manual](https://www.steinberg.help/api/khub/documents/YL~uVcPTrJjjZGd0jr_sxQ/content).

## 9. Arpèges, glissandos, portamentos et bends

**Éléments :** signes d'arpège et flèches de strumming ; glissando ; portamento ; bends et slides instrumentaux.

**Gestion dans MuseScore :** un arpège est appliqué à un accord ou à un groupe de notes ; sa hauteur graphique peut être ajustée et il peut couvrir plusieurs voix ou portées d'un instrument. Sa lecture peut comporter un délai de dispersion. Un glissando relie une note de départ à une note d'arrivée ; son type de ligne, son texte et son style de lecture (chromatique, diatonique, etc.) sont configurables. Les bends instrumentaux sont des objets distincts.

**À reprendre dans MireDo :** l'arpège conserve les notes concernées et son sens de réalisation ; le glissando/portamento conserve ses deux bornes et son type de transition ; les propriétés graphiques restent distinctes des paramètres de lecture ; les bends gardent leur contexte instrumental.

Référence : [MuseScore — Arpeggios and glissandos](https://handbook.musescore.org/notation/expressive-markings/arpeggios-and-glissandos).

## 10. Pauses, respirations et points d'orgue

**Éléments :** point d'orgue/fermata, respiration, césure/caesura et signes apparentés.

**Gestion dans MuseScore :** le point d'orgue peut être placé sur une note, un silence ou une barre. La respiration et la césure sont placées près de l'événement concerné. Ces éléments peuvent avoir un effet réglable sur la lecture. Dorico les regroupe dans Holds and Pauses.

**À reprendre dans MireDo :** conserver l'événement ou le repère concerné, la position et l'effet de prolongation ou de pause ; distinguer l'apparence graphique de l'effet temporel ; ne pas convertir ces indications en silences ordinaires si cela détruit leur fonction.

Références : [MuseScore — Breaths and pauses](https://handbook.musescore.org/notation/expressive-markings/breaths-and-pauses) ; [Dorico — Operation Manual](https://www.steinberg.help/api/khub/documents/YL~uVcPTrJjjZGd0jr_sxQ/content).

## 11. Liaisons et lignes musicales

**Éléments :** liaison d'expression, liaison de prolongation, laissez vibrer, lignes d'octave, de pédale, de trille, de nuances, de tempo et de techniques instrumentales.

**Gestion dans MuseScore :** les lignes spécialisées ont des extrémités ajustables, une plage et des propriétés graphiques. Elles peuvent comporter un texte ou un symbole de début/fin. Les liaisons, lignes d'octave, de pédale ou de trille conservent cependant une fonction musicale propre ; elles ne sont pas de simples traits décoratifs.

**À reprendre dans MireDo :** ne pas réduire toutes les lignes à un objet graphique générique. Conserver le type spécialisé, le début, la fin et la portée. Une liaison de prolongation conserve la continuité de durée ; une liaison d'expression conserve sa plage ; une ligne d'octave conserve son décalage ; une ligne de pédale ou de technique conserve sa fonction. La forme graphique est séparée de la fonction musicale.

Références : [MuseScore — Other lines](https://handbook.musescore.org/notation/expressive-markings/other-lines) ; [MuseScore — Items across repeats and jumps](https://handbook.musescore.org/notation/repeats/items-across-repeats-and-jumps).

## 12. Techniques de jeu instrumentales et vocales

**Éléments :** arco, pizzicato, con sordino, senza sordino, sourdine, harmoniques, vibrato, palm mute, let ring, slides, bends et techniques propres aux vents, cordes, percussions, claviers ou voix. Les doigtés et indications de corde sont à distinguer des techniques qui modifient le son.

**Gestion dans les références :** Dorico organise les techniques par familles d'instruments dans Playing Techniques. MuseScore les répartit dans les outils spécialisés selon les instruments. Certaines techniques modifient le son ou le comportement de lecture ; d'autres informent seulement l'interprète.

**À reprendre dans MireDo :** organiser les éléments selon le contexte instrumental ou vocal ; conserver le type, le symbole ou libellé, l'association et la portée ; représenter les changements d'état comme arco vers pizzicato par des débuts et fins lorsque nécessaire ; ne pas supprimer une indication parce que le moteur sonore ne sait pas la réaliser.

Référence : [Dorico — Operation Manual, Playing Techniques](https://www.steinberg.help/api/khub/documents/YL~uVcPTrJjjZGd0jr_sxQ/content).

## 13. Reprises, sauts et navigation

**Éléments :** barres de reprise, fins alternatives/voltas, D.C., D.S., Segno, Coda, Fine, To Coda, marqueurs, instructions de saut et nombres de répétitions.

**Gestion dans MuseScore :** les signes de reprise, fins alternatives, sauts et marqueurs sont des objets distincts. Les marqueurs ont des identifiants ou libellés ; les instructions de saut définissent une destination, un point jusqu'auquel jouer et éventuellement un point de continuation. Les propriétés contrôlent les relations et le comportement de lecture. Dorico regroupe les structures de répétition dans Repeat Structures.

**À reprendre dans MireDo :** conserver les instructions comme objets structurels, leurs destinations, identifiants, conditions et ordre de parcours. La lecture suit le parcours sans modifier l'ordre linéaire du document. Les décisions propres à Tonic Sol-fa restent prioritaires : D.C., D.S., Segno, Fine, Coda et To Coda ; les barres de reprise classiques ne deviennent pas le mécanisme par défaut de cette notation.

Références : [MuseScore — Jumps and markers](https://handbook.musescore.org/notation/repeats/jumps-and-markers) ; [MuseScore — Repeat signs](https://handbook.musescore.org/notation/repeats/repeat-signs) ; [Dorico — Operation Manual](https://www.steinberg.help/api/khub/documents/YL~uVcPTrJjjZGd0jr_sxQ/content).

## 14. Repères, textes et annotations musicales

**Éléments :** repères de répétition ; texte de portée ; texte de système ; texte d'expression ; indications de mouvement ou de caractère ; doigtés et annotations spécialisées.

**Gestion dans MuseScore :** plusieurs types de texte distincts existent :
- **Staff Text :** concerne une portée ou un instrument ;
- **System Text :** concerne le système entier ;
- **Expression Text :** annotation expressive qui ne modifie pas automatiquement la lecture ;
- **Rehearsal Mark :** repère de répétition et de navigation, généralement affiché au-dessus du système ;
- textes spécialisés : doigtés, indications de corde, etc.

Les repères peuvent être nommés manuellement ou numérotés automatiquement. Leur cadre, style, alignement et visibilité sont configurables.

**À reprendre dans MireDo :** conserver le type de texte, son contenu, sa portée de visibilité et son style. Un repère doit pouvoir identifier et retrouver une section. Un texte générique n'agit pas sur le tempo ou les nuances. Les paroles chantées conservent leur système dédié déjà conçu et ne sont pas fusionnées avec ces annotations.

Références : [MuseScore — Entering and editing text](https://handbook.musescore.org/text/entering-and-editing-text) ; [MuseScore — Rehearsal marks](https://handbook.musescore.org/text/rehearsal-marks) ; [MuseScore — Staff, system, and expression text](https://handbook.musescore.org/text/staff-system-and-expression-text).

## 15. Symboles harmoniques et chiffrages

**Éléments :** symboles d'accords ; analyse en chiffres romains ; système Nashville ; basse chiffrée ; N.C. ; diagrammes d'accords associés.

**Gestion dans MuseScore :** les symboles d'accords sont saisis comme texte structuré (fondamentale, qualité, extensions, altérations, renversements et modificateurs), puis mis en forme. MuseScore distingue symboles d'accords, chiffres romains, Nashville et basse chiffrée. Les comportements de lecture diffèrent : accords et Nashville peuvent être joués ; l'analyse en chiffres romains n'est pas jouée. La basse chiffrée dispose de son propre mécanisme de saisie.

**À reprendre dans MireDo :** distinguer le symbole harmonique de l'accord effectivement écrit en notes ; conserver la forme saisie et, si interprétée, sa structure ; distinguer accord, analyse romaine, Nashville et basse chiffrée ; conserver les paramètres de rendu et de lecture. Une analyse harmonique n'est pas automatiquement un événement sonore.

Références : [MuseScore — Chord symbols](https://handbook.musescore.org/text/chord-symbols) ; [MuseScore — Figured bass](https://handbook.musescore.org/text/figured-bass).

## 16. Autres symboles musicaux

Les logiciels de notation proposent des symboles spécialisés qui peuvent être ajoutés à une note, un silence, une barre ou un autre symbole. Il faut distinguer le symbole musical reconnu avec sa fonction, le glyphe purement graphique et le texte libre. Un symbole sans fonction sonore ne doit pas être interprété automatiquement par le moteur.

Référence : [MuseScore — Other symbols](https://handbook.musescore.org/notation/expressive-markings/other-symbols).

---

## 17. Synthèse des comportements

| Type fonctionnel | Exemples | Informations à conserver |
|---|---|---|
| Ponctuel | nuance, articulation, ornement, accord | unité, type, propriétés |
| Étendu | crescendo, glissando, liaison, ligne d'octave | début, fin, portée, type, propriétés |
| Structurel | D.C., D.S., Fine, Coda, volta | repères, destinations, conditions, parcours |
| Événement musical lié | note de grâce, trémolo alterné | événements concernés, lien, durée/réalisation |
| Texte spécialisé | texte de portée, repère, tempo textuel | type, contenu, portée, style, fonction |
| Graphique | symbole sans effet sonore | symbole, ancrage, position, apparence |

## 18. Établi et travaux restants

### Cadrage fonctionnel documenté

- Une catégorie générale « Informations supplémentaires ».
- Les familles et comportements décrits dans cette page.
- MuseScore comme référence principale et Dorico comme référence complémentaire.
- La distinction entre objets ponctuels, étendus, structurels, événements liés, textes spécialisés et symboles graphiques.
- La séparation entre rendu visuel et effet de lecture.
- La règle MireDo : unité pour le ponctuel, bornes pour les étendues, repères pour les structures.

### À concevoir avant l'implémentation

- Inventaire exhaustif des symboles et variantes.
- Propriétés exactes et valeurs possibles de chaque type.
- Organisation concrète du catalogue et des palettes.
- Gestes d'ajout, modification, déplacement et suppression dans l'éditeur.
- Schéma de stockage JSON du fichier .mrd.
- Rendu, alignement, collisions et mise en page.
- Paramètres de lecture, correspondance avec les banques de sons et limites des moteurs.
- Matrice de prise en charge par format d'export.

Ces travaux techniques et d'interface ne remettent pas en cause les décisions fonctionnelles déjà clôturées.

## 19. Références documentaires

### MuseScore Studio
- [Manuel MuseScore Studio](https://handbook.musescore.org/)
- [Expressive markings](https://handbook.musescore.org/notation/expressive-markings)
- [Tempo markings](https://handbook.musescore.org/text/tempo-markings)
- [Jumps and markers](https://handbook.musescore.org/notation/repeats/jumps-and-markers)
- [Repeat signs](https://handbook.musescore.org/notation/repeats/repeat-signs)
- [Entering and editing text](https://handbook.musescore.org/text/entering-and-editing-text)
- [Chord symbols](https://handbook.musescore.org/text/chord-symbols)

### Dorico
- [Dorico Operation Manual](https://www.steinberg.help/api/khub/documents/YL~uVcPTrJjjZGd0jr_sxQ/content)

Les manuels évoluent selon les versions. Les références documentent les comportements observés et devront être revérifiées au moment de l'implémentation.
