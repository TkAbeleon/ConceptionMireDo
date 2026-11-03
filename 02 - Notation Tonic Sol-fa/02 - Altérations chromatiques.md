# Altérations chromatiques

## État des règles

<badge color="success">Validé</badge> Principe de l'altération ascendante par ajout de `i`.

<badge color="warning">Partiel</badge> Principe de l'altération descendante par voyelle ; choix exact à préciser selon le degré et la convention retenue.

## Altération ascendante

L'ajout de la voyelle `i` au symbole du degré indique une élévation d'un demi-ton :

| Degré | Forme altérée |
|---|---|
| `d` | `di` |
| `r` | `ri` |
| `m` | `mi` |
| `f` | `fi` |
| `s` | `si` |
| `l` | `li` |
| `t` | `ti` |

## Altération descendante

Pour abaisser un degré d'un demi-ton, une voyelle parmi `a`, `e` ou `o` est utilisée selon la syllabe et la convention.

Exemple confirmé par l'utilisateur : le degré `t` abaissé peut être écrit `te`, `ta` ou `to`, selon la variante utilisée.

**Important :** la forme descendante exacte de chaque degré n'est pas encore arrêtée dans la conception MireDo. Ne pas générer automatiquement une table complète de formes sans validation.

## Exemple de séquence

Une séquence couramment rencontrée dans la convention décrite est :

`d di r ri m f fi s si l te`

La forme `te` peut avoir les variantes `ta` ou `to` selon l'usage.

## Orthographe et équivalence sonore

Une note altérée peut produire la même hauteur en tempérament égal qu'un autre degré écrit. Cela ne justifie pas de remplacer automatiquement sa graphie.

Exemple : `mi` (Mi augmenté) et `f` (Fa) peuvent correspondre à la même hauteur sonore dans un contexte tempéré, mais leur identité Sol-fa écrite reste distincte.

MireDo doit donc séparer :
1. la graphie saisie ;
2. le degré et l'altération interprétés ;
3. la hauteur absolue calculée.

## Signes accidentels

Dans la convention décrite par l'utilisateur, on n'ajoute pas de symbole autonome de bécarre à la notation Sol-fa. Les syllabes Sol-fa et leurs formes altérées sont utilisées directement.

Les symboles conventionnels `♮`, `♯` et `♭` ne doivent donc pas être introduits comme signes écrits de cette notation sans décision explicite.

## Questions ouvertes

- Quelle forme descendante retenir par défaut pour chaque degré ?
- Les variantes `te`, `ta`, `to` doivent-elles être toutes acceptées en entrée ?
- Le parseur doit-il conserver la variante exacte saisie lors d'une sérialisation ?
