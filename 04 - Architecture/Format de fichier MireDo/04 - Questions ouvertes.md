# Questions ouvertes — Format de fichier MireDo

Aucune question de cette page n'est considérée comme décidée par le seul fait qu'un champ apparaisse dans un exemple JSON.

## 1. Conteneur et extension

- [ ] Le fichier natif sera-t-il directement un document JSON ?
- [ ] L'extension `.mrd` contiendra-t-elle ce JSON, ou restera-t-elle associée à une autre représentation ?
- [ ] Faut-il permettre une archive contenant le document, les images, les polices ou d'autres ressources liées à la partition ?
- [ ] Quelle politique de versionnement et de migration sera adoptée ?

## 2. Source de vérité musicale

- [ ] La source canonique sera-t-elle une notation textuelle exacte, un modèle d'événements structuré, ou un modèle hybride ?
- [ ] Si une chaîne de notation est conservée, sa granularité sera-t-elle le morceau, la section, la mesure ou l'unité ?
- [ ] Comment préserver exactement l'écriture, l'ordre des jetons et les annotations après une modification partielle ?
- [ ] Les espaces, commentaires et choix de présentation textuelle doivent-ils être conservés à l'identique ?

## 3. Mesures et signatures

- [ ] Une partition peut-elle changer de signature rythmique au cours du morceau ?
- [ ] Si oui, le changement se fait-il par section, par mesure ou aux deux niveaux ?
- [ ] La disposition rythmique alternative reste-t-elle obligatoirement globale à la partition, comme dans la conception actuelle, ou peut-elle être définie par section ?
- [ ] Comment stocker les anacrouses, les mesures incomplètes, les doubles barres et les barres placées au milieu d'une mesure ?
- [ ] Les numéros de mesure sont-ils calculés ou configurables ?

## 4. Voix et organisation polyphonique

- [ ] Le modèle canonique stockera-t-il les mesures communes avec les données de chaque voix, ou des pistes indépendantes référencées par position ?
- [ ] Comment représenter les voix qui commencent plus tard, s'arrêtent temporairement ou ont des longueurs différentes ?
- [ ] Faut-il prévoir une propriété de rôle vocal (S, A, T, B) distincte du nom et de la référence de portée ?
- [ ] La tessiture ou le registre vocal doivent-ils être enregistrés, et selon quelle définition ?

## 5. Notes et rythme

- [ ] Définir, pour la notation textuelle Tonic Sol-fa, les conventions de saisie des divisions qui ne sont pas encore documentées et les cas combinant ces groupes avec des silences ou des prolongations. Le modèle temporel MireDo peut déjà représenter toute division entière positive N ; cette capacité interne ne préjuge pas de la syntaxe conventionnelle de la notation source.

- [ ] Une première version conservera-t-elle les fragments de notation Sol-fa comme chaînes, ou utilisera-t-elle immédiatement des jetons structurés ?
- [ ] Quelle représentation structurée conservera les divisions explicites et les portions silencieuses qu'elles délimitent ? La répartition implicite sans signe de division est définie : elle répartit l'unité entre notes et prolongations, sans possibilité d'y insérer un silence.
- [ ] Comment conserver les formes rares et la graphie exacte des notes ?
- [ ] Quels champs seront calculés à l'ouverture plutôt qu'enregistrés ?
- [ ] Comment représenter dans le modèle logique les groupes de trois et six positions, leurs courbes graphiques et les prolongations qui occupent certaines positions ? Les règles musicales de durée sont documentées dans la référence Tonic Sol-fa.

### 5.1 Références temporelles — décisions validées

**Statut : validé par l'utilisateur.** Le modèle distingue deux références complémentaires qui ne doivent pas être confondues.

#### Unité native Tonic Sol-fa — référence structurelle des durées

- Les durées exactes sont exprimées par des fractions de l'unité principale délimitée par `:`.
- La valeur de cette unité dépend du dénominateur de la signature, conformément aux conventions documentées dans [[../../02 - Notation Tonic Sol-fa/05 - Rythme et durée]].
- Cette référence organise la hiérarchie des mesures, unités, subdivisions et événements.

#### Noire — référence conventionnelle du tempo

- Les indications de tempo sont exprimées en noires par minute : `♩ = valeur`.
- Le tempo initial, lorsqu'il est défini, est enregistré dans le contexte musical de la partition.
- Tout changement de tempo est enregistré à sa position exacte dans la chronologie commune.
- La référence de noire par minute reste la même, quelle que soit la signature rythmique ou l'unité native Sol-fa.

#### Conséquence

La noire n'est pas l'unité structurelle des subdivisions Sol-fa. L'unité native Sol-fa ne remplace pas la référence conventionnelle du tempo.

Un changement de signature et un changement de tempo sont deux informations distinctes. Ils peuvent être positionnés au même endroit dans la partition, sans être confondus.

## 6. Référence tonale et hauteur

- [ ] Comment représenter les changements de référence tonale à une position précise ?
- [ ] Faut-il distinguer explicitement référence Sol-fa, centre tonal et éventuelle tonalité harmonique ?
- [ ] Comment enregistrer les indications de transition sans les confondre avec les notes jouées ?
- [ ] Quelle partie du calcul de hauteur absolue doit être conservée dans le fichier, si nécessaire ?

## 7. Paroles et annotations

- [ ] Comment identifier les couplets et leurs lignes communes ?
- [ ] Comment relier les syllabes aux attaques musicales de manière durable ?
- [ ] Comment enregistrer les paroles propres à une voix ?
- [ ] Comment représenter les accords latins, Sol-fa et chiffres romains ?
- [ ] Définir, lors de la conception technique, les structures de stockage, propriétés, paramètres et liens d'association des reprises, nuances, articulations, ornements et points d'orgue. Leur cadrage fonctionnel et leurs familles sont déjà validés dans [[../../02 - Notation Tonic Sol-fa/07 - Reprises et indications musicales]].

## 8. Mise en page et ressources

- [ ] Comment proposer dans l'éditeur le choix entre saisie compacte et saisie explicite, sans en faire deux logiques musicales distinctes ?
- [ ] Quelles visualisations permettront de présenter une même structure musicale sous différentes formes sans modifier son interprétation ?
- [ ] Les préférences de présentation seront-elles enregistrées dans le fichier natif ou dans un profil séparé ?
- [ ] Comment représenter les groupes de portées, les crochets, les clés affichées et la position des paroles ?
- [ ] Les retours de système et sauts de page manuels seront-ils stockés comme indications de mise en page ?
- [ ] Comment gérer les polices, images, annotations graphiques ou ressources externes ?

## 9. Validation et interopérabilité

- [ ] Quel schéma JSON permettra de valider la structure ?
- [ ] Comment les versions futures ignoreront-elles ou préserveront-elles les champs inconnus ?
- [ ] Quels tests garantiront qu'une ouverture puis sauvegarde conserve la graphie et le contenu ?
- [ ] Quels formats d'import/export doivent être prioritaires après le format natif ?

## Priorités recommandées

Avant de définir un schéma JSON complet, résoudre dans cet ordre :

1. Choisir la source de vérité (texte écrit ou événements structurés).
2. Définir l'organisation commune des mesures et des voix.
3. Décider si les signatures et dispositions peuvent changer pendant la partition.
4. Définir la représentation exacte des notes, unités, séparateurs, subdivisions et barres.
5. Ajouter les paroles, accords, indications, reprises et options de mise en page.
6. Définir versionnement, validation et tests aller-retour.
