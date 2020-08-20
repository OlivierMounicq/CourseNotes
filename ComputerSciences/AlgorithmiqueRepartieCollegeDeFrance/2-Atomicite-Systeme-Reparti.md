Comment construire une variable atomique ?  
Dans le domaine de l'algorithmique répartie/concurrente, on appelle cela un _registre_.

### 1/ Définition d'un registre 

Un _registre_ a deux opérations : read() et write().  

Et les méthodes:  

```py
read()
  return(x)
  
write(v)
  x <- v;
  return(OK);
```

Pour simplifier, nous supposons que regsitres ne sont que des entiers et la valeur par défaut de ces registre est zéro.

### 2/ Dimensions d'un registre

Il y a 3 dimensions : 
  - Dimension 1 : la valeuur du registre et la signification de la valeur stockée  
    - booléen si la valeur stockée dans le registre est 1 ou 0  
    - des entiers si on peut enregistrer n'importe quelle valeur dans le registre
  - Dimension 2 : 
    - SRSW : Single Reader, single writer  
    - MRSW : Multiple Reader, Single Writer  
    - MRMV : Multiple Reader, Multiple Writer  
  - Dimension 3 : le comportement de la variable en mode concurrentiel
    - safe  
    - regular
    - atomic

#### 2.1 / Dimension 3 : comportement du registre

##### 2.1.1 / Le mode _safe_

 Le mode _safe_ signifie seulement que le comportement est sur et prévisible lorsque le registre n'est accéder en écriture/lecture par un seul thread/CPU. On ne peut accéder à la lecture que lorsque l'écriture de la valeur du registre est terminé.  
Le comportement n'est pas sur voire indéterminé en mode concurrent c'est-à-dire que lorsqu'un thread/CPU accède en écriture et qu'un second thread/CPU accède en lecture avant la fin de l'écriture. Dans ce cas, la valeur lue peut être une valeur qui n'est même pas une valeur historique du registre. 
 
##### 2.2.2/ Le mode _regular_ 

Dans ce cas, le comportement est toujours imprévisible si deux threads/CPUs accèdent en même temps en écriture et lecture. Le seule chose assurée dans ce mode est le fait que la valeur retournée (bien qu'indéterminé) est une valeur qui a bien enregistré dans l'histoire du registre.  

##### 2.2.3/ Le mode _atomic_

Une variable atomique est une variable pour laquelle dès lors la lecture renvoie la valeur qui a été écrite par un autre thread/CPU, alors toutes les autres lectures renverront la même valeur jusqu'au déclenchement d'une nouvelle écriture.
   
_Atomicité_ : tout se passe comme si chaque opération s'éxécute en un seul instant atomique entre l'invocation d'une opération et la réponse.  

Quand on utilise une variable atomique, on a l'illusion que toutes les opérations sont séquentielles.

### 3/ Question centrale de l'algorithmique répartie

Comment en utilisant un matériel physique qui fournit des variables de type booleéen, ne pouvant être que lue par un seul lecteur et écrite que par un seul écrivain et de comportement _sur_ (_safe_), peut-on concevoir des algorithmes qui permettent d'émuler ou de construire des variables qui soit les plus fortes possibles c'est-à-dire des variables atomiques qui peuvent contenir une multitude de valeurs et pouvant être lues et écrites par n'importe quel thread/processeur ?

Après deux décennies de travaux en algorithmique répartie, on a atteint le résultat suivant : 

__Theroeme__ Un registre atomique acceptant une multitude de valeurs et pouvant être accédé en lecture et écriture par pluieurs CPU peut être implémenté par des registres binaire (booléen), lu par un seul lecteur et écrit que par un seul écrivain et avec un comportement _sur_.  
(A multivalued MRMW atomic _<b>register</b>_ can be wait-free implemented with binary SRSW safe register.)  

Wait-free : ici, un CPU prêt à lire ou à écrire dans le registre ne doit pas être obligé d'attendre d'autres processeurs. Cette notion couvre la notion de _robustesse_ dans le sens que si un processeur ne fonctionne plus, il ne bloque pas les autres processeurs.  

### 4/ Conventions

Le code d'un algorithme sera exécuté par N processeur mais on montre le fonctionnement de l'algorithme sur un seul processeur.

- Le processus executant le code est p<sub>i</sub>  
- Le système comporte N processus   
- Les processus se connaissent tous entre eux  
- Les opérations sur les registre de plus haut niveau commencent par des majuscules : _Read()_ et _Write()_  
- Les opérations sur les registres de base (booléen/SRSW/sûr) commencent par des minuscules : _read()_ et _write()_  
- On omet l'instruction _return(OK)_ à la fin des implémentations des opérations d'écriture _Write_  
- Les écritures sont censé de retourner OK et les lectures une valeur

Nous distinguerons les regstres de base et haut niveau.  

L'exercice devient plus compliqué lorsque:
- le nombre de processus évolue de manière dynamique  
- lorsque les processus ne se connaissent pas tous

### 5/ D'une variable booléenne _sûr_ SRSW vers une variable multi-valeur atomique MRMW

On passe de manière incrémentale d'une variable booléenne SRSW de comportement _sûr_ vers une variable multi valeur atomique MRMW.

#### 5.1/ 1ere étape : passer d'un registre binaire SRSW _sûr_ vers un registre binaire _sûr_ MRSW.  

On veut qu'une multitude de lecteur puisse accéder à cette variable.  


