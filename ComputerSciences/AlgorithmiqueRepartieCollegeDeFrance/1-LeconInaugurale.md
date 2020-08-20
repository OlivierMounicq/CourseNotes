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

#### 4.1 Les principales causes de la perte d'universalité

Les principales causes de la perte d'universalité sont:  
- la quête de robustesse d'un système d'information  
- la température des CPU, d'où l'utilisation des multi-coeurs

#### 4.2/ Algorithmique répartie  

L'algorithmique répartie contient en plus des instructions de l'algorithmique classique (addtion, soustraction, embranchement...) des instructions pour envoyer des messages afin de synchroniser les machines.

#### 4.3/ Algorithmique répartie et complexité  

##### 4.3.1 Complexité d'un algorithme classique

La complexité mesure l'évolution du nombre d'instructions d'un algorithme par rapport à la taille des données fournies en entrée.

##### 4.3.2 Complexité d'un algorithme réparti

La complexité d'un algorithme réparti mesure le nombre de message envoyé par rapport à la taille du réseau.  
On considère que le cout d'une instruction locale est négligeable. Ce qui est considéré comme couteaux : l'envoi de message.  

#### 4.4 Atomicité

L'atomicité est l'illusion d'avoir une machine universelle unique à la place d'un réseau de machine universelle.  

#### 4.5 Atomicité et robustesse : l'universalité perdue  

Lorsque l'armée américaine a commencé à dupliquer les informations au sein de son réseau d'ordinateurs, les concepteurs devaient assurer deux caractéristiques :  
- Atomicité :garder l'illusion de se connecter à une seule machine
- Robustesse : tolérance aux défaillances 

=> Il est impossible d'assurer ces deux caractéristiques en même temps.  (cf Hagit Attiya, Amotz Bar-Noy et Danny Dolev)

Le problème qui consiste donc à concevoir un algorithme qui va mettre d'accord un ensemble de machines est impossible à résoudre !

On a N serveurs et au minimum un peut tomber en panne  
=> dans ce cas, il est impossible de garantir l'unicité de la réponse envoyée par le réseau à un ensemble de client : l'atomicité est violer.


__Théorème Nancy Lynch / Michael Fisher / Michael Patterson__:  
_Aucun algorithme ne peut résoudre le consensus dans un réseau aynchrone avec envoi de message.

__==>Pas de consensus => pas d'atomicité => pas d'universalité__ 

#### 4.6 CPU multi-coeurs et la perte d'universalité  

Jusqu'en 2000, la vitesse des processeurs doublaient tous les 18 mois: un même algorithme allait 2 fois plus vite tous les 18 mois en chaneant simplement le processeur.  
Mais à partir de 2000, les CPU sont devenus multi-coeurs : il faut synchroniser les coeurs via une mémoire partagée.  

__Théorème Michael C. Loui & Hosmane H Abu-Amara (1987)__  
_Aucun algorithme ne peut résoudre le consensus dans un réseau asynchrone avec partage de mémoire (dans laquelle on peut lire et écrire)_  

Ce théorème est une généralisation/une extension de la preuve de Lynch:  
- Lynch : passage de message  
- Loui & Abu-Amara : partage de mémoire  


### 5/ Universalité et Consensus  

Donc nous savons que pas de consensus donc pas d'universalité.  
Mais la quête d'universalité part aussi du consensus. _Le consensus est une condition nécessaire à l'universalité._  
=> La résolution du consensus est une condition suffisante à l'universalité. (Bien que nous avons démontré qu'il est impossible de résoudre le problème de consensus).  

#### 5.1/ Théorème proposé par Leslie Lamport en 1978 et démontré par Schneider en 91  
__Toute solution de consensus permet de construire une machine répartie universelle__  

Donc si on résoud le problème du consensus alors on pourra créer une machine universelle répartie. (Mais on a démontré l'impossibilité de tendre vers un consensus !).  

#### 5.2/ Théorèmes et conditions rendant impossible  

_Dans un réseau (1) asynchrone avec (2) envoi de message ou (2) partage de mémoire, le (3) consensus est impossible._  

__(1) Asynchronisme__ : aucune hypothèse sur le temps de communication (le message met un certain temps à arriver mais on ne sait pas déterminer le seuil à partir duquel l'absence de réception de message permet de dire que l'émetteur est tombé en panne)  
=> Si on a une borne supérieure pour le temps de communication, la résolution du consensus est simple. Le fait d'avoir une borne supérieure est une hypothèse forte par définition. De plus, si la borne est trop élevé, la réactivité pour déterminer une panne sera moins bonne.  

Le travail des chercheurs : trouver une hypothèse plus faible sur le temps et qui permet de résoudre le consensus.  

_hypothèse faible_ : il existe une borne (on ne connait pas cette borne et on ne sait pas quand elle sera vérifiée)  

#### 5.3/ Consensus indulgent

__Consensus indulgent : ces algorithmes doivent pardonner le erreurs__  
=> Exemple : Algorithme Paxos de Lamport.  

#### 5.4/ Compare and swap (CAS)

Impossibilité du consensus en mémoire partagée repose sur le fait que les actions de lecture et d'écriture sont des actions séparées. Si on les regroupe et on ajoute une opération de test en une seule opération hardware, on obtient CAS (Compare And Swap). =>   


#### 5.5/ Restreindre le consensus  

Une piste aussi est de vouloir de restreindre le consensus : au lieu de vouloir d'atteindre le consensus pour les N machines du réseau, on veut résoudre le consensus pour k  machines (avec k < N).


=> Algorithme répartie & tolérance aux défaillances byzantines.













