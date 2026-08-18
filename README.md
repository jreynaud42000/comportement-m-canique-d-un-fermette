# Fermette — simulation du comportement mécanique

Application web autonome (un seul fichier) pour le thème **« La validation du comportement
mécanique d'un matériau »** du *projet d'aménagement des programmes de technologie du cycle 4*
(juin 2025), complété par le thème **« Le choix des matériaux »**.

Ouvrir [index.html](index.html) dans un navigateur. Aucune installation, aucun serveur,
aucune dépendance externe.

## Progression 5ᵉ → 4ᵉ → 3ᵉ

Le sélecteur de niveau en haut de l'écran verrouille ou déverrouille l'interface pour coller
à l'attendu de chaque classe.

| Niveau | Attendu du programme | Dans l'application |
|---|---|---|
| **5ᵉ** | Identifier la nature des sollicitations ; **utiliser** une simulation fournie ; protocole de test fourni | Tous les paramètres sont verrouillés. L'élève lit l'onglet *Sollicitations*, relève la déformation et saisit sa mesure expérimentale. |
| **4ᵉ** | **Paramétrer** la simulation : *nature du matériau* et *dimensions* | Bibliothèque de 12 matériaux et sections des barres déverrouillées ; onglet *Comparer les matériaux*. |
| **3ᵉ** | **Explorer aux frontières des exigences** les limites de charge et de déformation | Géométrie et charges déverrouillées ; onglet *Limites* : facteur k et charge maximale supportable. |
| **Expert** | (hors programme collège) | Neige EN 1991‑1‑3, vent EN 1991‑1‑4, combinaisons Eurocode, réactions d'appui. |

L'onglet *Objectifs du programme* rappelle, pour chaque niveau, les objectifs d'apprentissage
et où ils se travaillent dans l'application.

## Ce que calcule la simulation

Treillis plan à **nœuds articulés** résolu par la **méthode des rigidités** (`K·u = F`,
élimination de Gauss avec pivot partiel). Chaque barre est un ressort de raideur `E·A/L`.

Résultats produits :

- **sollicitation** de chaque barre — traction ou compression (les quatre modes du programme,
  *flexion, torsion, traction, compression*, sont présentés et situés) ;
- **déformation** : flèche maximale, déplacement de chaque nœud, allongement de chaque barre,
  forme déformée amplifiée sur le schéma ;
- **critère de déformation autorisée** (portée/200, /300, /400 ou valeur libre) avec verdict ;
- **taux de travail** σ / σ<sub>adm</sub> par barre ;
- **écart réel / simulé** à partir de la mesure expérimentale saisie ;
- **comparaison multicritère des matériaux** : rigidité, résistance, masse, empreinte carbone,
  fin de vie.

## Retirer une barre pour comprendre la triangulation

**Un clic sur une barre du schéma la retire** (croix rouge), un second clic la remet.
Le bouton *Tout rétablir* remonte la fermette complète.

La fermette étant **isostatique**, retirer n'importe quelle barre la transforme en **mécanisme** :
l'application le détecte en analysant le rang de la matrice de rigidité, calcule le **mode
d'effondrement** (noyau de la matrice) et l'**anime en rouge** sur le schéma. Le décompte de
stabilité `b + r` face à `2 × n` est affiché, ainsi que le nombre de degrés de liberté gagnés.

C'est la démonstration directe de la triangulation — et le cas du **poinçon**, dont l'effort est
nul sous neige seule mais dont le retrait fait s'effondrer la structure, montre qu'une barre à
effort nul n'est pas une barre inutile.

## Deux situations d'étude

- **Charpente réelle** — couverture, plafond et neige répartis sur l'entraxe des fermettes.
- **Maquette d'essai** — charges de toiture désactivées, une charge ponctuelle (en N ou en kg)
  appliquée au nœud choisi, pour confronter la simulation à un essai en classe.

## Matériaux

Bois résineux C24, lamellé‑collé GL24h, contreplaqué, balsa, carton fort, bambou, PLA, ABS,
PVC, acier S235, aluminium 6060, béton C25/30 — avec E, masse volumique, contraintes
admissibles, empreinte carbone et filière de fin de vie. **Valeurs indicatives à usage
pédagogique**, pas des valeurs de dimensionnement réglementaire.

## Limites du modèle

- La **flexion locale** d'une barre entre deux nœuds n'est pas calculée (charges ramenées aux nœuds) :
  la flèche réelle d'une fermette est donc supérieure à la valeur simulée.
- Le comportement des **assemblages** (connecteurs, clous, colle) et le **flambement** des barres
  comprimées ne sont pas modélisés.
- Aucune vérification Eurocode 5 : les contraintes admissibles sont des valeurs pédagogiques.

Ces limites sont exactement ce qui alimente la discussion sur **l'écart entre le réel et le simulé**
attendue par le programme.
