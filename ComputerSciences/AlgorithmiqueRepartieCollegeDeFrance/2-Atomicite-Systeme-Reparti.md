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
   
