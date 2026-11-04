# Analyse de la proposition initiale JSON

**Statut : analyse réalisée ; format non validé.**

## 1. Appréciation générale

L'idée d'utiliser JSON est pertinente pour un format natif : les métadonnées, les voix, les mesures et les annotations peuvent être organisées en objets et tableaux explicites. JSON est également lisible par les développeurs et exploitable par des outils externes.

Cependant, la proposition actuelle n'est pas encore un modèle cohérent de partition. Elle mélange des informations musicales, des propriétés de voix, des mesures et des fragments de notation textuelle. Plusieurs champs sont ambigus ou contredisent les conventions actuellement retenues par MireDo.

**Conclusion : conserver JSON comme candidat sérieux, mais ne pas adopter la structure proposée telle quelle.** Il faut d'abord clarifier le modèle logique de la partition.

## 2. Analyse champ par champ

| Élément proposé | Analyse | Recommandation |
|---|---|---|
| `metadata.title` | Correct : titre de l'œuvre. | Conserver. |
| `metadata.composer` | Correct : nom du compositeur. | Conserver. |
| `metadata.description` | Utile pour une description libre. | Facultatif. |
| `key: "Do = D"` | Mélange la référence tonale et son libellé d'affichage. La conception définit une référence `A` à `G`, éventuellement altérée avec `b` ou `#`. Elle ne définit pas le mode majeur ou mineur à partir de cette valeur. | Enregistrer la référence sous une valeur non ambiguë, par exemple `reference_tone: "D"`. Garder le libellé visuel dans les préférences d'affichage, s'il est nécessaire. |
| `time_signature` | La signature rythmique est une propriété de la partition dans la conception actuelle ; elle ne doit pas être répétée indépendamment dans chaque voix. | La placer dans le contexte métrique commun. La possibilité de la modifier par section ou mesure reste à décider. |
| `voices` | Le tableau de voix est cohérent avec les partitions polyphoniques. | Conserver un identifiant stable par voix. |
| `name` | Le nom de la voix est libre : Soprano, Alto, Ténor, Basse, Voix 1, etc. | Conserver. |
| `range: "SATB"` | Incorrect sémantiquement. SATB désigne une organisation chorale, pas l'étendue vocale d'une voix individuelle. La conception sépare le nom de la voix, sa référence de portée et son registre. | Supprimer ce champ sous cette forme. Représenter la référence de portée séparément. Une éventuelle tessiture pourra être étudiée plus tard. |
| `measures` dans chaque voix | Cette organisation duplique la chronologie des mesures dans chaque voix et peut produire des numéros, signatures ou nombres de mesures incohérents entre voix. | Construire une chronologie de mesures commune à la partition ; chaque mesure contient les données de toutes les voix concernées. |
| `number` | Le numéro est utile à l'affichage, mais peut être déduit de l'ordre des mesures. Les anacrouses et les reprises peuvent compliquer la numérotation affichée. | Distinguer l'identifiant stable de la mesure du numéro d'affichage, qui peut être calculé ou explicitement configuré. |
| `notation` | Conserver la notation Sol-fa sous forme de texte est une solution simple pour un premier modèle et permet de garder les graphies saisies. Mais cela signifie que le contenu musical doit encore être analysé par une grammaire. | Conserver éventuellement un fragment de notation écrit exact au début ; définir ensuite comment les événements structurés et le texte source coexistent sans devenir deux sources de vérité. |

## 3. Incompatibilités avec les conventions Sol-fa retenues

### 3.1 La virgule de `d,` n'est pas une octave dans la saisie MireDo actuelle

L'exemple utilise `d,` pour représenter une note grave.

Or la conception de MireDo retient les suffixes numériques pour saisir les octaves :

- `d1` : une octave plus haut ;
- `d_1` : une octave plus bas ;
- `di_1` : degré altéré d'un demi-ton vers le haut, une octave plus bas.

La virgule `,` possède déjà une fonction rythmique dans la notation décrite : elle subdivise une partie d'unité. Le Studio l'analyse comme un jeton de subdivision, et non comme un suffixe d'octave.

La notation traditionnelle peut employer des virgules pour représenter certaines octaves graves, mais la conception MireDo privilégie une saisie numérique explicite. Le rendu traditionnel reste une couche de présentation.

**Correction recommandée dans l'exemple :** écrire `d_1` pour la note grave, et réserver `,` à sa fonction rythmique.

### 3.2 Le regroupement habituel de 4/4 n'apparaît pas

La conception décrit `!` comme séparateur des deux moitiés égales d'une mesure lorsque sa disposition le prévoit.

Pour 4/4, la disposition habituelle est 2 + 2 :

```text
|d:r!m:f|
```

L'exemple `|d:r:m:f|` contient bien quatre unités, mais ne montre pas le séparateur habituel de regroupement. Il ne doit donc pas être présenté comme l'exemple canonique du 4/4 sans préciser une disposition alternative.

Les exemples en 3/4 et 2/4, sans `!`, sont cohérents avec les dispositions habituelles décrites.

### 3.3 L'objet numéroté « mesure 1 » contient en réalité deux mesures

Dans l'exemple Soprano :

```text
| d : r : m : f | s : - : m : - |
```

Deux séquences délimitées par des barres sont présentes. Il en va de même pour les autres objets proposés.

Un objet nommé `measure` doit représenter une seule mesure. Sinon, son numéro et sa signature ne permettent plus de savoir à quelle mesure ils s'appliquent.

**Correction recommandée :** séparer chacune des séquences musicales en un objet de mesure distinct. Si l'intention est de grouper plusieurs mesures, il faudra choisir un nom comme `section` ou `phrase`, et conserver les mesures à l'intérieur.

### 3.4 Les changements de signature ne sont pas encore une règle validée

L'exemple passe de 4/4 à 3/4 puis à 2/4 au cours de la même partition.

Dans la conception actuelle :

- la signature est déclarée pour la partition ;
- la disposition habituelle dépend de cette signature ;
- une disposition alternative choisie par le compositeur s'applique à toute la partition ;
- le Studio expose actuellement une seule signature dans son en-tête.

La possibilité de changer de signature par section ou par mesure n'est pas définie dans les règles validées.

Le format pourrait prévoir une extension pour le stockage de tels changements, mais cette capacité de stockage ne doit pas être interprétée comme une autorisation musicale déjà décidée.

### 3.5 Les sept degrés et leurs graphies doivent rester libres

Le format ne doit pas se limiter à `d r m f s l t` sans altérations.

Il doit permettre de préserver :

- les formes montantes avec `i` ;
- les formes descendantes valides avec `a`, `e` ou `o` ;
- les formes rares mais valides ;
- les suffixes numériques d'octave ;
- les orthographes enharmoniques distinctes.

Une note comme `mi` ne doit jamais être réécrite automatiquement en `f`, même si les deux graphies produisent une hauteur équivalente.

## 4. Le modèle ne couvre pas encore toute une partition

Le modèle proposé ne décrit pas encore explicitement plusieurs éléments déjà présents dans la conception :

| Élément à représenter | Besoin issu de la conception |
|---|---|
| Référence de portée par voix | Chaque voix possède une référence numérique indépendante de son nom. |
| Signature et disposition | Elles sont distinctes et la disposition peut être choisie pour la partition. |
| Anacrouse et séparateurs | Le début d'une mesure peut être décalé ; `:`, `!` et les barres ont des rôles distincts. |
| Subdivisions et silences | `.`, `,`, les parties vides et les notes collées déterminent les durées. |
| Prolongations | `-` prolonge la note précédente et peut traverser des unités ou des mesures. |
| Changement de référence | Des changements et indications de transition peuvent apparaître à une position musicale précise. |
| Accords | Les chiffres romains, accords latins et accords Sol-fa sont facultatifs et distincts des notes. |
| Paroles | Paroles communes, couplets supplémentaires et paroles propres à une voix doivent être représentables. |
| Reprises et indications | Segno, D.C., D.S., Fine, Coda, To Coda, nuances, tempo, articulations et point d'orgue. |
| Mise en page | Retours à la ligne, sauts de page, crochets, groupes de portées et emplacement des paroles. |

Toutes ces informations ne doivent pas nécessairement être placées dans le même objet JSON. Certaines relèvent de la partition musicale, d'autres de son affichage.

## 5. Recommandation

La piste recommandée est un **JSON structuré autour de la partition entière et de sa chronologie commune** :

1. les métadonnées sont séparées du contexte musical ;
2. le contexte musical contient le système de notation et la référence tonale ;
3. les voix sont déclarées une fois, avec leur nom et leur référence de portée ;
4. les mesures sont déclarées une fois au niveau de la partition ;
5. chaque mesure contient le fragment ou les événements de chaque voix ;
6. les paroles, accords, reprises et indications sont associés à des positions musicales explicites ;
7. les options de mise en page sont séparées du contenu musical.

La conservation d'une chaîne de notation écrite peut constituer une première étape pragmatique. Une représentation structurée des événements pourra être définie ensuite, à condition de préserver exactement les graphies et la sémantique validées.

## 6. Conclusion

JSON est une bonne direction à explorer, mais la structure fournie n'est pas prête à devenir le format natif de MireDo.

Les corrections prioritaires sont :

- séparer la référence tonale de son libellé ;
- remplacer `d,` par une saisie d'octave non ambiguë, ici `d_1` ;
- intégrer les regroupements `!` usuels dans l'exemple 4/4 ;
- faire correspondre chaque objet `measure` à une seule mesure réelle ;
- centraliser la chronologie des mesures au niveau de la partition ;
- décider explicitement si les signatures peuvent changer pendant une partition ;
- définir la représentation des éléments musicaux et éditoriaux manquants.

Aucune de ces propositions techniques ne modifie les règles musicales déjà validées.
