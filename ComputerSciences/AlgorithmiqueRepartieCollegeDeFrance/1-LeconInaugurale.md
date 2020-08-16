## Algorithme répartie : Leçon inaugurale

[Leçon inaugurale](https://www.college-de-france.fr/site/rachid-guerraoui/_inaugural-lecture.htm)  

### 1/Les différents types de temps  

- Communication synchrone : temps conceptuellement nul  
- Temps vibratoire : temps physiquement prévisible  

### 2/ TL;TR; Universalité perdue

Quand on décide de dé^ployer un algorithme sur un réseau d'ordinateurs, il faut que ces machines de Turing se mettent d'accord sur l'ordre d'exécution des instructions de l'algorithme.  
=> mettre d'accord des machines est __impossible__   
=> Pas de consensus => pas d'universalité => perte d'universalité  

### 3/ Concept de la machine universelle

#### 3.1/ La pascaline : machine non universelle  

La Pascaline : machine à coder de Pascal  
L'algorithme est soudé dans le mécanisme de la machine : un algorithme, une machine  
La machine ne fait qu'un seul type de calcul, elle est ultra spécialisée => machine efficace mais non universelle  

#### 3.2/ Machine de Turing : machine universelle  

La machine de Turing contient un algorithme qui lui même peut exécuter d'autres algorithmes fournis en entrée.  

Tous les ordinateurs sont concçus sur le même modèle : le modèle universel de la machine de Turing.  
=> Abstraction de la couche hardware / implémentation physique.  
=> on s'abstrait des détails technologiques.  

### 4/ Universalité Perdue

#### 4.1/ Algorithmique répartie  

L'algorithmique répartie contient en plus des instructions de l'algorithmique classique (addtion, soustraction, embranchement...) des instructions pour envoyer des messages afin de synchroniser les machines.

#### 4.2/ Algorithmique répartie et complexité  

##### 4.2.1 Complexité d'un algorithme classique

La complexité mesure l'évolution du nombre d'instructions d'un algorithme par rapport à la taille des données fournies en entrée.

##### 4.2.2 Complexité d'un algorithme réparti

La complexité d'un algorithme réparti mesure le nombre de message envoyé par rapport à la taille du réseau.  
On considère que le cout d'une instruction locale est négligeable. Ce qui est considéré comme couteaux : l'envoi de message.  

#### 4.3 Atomicité

L'atomicité est l'illusion d'avoir une machine universelle unique à la place d'un réseau de machine universelle.  

#### 4.4 Atomicité et robustesse : l'universalité perdue  

Lorsque l'armée américaine a commencé à dupliquer les informations au sein de son réseau d'ordinateurs, les concepteurs devaient assurer deux caractéristiques :  
- Atomicité :garder l'illusion de se connecter à une seule machine
- Robustesse : tolérance aux défaillances 

=> Il est impossible d'assurer ces deux caractéristiques en même temps.  (cf Hagit Attiya, Amotz Bar-Noy et Danny Dolev)

Le problème qui consiste donc à concevoir un algorithme qui va mettre d'accord un ensemble de machines est impossible à résoudre !

On a N serveurs et au minimum un peut tomber en panne  
=> dans ce cas, il est impossible de garantir l'unicité de la réponse envoyée par le réseau à un ensemble de client : l'atomicité est violer.



__Pas de consensus => pas d'atomicité => pas d'universalité__ 











