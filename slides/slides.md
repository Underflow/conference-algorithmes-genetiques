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
    for i = 1 to max\_iter do
        next = HillClimbing(RandomState(problem))
        if Score(next) > Score(best) then
            best = next
    return best
~~~

#### Verdict

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

### Simulated Annealing (2)
#### Ouh, c'est chaud

* Complet
* Rapide
* Mais utilise trop peu de mémoire, pourquoi ne pas BOURRINER UN PEU PLUS ?

### Particle Swarm Optimization

~~~
PSO(problem) : State
    currents = GetKRandomStates(problem, K)
    forever
        foreach state in currents
            state = ApplyForceTo(state, Best(currents));
        if IsSolution(Best(scores)) then
            return Best(scores)
~~~

#### Verdict

* Définition de "force" compliquée sinon
* Très joli à afficher :D
* Intéressants dans des espaces "spatiaux" 2D ... nD
* Beaucoup de notions superflues (acceleration, force, vitesse)

### Local Beam Search

~~~
LocalBeam(problem) : State
    currents = GetKRandomStates(problem, K)
    forever
        nexts = {}, scores = []
        foreach state in currents do
            nexts += Successors(state)
        foreach state in nexts
            scores += (Score(state), state)
        Sort(scores)
        currents = {}
        if IsSolution(Best(scores)) then
            return Best(scores)
        currents = KeepKBests(scores, K)
~~~

#### Verdict

* Utilise bien la mémoire
* Complet
* Rapide

## Algorithmes génétiques

### Citations

* ``La sélection sexuelle... dépend de l'ardeur, du courage, de la rivalité des
  mâles autant que du discernement, du goût et de la volonté de la femelle.''
  (Charles Darwin / 1809-1882)
* ``C'est d'la merde'' (Aurélie Teri)
* ``Le créationnisme est la vue qu’il est possible de déduire grâce aux
  preuves empiriques que certaines observations de l’univers et du monde du
  vivant sont mieux expliquées par Dieu que par des processus non dirigés tels
  que la sélection naturelle'' (New World Encyclopaedia)

### Une histoire de selection naturelle

\begin{center}\includegraphics[scale=0.5]{selection.png}\end{center}

La séléction naturelle est un phénomène naturel qui s'est mis en place avec
l'émergence d'entités capables de se reproduire.

### Un peu de biologie...

* Plus un être vivant est "performant" plus il a de chances de se reproduire
* La performance d'un individu dépend de son génome (ADN)
* Quand un individu se reproduit, il mélange son ADN avec un autre individu
* Au cours de sa vie et pendant la reproduction, des erreurs de copie d'ADN
  surviennent : les mutations

### De l'ADN

\begin{center}\includegraphics[scale=0.5]{adn.png}\end{center}

### Du génotype au phénotype

\begin{center}\includegraphics[scale=0.5]{translation.png}\end{center}

### Et l'algorithmie dans tout ça ?

Les algorithmes génétiques implémentent l'ensemble de ces processus. Tout comme
les êtres vivants, les solutions évoluent progressivement vers l'optimalité !

### L'espace de recherche

#### Rappel

Fonction de coût (fitness pour un algorithme génétique) : $f : E \to \mathbb{R}$

#### Génome

Vous cherchez un élement de E, pour cela, on commence par définir un génome
(ADN) "codant" un élement de E.

Le génome est une suite d'octets (découpés en gènes) pouvant représenter par exemple :

* Un ou plusieurs nombres (optimisation combinatoire)
* Une image, la position de solides pour une simulation physique (<3)
* Une séquence d'instructions, un arbre de syntaxe abstrait
* ...

### Population et individus

Afin de simuler l'évolution, il est nécessaire de disposer d'une population.

* Une population est un ensemble fini d'individus (caractérisés par un génome).
* La taille de la population influe sur la rapidité de convergence de
l'algorithme.
* La population est triée en classant les individus en fonction de leur
  fitness.

### Reproduction

On mélange le génome de deux individus.

* Mélange gène par gène, octet par octet...
* Mélange des sous-arbres (génome arborescent)

La reproduction doit avoir un sens, c'est à dire qu'il doit y avoir une
continuité des phénotypes après reproduction.


### Selection artificielle

La séléction permet de faire émerger les meilleurs individus au fur et à mesure
des générations.

* Selection par tournoi
* Selection avec roue biaisée
* Reward-based selection (les individus héritent un score de récompense de
  leur parents s'ils ont tendance à faire évoluer la population)
* etc...

### Mutation

Au cours de l'évolution, les individus doivent subir des mutations de façon à
permettre l'apparition de nouveaux phénotypes.

#### Définition
Les mutations sont des modifications aléatoires, brutales et définitives du
génome.
