% TP : Algorithmes génétiques
% Quentin de Laroussilhe et Guillaume Sanchez

\tableofcontents
\newpage

# Introduction

Dans ce TP vous allez être amené à réaliser un algorithme génétique qui va
chercher à reproduire une image modèle à l'aide de n carrés de couleurs et de
tailles différentes disposées à des positions différentes sur l'image. Le
génome représentera l'ensemble des carrés à dessiner pour obtenir la
reproduction.

Vous pourrez voir l'image se dessiner et admirer votre population
évoluer sous vos yeux.

Aucun langage n'est imposé, libre à vous de choisir celui avec lequel vous êtes
le plus à l'aise !

![Un exemple de rendu](joconde.png)

\newpage

# C'est parti

## Des fonctions de dessin

Avant de commencer à bourriner de l'ADN, vous allez devoir commencer par écrire
les fonctions vous permettant de manipuler votre image.

Afin de simplifier le travail en C#, je vous recommande d'utiliser SDL.NET
plutôt que XNA (sauf si vous savez manipuler les surfaces avec XNA).

### Dessine moi un carré

Ecrire une fonction dessinant un carré sur une surface, avec la taille, les
trois composantes RGB de la couleur, et la position en paramètre.

### Comparaision d'images

Afin de déterminer le fitness de vos individus (et donc de vos images), il est
nécessaire de pouvoir évaluer la ressemblance d'une image générée à partir d'un
code ADN et le modèle.

Pour cela, vous allez utiliser un algorithme simple, de complexité $n^2$ qui va
parcourir chaque pixel de votre image et calculer la moyenne de la somme de la différence
de chaque composante RGB de chaque pixels[^1].  
Ce chiffre sera donc compris entre 0 et $255*3$

[^1]: Je n'ai pas plus clair, désolé !

#### Prototype  
Surface1 x Surface2 -> entier

### Vérification

Pour vérifier vos fonctions, initialisez deux surfaces de taille 800x800,
dessinez à l'aide de la première fonction un carré de taille 800x800 à la
position (0,0) de couleur (8,10,24) sur la première surface. Sur la deuxième
surface, dessinez un carré de taille 800x800 à la position (0,0) de couleur
(0,0,0).

Comparez les deux surfaces et vérifiez que le résultat donné est bien 42.

## Un génome

On attaque (enfin) le vif du sujet. Vous allez être amené à réaliser la
structures de données que votre algorithme génétique va manipuler : un génome.
C'est sur cette structure que vont être effectuées l'ensemble des mutations,
croisements et autres opérations qui vont conduire à faire tendre votre image
vers l'image modèle.

### Les gènes

Votre génome sera constitué de plusieurs gènes. Il serait donc intelligent de
commencer par définir un gène. Un gène décira les caractéristiques (taille,
position...) d'un carré. Le génome, constitué de plusieurs gènes sera le "plan
de construction" de votre image.

Créez donc une structure (ou classe) décrivant un gène. Un gène contient :

* Deux variables x et y pour la position du carré
* Trois variables r, g, b pour la couleur du carré
* Une variable size pour la taille du carré

#### Randomisation \newline

Au début de votre algorithme génétique, vous serez amené à générer des génomes
aléatoires pour chaqun de vos individus.  
Codez donc une fonction qui crée un gène aléatoire. Les coordonnées x et y et
size seront indiquées en pourcentage et donc comprises entre 0 et 100, 
{r, g, b} entre 0 et 255.

#### Mutation \newline

Le rôle des mutations est de permettre l'apparition de nouveaux caractères au
sein des individus.  
Codez une fonction qui randomize le gène en appelant la fonction codée
précédemment avec une probabilitée de $1/n$ a avec n passé en paramètre.


