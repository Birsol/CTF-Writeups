## The Gallery

Pour The Gallery, il fallait que j'arrive à avoir un reverse shell sur le serveur web d'une manière ou d'une autre.

Le seul moyen que j'ai trouvé a été de modifier le fichier `.htaccess`.

On peut voir grâce à l'erreur 403 de la page `uploads/` que c'est un serveur Apache, donc j'ai upload un fichier `.htaccess` autorisant l'exécution de PHP par le serveur pour mon extension de fichier.

```
AddType application/x-httpd-php .pwn
```

Ensuite, il y avait juste à upload un reverse shell en PHP (pour rester dans le thème du CTF j'ai utilisé celui de `pentestmonkey`), mais renommé avec notre extension `.pwn`.

Un petit `nc -nvlp 5555`, on se rend sur la page de notre exploit (`10.0.0.4:7070/uploads/payload.pwn`) et le tour est joué !

Le flag se trouvait à l'emplacement `/flag/flag.txt` sur le serveur.