# Octaves et représentation

## État

<badge color="success">Validé</badge> Utilisation de suffixes numériques pour exprimer le déplacement d'octave dans la notation numérique de MireDo.

<badge color="warning">À préciser</badge> Référence exacte à partir de laquelle le déplacement est compté, règles complètes de validation, limites numériques et convention exacte de rendu.

## Convention numérique établie

Les formes suivantes ont été données et validées comme exemples de notation :

| Écriture numérique | Sens établi |
|---|---|
| `d1` | `d` une octave plus haut |
| `r1` | `r` une octave plus haut |
| `m2` | `m` deux octaves plus haut |
| `d_1` | `d` une octave plus bas |
| `s_2` | `s` deux octaves plus bas |
| `di_1` | `di` une octave plus bas |
| `di1` | `di` une octave plus haut |

Le nombre exprime un déplacement en octaves ; le suffixe positif indique le sens aigu et le nombre précédé d'un soulignement indique le sens grave.

**Point non encore établi :** l'octave ou la hauteur de référence par rapport à laquelle ce déplacement est calculé. Ne pas supposer que l'absence de suffixe définit à elle seule une octave de référence précise. La question doit être clarifiée avec des exemples concrets avant de spécifier le modèle ou le calcul.

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

- Quelle est la référence exacte utilisée pour calculer le déplacement d'octave ?
- Quel est le domaine numérique autorisé pour le déplacement d'octave ?
- Le suffixe `0` doit-il être accepté ou omis ?
- Comment gérer les espaces ou séparateurs entre note et suffixe ?
- Le rendu traditionnel apostrophe/virgule sera-t-il un thème alternatif ou une sortie dédiée ?
