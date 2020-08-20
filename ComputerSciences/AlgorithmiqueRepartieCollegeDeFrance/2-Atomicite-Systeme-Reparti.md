Comment construire une variable atomique ?  
Dans le domaine de l'algorithmique répartie/concurrente, on appelle cela un _registre_.

### 1/ Définition d'un registre 

Un _registre_ a deux opérations : read() et write().  

Et les méthodes:  

```py
read()
  return(x)
  
write(v)
  x -< v;
  return(OK);
```

