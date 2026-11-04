# Exigences de conception du format natif

**Statut : premières exigences déduites de la conception existante ; schéma non validé.**

Ce document énumère ce que le futur format doit pouvoir préserver et représenter. Il ne fixe pas encore les noms définitifs des champs JSON.

## 1. Identité et évolutivité du fichier

Le format devrait posséder :

- un identifiant explicite du format ;
- une version du format indépendante de la version de l'application ;
- une structure permettant de détecter un fichier incompatible ou plus récent ;
- une stratégie de migration lorsque la structure évolue ;
- un encodage de texte défini, avec prise en charge des caractères Unicode utilisés dans les titres, paroles et indications.

L'extension native envisagée est `.mrd`. Le choix entre un document JSON directement enregistré sous cette extension et une autre organisation reste ouvert.

## 2. Conserver l'écriture originale

La graphie saisie est une donnée essentielle.

Le format doit préserver :

- chaque degré Sol-fa écrit ;
- la voyelle d'altération exacte ;
- le suffixe numérique d'octave ;
- les formes rares valides ;
- les équivalences enharmoniques sans substitution ;
- les signes rythmiques et leur ordre ;
- les indications et annotations écrites.

Une hauteur MIDI, un nom absolu ou une graphie alternative sont des résultats calculés. Ils ne doivent pas écraser la graphie originale.

Le fichier doit pouvoir être ouvert puis enregistré sans transformer silencieusement `mi` en `f`, `de` en `t_1`, ou toute autre graphie équivalente.

## 3. Séparer les catégories d'information

Le modèle devra distinguer :

| Catégorie | Exemples |
|---|---|
| Métadonnées | Titre, compositeur, description, auteurs, informations éditoriales. |
| Contexte musical | Système de notation, référence tonale, signature, tempo. |
| Voix | Identifiant, nom, référence de portée. |
| Contenu musical | Notes, silences, subdivisions, prolongations, mesures. |
| Annotations | Accords, paroles, reprises, nuances, articulations, transitions. |
| Mise en page | Groupes de portées, crochet, placement des paroles, retours de système, sauts de page. |
| Données dérivées | Hauteur absolue, durée calculée, ordre de lecture, diagnostics. |

Les données dérivées peuvent être recalculées à l'ouverture. Elles ne constituent pas la source de vérité du fichier.

## 4. Organisation commune des voix

Les voix doivent partager une même chronologie de partition.

Le format ne doit pas permettre qu'une voix possède implicitement une mesure 2/4 pendant qu'une autre possède une mesure 3/4 au même emplacement sans relation explicite.

Chaque voix possède au minimum :

- un identifiant stable ;
- un nom libre ;
- une référence de portée indépendante du nom.

La référence de portée ne doit pas être confondue avec une tessiture, un registre vocal ou une catégorie SATB.

## 5. Fidélité aux règles rythmiques

Le futur modèle doit pouvoir représenter les conventions existantes :

- mesures délimitées ;
- unités séparées par `:` ;
- regroupements indiqués par `!` ;
- subdivisions explicites avec `.` et `,` ;
- parties vides représentant des silences lorsque la structure de division explicite les permet ;
- répartition implicite égale des notes et des prolongations lorsqu'aucun signe de division explicite n'est présent : chaque note et chaque `-` compte pour un élément de même durée, et leur somme remplit l'unité ;
- triolets de trois positions égales et sextolets de six positions égales, chacun occupant une unité native Sol-fa complète ;
- groupes rythmiques spécifiés ;
- prolongations `-` ;
- anacrouses et séparateurs au début d'un passage ;
- doubles barres facultatives et changements de référence.

Le format ne doit pas ajouter une règle générale pour les divisions rythmiques qui ne sont pas définies dans la conception.

La signature et la disposition doivent rester deux informations distinctes.

## 6. Fidélité à la hauteur

Le modèle doit pouvoir conserver séparément :

- la graphie Sol-fa ;
- le degré ;
- l'altération ;
- le déplacement d'octave ;
- la référence tonale active ;
- la hauteur absolue calculée, lorsqu'elle est nécessaire.

La représentation de la hauteur calculée ne doit pas devenir une normalisation de la graphie.

## 7. Paroles, accords et indications

Le format doit prévoir de représenter indépendamment :

- les paroles communes et leurs couplets ;
- les paroles propres à une voix ;
- les positions syllabiques par rapport aux attaques des notes ;
- les accords en lettres latines ;
- les accords Sol-fa relatifs à Do ;
- les degrés harmoniques en chiffres romains ;
- les indications de tonalité et de transition ;
- les repères et parcours de reprise ;
- les nuances, indications de tempo, articulations et ornements.

Les accords ne remplacent jamais les notes. Les indications de transition ne sont pas des notes supplémentaires jouées.

## 8. Contenu musical et présentation visuelle

Le fichier doit distinguer les faits musicaux de leur présentation :

- le choix d'une saisie compacte ou explicite est une modalité d'interaction avec l'éditeur, pas une règle musicale supplémentaire ;
- les différents modes de visualisation doivent présenter une même structure musicale sans en modifier les durées, les événements ou l'interprétation ;
- une préférence de saisie ou de visualisation ne doit pas créer une seconde logique rythmique ni remplacer les données musicales canoniques ;

- le crochet peut être affiché ou masqué sans modifier la musique ;
- les clés ou références de portée ne doivent pas modifier la graphie Sol-fa ;
- les paroles peuvent être affichées dessous ou entre des groupes de portées ;
- les systèmes et les pages peuvent être réorganisés sans changer l'ordre musical ;
- un saut de ligne ou de page ne modifie pas les durées ;
- le rendu typographique des octaves ne modifie pas leur valeur stockée.

## 9. Source de vérité et sérialisation

Il faudra choisir une stratégie explicite entre :

1. une source de notation textuelle conservée exactement et analysée à l'ouverture ;
2. un modèle d'événements structuré qui conserve aussi les graphies écrites ;
3. un modèle hybride où une représentation est canonique et l'autre est strictement dérivée.

Il faut éviter d'enregistrer deux représentations modifiables indépendamment, qui pourraient se contredire.

Une sauvegarde sans modification musicale doit être sans perte : les graphies, les positions et les annotations ne doivent pas être normalisées ou supprimées.

## 10. Compatibilité et validation

Le format devrait être accompagné :

- d'un schéma de validation ;
- d'exemples valides et invalides ;
- de tests de lecture et d'écriture aller-retour ;
- de tests de conservation des graphies ;
- de tests de partitions polyphoniques ;
- de tests couvrant les cas rythmiques et les indications musicales validés dans la conception.

Le Studio existant pourra servir de référence comportementale pour les cas déjà implémentés, sans que ses choix provisoires deviennent automatiquement des exigences du format.
