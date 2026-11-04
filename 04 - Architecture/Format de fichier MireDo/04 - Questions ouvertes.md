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

- [ ] Une première version conservera-t-elle les fragments de notation Sol-fa comme chaînes, ou utilisera-t-elle immédiatement des jetons structurés ?
- [ ] Comment représenter les subdivisions et les silences non encore spécifiés par la conception ?
- [ ] Comment conserver les formes rares et la graphie exacte des notes ?
- [ ] Quels champs seront calculés à l'ouverture plutôt qu'enregistrés ?
- [ ] Comment les groupes rythmiques et les prolongations seront-ils reliés aux unités et mesures ?

### 5.1 Unité temporelle de référence — décision ouverte

**Statut : non décidé.** Deux options sont étudiées pour exprimer les fractions exactes de durée dans le modèle logique.

#### Option A — La noire comme unité de référence

**Avantages :**
- unité conventionnelle familière dans les logiciels de notation et les représentations musicales classiques ;
- échanges et conversions potentiellement plus directs avec MIDI et les outils qui expriment les durées en noires ou fractions de noire ;
- même unité de référence quelle que soit la signature rythmique.

**Inconvénients :**
- la durée de l'unité native Sol-fa doit être convertie avant d'être exprimée dans le modèle ;
- la relation entre l'organisation écrite avec les séparateurs `:` et les durées stockées est moins immédiate ;
- la conversion ajoute une étape conceptuelle et technique au traitement de la notation source.

#### Option B — L'unité native Tonic Sol-fa comme unité de référence

L'unité native désigne ici l'unité principale délimitée par `:`. Sa valeur dépend du dénominateur de la signature, conformément aux conventions documentées dans [[../../02 - Notation Tonic Sol-fa/05 - Rythme et durée]].

**Avantages :**
- correspondance directe entre la structure rythmique écrite et la hiérarchie du modèle ;
- subdivisions et prolongations exprimables naturellement comme fractions d'une unité native ;
- interprétation et inspection du modèle plus proches de la notation source Tonic Sol-fa.

**Inconvénients :**
- une même fraction n'a pas nécessairement la même durée absolue lorsque le dénominateur de la signature change ;
- les échanges avec MIDI et les outils fondés sur la noire nécessitent une conversion ;
- les opérations entre mesures de signatures différentes doivent tenir compte de la valeur réelle de l'unité native dans chaque contexte.

#### Recommandation de conception — non approuvée

La recommandation actuelle est de retenir l'unité native Tonic Sol-fa comme référence structurelle du modèle, tout en prévoyant une conversion exacte vers la noire pour les échanges externes.

Cette approche privilégie la fidélité à la notation que MireDo doit représenter, sans empêcher l'interopérabilité. Elle ne devient pas une décision tant que l'utilisateur ne l'a pas explicitement confirmée.

**Question à trancher :** les fractions exactes de durée doivent-elles être exprimées par rapport à la noire ou par rapport à l'unité native Tonic Sol-fa ?

## 6. Référence tonale et hauteur

- [ ] Comment représenter les changements de référence tonale à une position précise ?
- [ ] Faut-il distinguer explicitement référence Sol-fa, centre tonal et éventuelle tonalité harmonique ?
- [ ] Comment enregistrer les indications de transition sans les confondre avec les notes jouées ?
- [ ] Quelle partie du calcul de hauteur absolue doit être conservée dans le fichier, si nécessaire ?

## 7. Paroles et annotations

- [ ] Comment identifier les couplets et leurs lignes communes ?
- [ ] Comment relier les syllabes aux attaques musicales de manière durable ?
- [ ] Comment enregistrer les paroles propres à une voix ?
- [ ] Comment représenter les accords latins, Sol-fa et chiffres romains sur la chronologie ?
- [ ] Comment représenter les reprises, nuances, tempos, articulations, ornements et points d'orgue ?

## 8. Mise en page et ressources

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
