# Check Pass

En analysant le fichier avec IDA, on voit que la fonction `check_pass` vérifie avec `strncmp` si la chaine de caractère passée à l'exécution du programme correspond à `4_The_Monkey_heap_heap_heap_00ra`.

Cependant, l'input demandé est modifié par la fonction `tricky_move` (qui décale tous les caractères vers la droite) avant de le comparer.

Il faut donc entrer l'input mais avec un caractère aléatoire d'abord, puis `4_The_Monkey_heap_heap_heap_00ra`

Avec netcat :

```console
┌──(birsol㉿Kali)-[~]
└─$ nc 10.0.0.4 7069
What's the pass phrase stranger ?
a4_The_Monkey_heap_heap_heap_00ra
Here is your key, come join us mate
ZiTF{flag}
```