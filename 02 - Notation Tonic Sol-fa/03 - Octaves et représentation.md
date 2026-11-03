# Octaves et représentation

## État

<badge color="success">Validé</badge> Utilisation de suffixes numériques pour exprimer le déplacement d'octave dans la notation numérique de MireDo.

<badge color="warning">À préciser</badge> Règles complètes de validation, limites numériques et convention exacte de rendu.

## Convention numérique

Le nombre placé après le symbole indique un déplacement vers l'aigu :

| Écriture numérique | Interprétation |
|---|---|
| `d1` | `d` une octave plus haut |
| `r1` | `r` une octave plus haut |
| `m2` | `m` deux octaves plus haut |

Le nombre précédé d'un soulignement indique un déplacement vers le grave :

| Écriture numérique | Interprétation |
|---|---|
| `d_1` | `d` une octave plus bas |
| `s_2` | `s` deux octaves plus bas |

La même règle s'applique aux notes altérées :

- `di_1` : `di` une octave plus bas ;
- `di1` : `di` une octave plus haut.

## Rendu typographique souhaité

Le stockage et la saisie numériques doivent pouvoir être rendus sous une forme typographique avec exposant ou indice :

| Forme numérique | Rendu |
|---|---|
| `d1` | d¹ |
| `d_1` | d₁ |
| `di_1` | di₁ |
| `di1` | di¹ |

Le rendu est une représentation visuelle ; il ne doit pas modifier la valeur stockée ni la graphie de base.

## Relation avec la notation traditionnelle

La notation Tonic Sol-fa peut également utiliser des apostrophes pour les octaves supérieures et des virgules pour les octaves inférieures. MireDo privilégie une notation numérique explicite dans la saisie et les données, plus facile à taper et à parser.

Une couche de rendu pourra proposer une présentation inspirée de la notation traditionnelle.

## Préservation de l'identité

Une note comme `ti_1` peut produire une hauteur équivalente à un `d` situé dans une autre octave selon le contexte tonal. MireDo ne doit pas remplacer automatiquement `ti_1` par `d` : l'orthographe Sol-fa doit être conservée.

## Questions ouvertes

- Quel est le domaine numérique autorisé pour le déplacement d'octave ?
- Le suffixe `0` doit-il être accepté ou omis ?
- Comment gérer les espaces ou séparateurs entre note et suffixe ?
- Le rendu traditionnel apostrophe/virgule sera-t-il un thème alternatif ou une sortie dédiée ?
