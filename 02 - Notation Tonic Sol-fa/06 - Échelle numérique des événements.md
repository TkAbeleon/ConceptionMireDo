# Échelle numérique des événements — ensemble ℤ

<badge color="success">Convention de représentation</badge>

Ce document décrit l'échelle entière utilisée pour représenter les événements musicaux de MireDo. Elle rassemble dans un même espace numérique les **hauteurs de notes**, les **silences** et les **prolongations**.

Il complète deux domaines qui restent distincts dans leur sens musical :

- [[05 - Représentation numérique des hauteurs]] décrit l'axe chromatique des hauteurs ;
- [[05 - Rythme et durée]] décrit les positions, les durées, les silences et les prolongations dans l'unité native Tonic Sol-fa.

L'entier enregistré pour un événement est un **code d'événement**. Il ne faut pas le confondre avec la coordonnée chromatique de la hauteur.

## 1. Ensemble des valeurs

L'échelle utilise l'ensemble des entiers relatifs :

**ℤ = { …, -5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5, … }**

Deux valeurs négatives sont réservées aux événements qui ne portent pas de hauteur :

| Code | Signification | Nature |
|---:|---|---|
| **-1** | Silence | Événement temporel sans hauteur |
| **-2** | Prolongation | Segment qui prolonge la note précédente |

Toutes les autres valeurs représentent une hauteur de note selon la correspondance définie ci-dessous.

## 2. Valeurs représentant les hauteurs

### 2.1 Référence et valeurs positives ou nulles

La référence chromatique conserve la convention de [[05 - Représentation numérique des hauteurs]] :

- **0** représente la note de référence **d** ;
- chaque demi-ton vers l'aigu ajoute 1 ;
- les valeurs positives poursuivent l'axe chromatique vers l'aigu.

Exemples :

| Code d'événement | Graphie de référence |
|---:|---|
| 0 | **d** |
| 1 | **di** |
| 2 | **r** |
| 3 | **ri** |
| 4 | **m** |
| 5 | **f** |
| 6 | **fi** |
| 7 | **s** |
| 8 | **si** |
| 9 | **l** |
| 10 | **te** |
| 11 | **t** |
| 12 | **d'** |

### 2.2 Valeurs négatives représentant les hauteurs graves

Les codes **-1** et **-2** étant réservés au silence et à la prolongation, les hauteurs situées sous la référence utilisent les valeurs à partir de **-3**.

La correspondance est décalée de deux unités pour ces seules valeurs :

**Coordonnée chromatique = code d'événement + 2**, lorsque le code est inférieur ou égal à -3.

Exemples :

| Code d'événement | Coordonnée chromatique | Graphie de référence |
|---:|---:|---|
| -3 | -1 | **t_1** |
| -4 | -2 | **te_1** |
| -5 | -3 | **l_1** |
| -6 | -4 | **si_1** |

La progression continue vers le grave sans borne théorique. Les graphies exactes restent soumises aux règles d'altération, d'octave et de conservation orthographique déjà définies dans les documents de notation.

## 3. Place du silence : code -1

Le code **-1** représente un silence.

Un silence :

- occupe une portion de temps dans l'unité native ;
- possède une position de début et une durée calculée comme les autres événements temporels ;
- ne possède aucune hauteur chromatique ;
- ne déclenche aucune attaque de note.

Le silence n'est donc pas une hauteur négative. Il s'agit d'un type d'événement distinct, identifié par sa valeur réservée.

Dans la notation Tonic Sol-fa décrite dans [[05 - Rythme et durée]], le silence peut notamment résulter d'une portion laissée vide par une subdivision explicite. Il ne faut pas ajouter un symbole de note pour représenter cette portion.

## 4. Place de la prolongation : code -2

Le code **-2** représente une prolongation de la note précédente.

Une prolongation :

- occupe une position rythmique ;
- ne crée pas une nouvelle attaque ;
- ne représente pas une nouvelle hauteur ;
- augmente la durée totale de la note qu'elle prolonge.

La prolongation doit rester rattachée à la note concernée. Elle ne doit pas être interprétée comme un silence, même si elle ne produit pas de nouvelle attaque.

La structure temporelle conserve les segments d'origine de la note prolongée. La durée totale de cette note est calculée en réunissant sa durée initiale et les durées de ses segments de prolongation. Cette distinction préserve à la fois le résultat temporel et l'écriture source.

## 5. Lecture commune des trois catégories

| Catégorie | Valeurs | Interprétation |
|---|---|---|
| Hauteur de note aiguë ou de référence | 0 et valeurs positives | Coordonnée chromatique directe |
| Hauteur de note grave | Valeurs inférieures ou égales à -3 | Coordonnée chromatique obtenue en ajoutant 2 au code |
| Silence | -1 | Portion temporelle sans hauteur |
| Prolongation | -2 | Portion temporelle rattachée à la note précédente |

Cette organisation permet de représenter les différents événements dans un même ensemble de valeurs entières, tout en maintenant leur interprétation distincte.

## 6. Ne pas confondre code, position et durée

Le code d'événement indique **ce qui occupe une position** : une hauteur, un silence ou une prolongation.

Il ne donne pas à lui seul :

- la position temporelle de l'événement dans l'unité ;
- la durée de l'événement ;
- le dénominateur de division de l'unité ;
- la graphie Sol-fa originale lorsque celle-ci doit être conservée séparément.

Les positions et les durées restent régies par les fractions exactes décrites dans [[05 - Rythme et durée]]. Les codes d'événement ne remplacent donc pas l'index temporel.

## 7. Exemples de lecture

Pour une suite d'événements dont les codes sont **[0, -1, 2]**, la lecture des catégories est :

1. note **d** ;
2. silence ;
3. note **r**.

Pour une suite **[0, -2, 2]**, la lecture est :

1. attaque de la note **d** ;
2. prolongation de cette même note ;
3. attaque de la note **r**.

Dans le second exemple, la prolongation ne constitue pas une note supplémentaire : elle augmente la durée de **d** avant l'attaque de **r**.

Ces exemples illustrent uniquement le sens des codes. Les positions et les durées exactes doivent être déterminées par la structure rythmique de l'unité.

## 8. Règles de conservation

- La valeur **-1** reste réservée au silence.
- La valeur **-2** reste réservée à la prolongation.
- Les codes de hauteur ne doivent jamais utiliser ces deux valeurs réservées.
- Une hauteur grave utilise le décalage indiqué dans la section 2.2.
- Le code numérique ne remplace pas la graphie Sol-fa originale.
- Le code numérique ne remplace ni la position temporelle ni la durée.
- Une prolongation reste liée à la note qu'elle prolonge.

Le schéma JSON définitif du fichier **.mrd** et les noms de ses propriétés ne sont pas définis par ce document.
