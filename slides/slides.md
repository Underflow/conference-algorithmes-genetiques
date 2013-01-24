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

* A\*
* Parcours largeur
* Parcours profondeur
* Bob le Bricoleur
* Dijkstra

Alors vazzy monsieur kes tu nou pran la taite ?

### Du calme jeune homme fougueux

* Recherche exhaustive trop coûteuse
* L'optimalité n'est pas requise

### Prérequis

* $\forall x \in E \exists!y \in \mathbb{R} f(x) = y$
* $\forall x \in E \exists y \in E^{n} Succ(x) = y$

## Let's go fuckin code

### Hill-Climbling

~~~
HillClimbing(initial) : State
  current = initial
  forever
    next = BestSuccessor(initial)
    if Score(next) < Score(current) then
        return current
    current = next
~~~

#### Savokoi

* Rapide
* Simple
* Mais extremum local
* Mais plateaux

### Random Restart Hill Climbing

~~~
RRHillClimbing(problem, max\_iter) : State
    best = HillClimbing(RandomState(problem))
    for i in max\_iter do
        next = HillClimbing(RandomState(problem))
        if Score(next) > Score(best) then
            best = next
    return best
~~~

#### SKE C B1 LOL ?

* Toujours rapide sur des ensembles réduits
* Évite plateaux et extremums locaux
* problématique sur des problèmes NP-complets avec beaucoup d'extremums locaux
* N'autorise pas les "retours arrière" donc incomplet

### Simulated Annealing

~~~
SimulatedAnnealing(initial) : State
    current = initial
    for time = 1 to \infinity do
        temp = GetTemp(time)
        if temp = 0 then
            return current
        next = RandomChoice(Successors(current))
        diff = Score(next) - Score(current)
        if diff > 0
            current = next
        else if AcceptMaybe(exp(diff / temp)) then
            current = next
~~~
