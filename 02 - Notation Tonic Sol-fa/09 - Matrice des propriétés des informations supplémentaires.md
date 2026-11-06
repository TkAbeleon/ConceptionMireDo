# Matrice des propriétés des informations supplémentaires

Cette page complète le catalogue fonctionnel des informations supplémentaires. Elle identifie les données qu'un élément doit conserver pour rester fidèle aux conventions des logiciels de notation de référence.

**Important :** il s'agit d'une matrice de besoins fonctionnels et de contraintes de données, pas encore du schéma JSON final. Les noms ci-dessous sont des concepts descriptifs, pas des noms de clés JSON imposés.

Références principales : MuseScore Studio Handbook ; Dorico Operation Manual. Les propriétés observées dans ces logiciels sont adaptées à MireDo sans reprendre leur modèle interne à l'identique.

## 1. Principes de conception des propriétés

### 1.1 Distinguer quatre couches

Chaque élément doit être analysé selon quatre couches indépendantes :

1. **Identité et sens musical** : de quel élément s'agit-il et quelle est sa fonction conventionnelle ?
2. **Association et portée** : à quelle unité, quel événement, quelle plage, quelle voix, quelle portée ou quel repère s'applique-t-il ?
3. **Présentation graphique** : quel symbole/texte est affiché, où et comment ?
4. **Interprétation et lecture** : quel effet musical ou sonore est produit, s'il y en a un ?

Ces couches ne doivent pas être fusionnées. Par exemple, déplacer un symbole au-dessus ou au-dessous de la portée ne doit pas changer son effet musical. Modifier le texte visible ne doit pas implicitement modifier une valeur de tempo ou une destination de reprise.

### 1.2 Propriétés communes conceptuelles

Tout objet d'information supplémentaire doit pouvoir conserver, lorsque pertinent :

| Groupe | Informations à conserver | Règle |
|---|---|---|
| Identité | type fonctionnel, variante, famille | type explicite ; ne pas déduire uniquement du texte ou du glyphe |
| Association | unité ou événement associé, ou repère structurel | ponctuel = unité MireDo ; ne pas descendre à une granularité plus fine |
| Étendue | début, fin, portée concernée | obligatoire pour une indication qui couvre une plage |
| Contexte | voix, portée/instrument, portée locale ou globale | uniquement lorsque la convention le demande |
| Contenu | texte saisi, symbole, valeur musicale structurée | garder le texte et les valeurs interprétées distincts |
| Présentation | placement, alignement, taille, décalage, visibilité | propriétés de rendu ; ne changent pas le sens musical |
| Lecture | activation, paramètres d'effet, valeur interprétée | uniquement pour les objets ayant une fonction de lecture |
| Relations | lien vers une note, une autre indication, une destination ou un groupe | références stables ; ne pas copier le contenu lié |
| État | actif/inactif, éventuellement masqué ou non joué | visibilité et activation sonore sont deux notions distinctes |

Toutes ces propriétés ne sont pas obligatoires pour chaque élément. Le type détermine les propriétés applicables.

### 1.3 Propriétés individuelles et styles globaux

MuseScore distingue les propriétés d'un objet particulier des styles généraux de la partition. MireDo doit conserver cette séparation :

- **propriété de l'objet** : exception propre à une indication ;
- **style de famille** : valeurs par défaut communes aux éléments d'une famille ;
- **style général de partition** : règles globales de notation et d'espacement ;
- **préférence d'éditeur** : préférence d'interface qui n'est pas nécessairement une donnée musicale du fichier.

Ne pas enregistrer dans chaque indication une valeur identique qui relève du style global, sauf lorsqu'elle constitue une surcharge individuelle explicite.

### 1.4 Position automatique et position manuelle

La position par défaut doit être calculée selon les règles de placement et d'évitement des collisions. Une position manuelle peut être conservée comme ajustement explicite. Il faut donc distinguer conceptuellement :

- le mode de placement : automatique ou manuel ;
- le côté ou la région de placement : au-dessus, au-dessous, entre portées, etc. ;
- le décalage manuel, si l'utilisateur en a défini un ;
- la visibilité dans la partition ou dans une partie, si cette distinction existe.

La position ne doit jamais remplacer l'association musicale.

### 1.5 Valeurs de lecture

Les valeurs destinées à la lecture doivent être stockées dans des unités définies et indépendantes de la représentation graphique. Les valeurs dérivées peuvent être calculées, mais les paramètres saisis par l'utilisateur doivent être conservés.

La propriété générale « jouer/ne pas jouer » ne suffit pas pour décrire tous les effets : certains objets changent une durée, d'autres un tempo, une dynamique, une hauteur ou un parcours.

---

## 2. Matrice par famille

Les tableaux distinguent les données fonctionnelles nécessaires, les propriétés de présentation et les propriétés de lecture. « Selon prise en charge » signifie que MireDo conserve l'indication même si le moteur sonore ou l'instrument ne peut pas la reproduire.

### 2.1 Nuances et dynamique

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | type de nuance conventionnelle (pp, p, mp, mf, f, ff, etc.) |
| Association | unité musicale d'application |
| Portée | voix concernée, toutes les voix ou portée/instrument concerné |
| Contenu | symbole dynamique ; texte intégré à la nuance si la convention le prévoit |
| Présentation | placement, taille, alignement, espacement, position manuelle éventuelle |
| Lecture | niveau dynamique cible ou intensité conventionnelle interprétée ; portée d'application |
| Relations | texte d'expression séparé éventuellement aligné avec la nuance |

Ne pas confondre une nuance avec un texte d'expression placé à côté. Une nuance peut être appliquée à une voix particulière ou à l'ensemble de l'instrument ; cette portée a une conséquence possible sur la lecture.

### 2.2 Évolutions progressives de dynamique

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | crescendo, diminuendo/decrescendo, soufflet ou ligne textuelle |
| Association | début et fin exacts dans la chronologie MireDo |
| Portée | voix/portée/instrument concerné |
| Contenu | symbole ou texte affiché, éventuelle nuance cible |
| Présentation | forme du soufflet, ouverture, ligne, épaisseur, tirets, placement |
| Lecture | niveau de départ/cible si défini, courbe ou interpolation, activation |
| Relations | liaison éventuelle aux nuances de départ et d'arrivée |

La plage est une donnée fonctionnelle. Le dessin du soufflet est une donnée de présentation. Les deux ne doivent pas être confondus.

### 2.3 Tempo et indications de mouvement

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | marque métronomique, indication verbale, changement ponctuel, ligne progressive, modulation métrique |
| Association | unité ou position chronologique d'effet |
| Portée | partition entière / système commun, selon la fonction |
| Contenu | valeur de note de référence, nombre, texte verbal, équation métrique |
| Présentation | glyphe de note, texte, taille, placement, style |
| Lecture | tempo effectif en noires par minute, mode suivre l'écrit ou valeur de remplacement |
| Progression | début, fin, valeur cible ou pourcentage, courbe de transition |
| Relations | tempo précédent restauré pour a tempo ; tempo initial pour tempo primo, si cette fonction est choisie |

**Décision MireDo déjà validée :** la référence conventionnelle du tempo est la noire par minute, indépendante de l'unité native Sol-fa. Le modèle doit conserver le texte/repère écrit et la valeur interprétée séparément.

Le manuel MuseScore distingue les marques métronomiques, les indications verbales, les lignes progressives et les modulations métriques. Il permet des paramètres de remplacement du tempo écrit et, pour les lignes, une cible et une méthode de transition. Il précise également que les indications de tempo agissent sur toutes les portées de la partition.

### 2.4 Articulations et accents

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | type d'articulation (staccato, tenuto, accent, marcato, etc.) |
| Association | unité musicale concernée |
| Portée | événement/unité et voix concernée si nécessaire |
| Présentation | au-dessus/au-dessous, alignement avec hampe ou tête, combinaison avec d'autres articulations |
| Lecture | effet propre au type : durée, attaque, intensité, ou aucun effet |
| Relations | groupe d'articulations combinées si plusieurs signes forment un ensemble |

Le placement et l'alignement sont des propriétés graphiques. L'effet sonore dépend du type d'articulation et ne doit pas être généralisé à tous les signes.

### 2.5 Ornements

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | trille, mordant, gruppetto, tour, autre ornement |
| Association | unité de la note ornée |
| Contexte musical | intervalle, numéro et qualité d'intervalle ; sens ou variante |
| Altérations | altérations nécessaires à la réalisation et règles d'affichage |
| Présentation | symbole, placement, taille, note auxiliaire éventuelle, visibilité des altérations |
| Lecture | réalisation de l'ornement, activation, paramètres de réalisation |
| Étendue | bornes si l'ornement est une ligne de trille ou un objet prolongé |

MuseScore prend en compte l'armure et les altérations de la mesure ; les propriétés d'intervalle peuvent modifier simultanément l'affichage des altérations et la lecture. Cette dépendance doit être conservée dans MireDo.

### 2.6 Notes de grâce

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | appoggiature, acciaccatura, autre type |
| Relation | note principale à laquelle le groupe est attaché |
| Événements | hauteur, ordre, nombre de notes et éventuelles altérations |
| Présentation | taille réduite, hampe, barre oblique, groupement, placement |
| Lecture | mode de réalisation, durée prise sur la note principale, ordre d'exécution |
| Temporalité | ne pas ajouter automatiquement une durée métrique autonome à l'unité |

Une note de grâce est un événement musical lié, pas un simple symbole. Sa représentation doit préserver la relation avec la note principale et l'ordre des événements.

### 2.7 Trémolos et roulements

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | trémolo sur une note, trémolo entre événements, roulement |
| Relations | note ou notes/accords participants |
| Répétition | nombre de barres ou niveau de subdivision noté |
| Présentation | symbole, nombre de barres, placement |
| Lecture | nombre/vitesse de répétitions ou type de réalisation, si pris en charge |
| Temporalité | conservation de la durée globale des événements concernés |

Un trémolo à une note et un trémolo alterné n'ont pas les mêmes relations. La structure doit pouvoir les distinguer.

### 2.8 Arpèges, glissandos, portamentos et bends

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | arpège, glissando, portamento, bend, slide |
| Association | accord/groupe de notes ou deux événements de début et de fin |
| Sens | direction de l'arpège ou transition de hauteur |
| Étendue | notes/portées couvertes, début et fin |
| Présentation | flèche, ligne, courbe, texte, épaisseur, hauteur graphique |
| Lecture | délai d'arpégiation, type de transition (chromatique/diatonique ou spécifique), amplitude et courbe si applicables |
| Activation | lecture activée ou désactivée lorsque la référence propose cette option |

MuseScore permet notamment un délai de dispersion et une désactivation de lecture pour les arpèges. Les glissandos relient deux notes et peuvent avoir un mode de lecture propre. Les propriétés graphiques restent indépendantes.

### 2.9 Pauses, respirations et points d'orgue

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | fermata, respiration, césure ou autre pause |
| Association | note, silence, unité ou repère concerné selon le signe |
| Présentation | symbole, au-dessus/au-dessous, taille, placement |
| Lecture | facteur de prolongation ou d'étirement temporel, durée de pause, activation |
| Portée | portée/instrument ou ensemble concerné selon le type |

MuseScore permet de régler l'effet de lecture des pauses par un facteur d'étirement temporel. MireDo doit conserver cet effet séparément du symbole affiché.

### 2.10 Liaisons et lignes musicales

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | liaison d'expression, liaison de prolongation, laissez vibrer, ligne d'octave, pédale, trille, ligne textuelle ou autre ligne spécialisée |
| Étendue | début, fin, portée/voix concernée |
| Sémantique | continuité de durée, expression, transposition d'octave, pédale, technique ou autre fonction |
| Présentation | type de trait, courbe, crochet, épaisseur, tirets, texte de début/fin, texte de continuation |
| Lecture | effet propre au type : prolongation, octave, sustain, trille, technique, ou aucun |
| Relations | notes de départ et de fin, ou indication dont la ligne matérialise l'étendue |

Ne pas utiliser un unique objet « ligne » sans type fonctionnel. La liaison de prolongation n'est pas une liaison d'expression ; une ligne d'octave n'est pas une simple annotation.

### 2.11 Techniques de jeu

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | technique conventionnelle et variante |
| Contexte | instrument ou famille instrumentale/vocale concernée |
| Association | unité, événement ou début/fin d'une plage |
| État | activation, désactivation ou remplacement par une autre technique |
| Présentation | texte, symbole, placement, taille |
| Lecture | technique/son associé si la banque sonore la prend en charge |
| Relations | technique de début et technique de retour éventuelle (ex. arco après pizzicato) |

Le catalogue peut être organisé selon l'instrument, mais l'identité de la technique doit rester indépendante du nom du son effectivement disponible.

### 2.12 Reprises et navigation

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | instruction de saut ou marqueur structurel |
| Marqueur | type (Segno, Coda, Fine, To Coda), identifiant/label stable |
| Instruction | type D.C./D.S. et variante al Fine/al Coda |
| Destination | marqueur cible |
| Parcours | point jusqu'auquel jouer, destination de continuation, répétitions éventuelles |
| Conditions | règle de déclenchement et état de parcours |
| Présentation | texte/symbole, alignement, taille |
| Lecture | activation des reprises/sauts et règles d'exécution |

MuseScore relie les sauts et marqueurs par des labels qui peuvent être différents du texte affiché. Un saut peut avoir une destination, un point jusqu'auquel jouer, une destination de continuation et une option concernant les reprises. Cette distinction entre label fonctionnel et texte affiché est indispensable.

**Point encore à concevoir :** les règles exactes de parcours de plusieurs retours, Fine et Coda dans MireDo. La syntaxe Sol-fa et les décisions déjà consignées restent prioritaires.

### 2.13 Repères, textes et annotations

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | texte de portée, texte de système, expression, repère de répétition, texte spécialisé |
| Contenu | texte exact, caractères spéciaux, formatage par caractère si nécessaire |
| Association | unité ou repère de position |
| Portée | portée/instrument, système entier ou repère partagé |
| Présentation | style de texte, police, taille, gras/italique, alignement, cadre, placement |
| Lecture | aucun effet par défaut ; effet spécifique seulement pour un type explicitement fonctionnel |
| Relations | association à une nuance, une technique ou un repère de parcours si nécessaire |

MuseScore distingue Staff Text, System Text et Expression Text. Le texte de portée peut agir sur un instrument ; le texte de système peut agir sur tous les instruments ; l'expression textuelle ne modifie pas automatiquement la lecture. MireDo doit conserver ces distinctions fonctionnelles.

Les paroles chantées restent dans leur système dédié, en dehors de cette famille d'annotations.

### 2.14 Symboles harmoniques et chiffrages

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | symbole d'accord, Nashville, chiffres romains, basse chiffrée |
| Contenu saisi | forme textuelle d'origine |
| Structure interprétée | fondamentale, qualité, extensions, altérations, renversement, modificateurs, selon le type |
| Association | position/unité harmonique |
| Présentation | style, police, formatage, diagramme associé si présent |
| Transposition | comportement de transposition, si applicable |
| Lecture | voicing, instrument, octave, durée ou désactivation selon le type |
| Sémantique | distinguer accord jouable et analyse harmonique non jouée |

MuseScore permet la lecture des symboles d'accords et des nombres Nashville, tandis que l'analyse en chiffres romains n'est pas jouée. La structure harmonique et le texte affiché doivent rester distincts.

### 2.15 Autres symboles

| Dimension | Propriétés à prévoir |
|---|---|
| Identité | identifiant du symbole musical ou glyphe |
| Association | ancrage pertinent |
| Présentation | taille, placement, décalage, orientation éventuelle |
| Fonction | fonction musicale reconnue ou caractère purement graphique |
| Lecture | aucune par défaut, sauf fonction explicitement documentée |

---

## 3. Contraintes transversales à respecter

1. **Pas de sémantique implicite depuis le texte.** Le texte « Allegro » ne suffit pas à définir un événement Tempo.
2. **Pas de sémantique implicite depuis le glyphe.** Un glyphe décoratif n'est pas automatiquement un événement musical.
3. **Pas de perte d'association.** Déplacer graphiquement un objet ne doit pas changer l'unité ou la plage musicale à laquelle il s'applique, sauf action explicite de réassociation.
4. **Pas de perte de portée.** Une indication locale à une voix ne doit pas devenir globale par défaut.
5. **Pas de confusion entre portée et placement.** « Au-dessus de la portée » est une position graphique, pas une portée musicale.
6. **Pas de confusion entre masqué et inactif.** Un objet caché peut rester fonctionnel ; un objet visible peut être exclu de la lecture.
7. **Pas de confusion entre valeur écrite et valeur jouée.** Une surcharge de lecture doit être conservée sans détruire le texte ou la notation d'origine.
8. **Pas de perte des types spécialisés.** Les notes de grâce, liaisons, trémolos, reprises et techniques conservent leurs relations et structures propres.
9. **Les propriétés non applicables sont absentes.** Ne pas remplir tous les objets avec des champs vides ou artificiels.
10. **Les références doivent rester stables.** Les relations entre début/fin, note principale, marqueur, saut et technique doivent survivre à la réorganisation du document.

## 4. Propriétés de style et de présentation communes

Le système de rendu doit prévoir, selon les objets :

- placement automatique ou manuel ;
- position relative à la portée, à l'unité ou à un autre objet ;
- décalage horizontal et vertical ;
- taille ou échelle ;
- alignement ;
- espacement avant/après ;
- type de trait, épaisseur, tirets et crochets pour les lignes ;
- police, style, taille et formatage pour les textes ;
- ordre d'affichage en cas de chevauchement ;
- visibilité dans la partition et les parties, si celles-ci sont prises en charge.

Ces propriétés ne sont pas toutes nécessaires pour chaque type. Le catalogue de propriétés doit être typé et limité aux possibilités pertinentes.

## 5. Propriétés de lecture communes

Le moteur de lecture doit pouvoir distinguer les effets suivants, sans imposer qu'ils existent pour tous les objets :

- dynamique / intensité ;
- tempo / vitesse ;
- durée / prolongation / étirement ;
- attaque et articulation ;
- ornementation ;
- répétition rapide / trémolo ;
- transition de hauteur ;
- pédale ou sustain ;
- technique instrumentale ;
- navigation et parcours de répétition.

Un objet peut n'avoir aucun effet de lecture. Cette absence est un comportement valide et doit être conservée.

## 6. Contrôle de préparation avant schéma JSON

### Informations supplémentaires

- [x] Catégorie générale unique et familles fonctionnelles définies.
- [x] Référence principale MuseScore et référence complémentaire Dorico.
- [x] Distinction entre objets ponctuels, étendus, structurels, événements liés, textes et symboles graphiques.
- [x] Règle d'association MireDo : unité pour le ponctuel, bornes pour l'étendu, repères pour le structurel.
- [x] Principes de séparation identité / association / présentation / lecture.
- [x] Matrice des propriétés conceptuelles par famille.
- [x] Contraintes transversales de conservation et d'intégrité.
- [ ] Inventaire exhaustif des symboles et de leurs variantes.
- [ ] Décision détaillée sur les propriétés de chaque variante rare ou spécialisée.
- [ ] Résolution des règles de parcours complexes D.C./D.S./Fine/Coda.
- [ ] Définition de la prise en charge exacte des effets sonores et des limites du moteur.
- [ ] Définition des styles globaux, des surcharges individuelles et des préférences d'éditeur dans l'architecture générale.

### Conclusion

Le **niveau conceptuel des propriétés** des informations supplémentaires est suffisamment décrit pour servir de base au schéma : les familles, les associations, les données fonctionnelles, la présentation et la lecture sont distinguées.

Cela ne signifie pas que chaque variante de symbole est déjà entièrement paramétrée. Les détails rares peuvent être affinés après le premier schéma si celui-ci prévoit une structure extensible et versionnée. Les règles de parcours complexes et les choix de lecture doivent toutefois être définis avant de figer les structures correspondantes.

Le schéma JSON ne doit pas être écrit à partir de cette seule page : il doit intégrer également les décisions déjà validées sur les mesures, les voix, les notes, les durées, les paroles, les références tonales, le tempo et la source de vérité du document.

## 7. Références documentaires

### MuseScore Studio Handbook

- [Dynamics and hairpins](https://handbook.musescore.org/notation/expressive-markings/dynamics-and-hairpins)
- [Tempo markings](https://handbook.musescore.org/en_gb/text/tempo-markings)
- [Articulations](https://handbook.musescore.org/notation/expressive-markings/articulations)
- [Ornaments](https://handbook.musescore.org/notation/expressive-markings/ornaments)
- [Grace notes](https://handbook.musescore.org/notation/expressive-markings/grace-notes)
- [Tremolos and rolls](https://handbook.musescore.org/notation/expressive-markings/tremolos-and-rolls)
- [Arpeggios and glissandos](https://handbook.musescore.org/notation/expressive-markings/arpeggios-and-glissandos)
- [Breaths and pauses](https://handbook.musescore.org/notation/expressive-markings/breaths-and-pauses)
- [Other lines](https://handbook.musescore.org/notation/expressive-markings/other-lines)
- [Jumps and markers](https://handbook.musescore.org/notation/repeats/jumps-and-markers)
- [Staff, system, and expression text](https://handbook.musescore.org/en_gb/text/staff-system-and-expression-text)
- [Chord symbols](https://handbook.musescore.org/en_gb/text/chord-symbols)
- [Rehearsal marks](https://handbook.musescore.org/text/rehearsal-marks)
- [Properties panel](https://handbook.musescore.org/fr/basics/properties-panel)
- [Formatting text](https://handbook.musescore.org/text/formatting-text)
- [Positioning and automatic placement](https://handbook.musescore.org/fr/basics/using-the-palettes)

### Dorico

- [Dorico Operation Manual](https://www.steinberg.help/api/khub/documents/YL~uVcPTrJjjZGd0jr_sxQ/content)
