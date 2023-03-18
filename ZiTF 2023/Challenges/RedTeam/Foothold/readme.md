## Foothold

Au départ, j'ai pensé à utiliser la même méthode que pour le challenge <a href="https://github.com/CTF-Writeups/ZiTF%202023/The%20Gallery" target="_blank">The Gallery</a>, en utilisant la fonction permettant de changer la photo de profil du CTF.

La solution que j'ai trouvé était plus simple que ça :

Sur le panel de gestion du CTF, il y a une page cachée réservée aux administrateurs. On peut y lire que les singes ont un accès ssh via une private key située dans un .zip qu'on peut télécharger.

Problème : le fichier est protégé par un mot de passe

On va donc devoir le bruteforce avec John the Reaper, en premier avec la commande `zip2john`

```console
┌──(birsol㉿Kali)-[~]
└─$ zip2john ssh_key_647032702ede7e519b1eb0279ba0ef99572e92.zip > file
```

Ensuite avec la commande `john`

```console
┌──(birsol㉿Kali)-[~]
└─$ john file
```

Après quelques minutes d'attente, on obtient le mot de passe `bonobo` pour le fichier .zip

Il ne reste plus qu'à l'extraire, le renommer (`mv monkey_ssh id_rsa`), lui mettre les bonnes permissions (`chmod 400 id_rsa`), et à se connecter en SSH pour récupérer le `flag.txt`