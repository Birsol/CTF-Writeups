## CTFdisaster

En cherchant les failles connues de la plateforme CTFd, on peut voir qu'il est possible de créer un utilisateur ayant le même pseudo que l'admin mais avec un email différent.

J'ai donc créé un utilisateur nommé ` undercut_monkey` (avec un espace en tant que premier caractère) et avec mon adresse mail.

Il ne restait plus qu'à réinitialiser le mot de passe du compte lié à mon addresse mail pour changer également celui du compte admin.

Le flag était celui du "challenge impossible", qu'on pouvait récupérer depuis le panel admin.