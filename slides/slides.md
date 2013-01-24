% Algorithmes génétiques
% Quentin de Laroussilhe - Guillaume Sanchez

# Optimisation

## Qu'est-ce que l'optimisation ?

### Définition formelle

\footnotetext[1]{Si E est un ensemble tel que $dim(E) \geq 1$ on parle
d'optimisation combinatoire.}
\footnotetext[2]{Ah oui très bien !}

Soit E un ensemble et $f : E \to \mathbb{R}$

#### Minimisation

Trouver $y \in E$ tel que $\forall x \in E, f(y) \leq f(x)$

#### Maximisation

Trouver $y \in E$ tel que $\forall x \in E, f(y) \geq f(x)$

### Définition un peu moins formelle...

Trouver le meilleur élément d'un ensemble par rapport à une fonction de coût/de
score permettant d'évaluer chaque élément de cet ensemble.

#### Exemples

* Trouver le meilleur prix pour un article donné
* Agencer des photos dans une gallerie pour avoir le résultat le plus joli
* Trouver le plus court chemin entre deux villes
* Chercher les meilleurs paramètres pour une intelligence artificielle

## Quand

### Ce qui est connu

Mais euh ! On connaît déjà

* A
* Parcours largeur
* Parcours profondeur
* Bob le Bricoleur
* Dijkstra

Alors vazzy monsieur kes tu nou pran la taite ?

### Du calme jeune homme fougueux

* Recherche exhaustive trop coûteuse
* L'optimalité n'est pas requise

### Prérequis

* $\forall x \in E \exists!y f(x) = y$
