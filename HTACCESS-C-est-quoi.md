![Apache_logo](./images/Apache_logo.png)

# C’est quoi exactement un fichier .htaccess ?

Le terme .htaccess désigne un fichier texte dont l’utilisateur ayant les droits d’administration se sert pour configurer un serveur Web compatible à NCSA. 

Cette technique a été inventée dans les années 90 pour le serveur Web NCSA HTTPD, très innovant pour l’époque. Actuellement, elle intervient avant tout sur le serveur HTTP Apache dont l’exploitation est gérée par plusieurs fichiers centraux, les « httpd.conf ».

Ces données de configuration supérieures sont enregistrées en règle générale dans un répertoire du programme du serveur Web et définis par l’administrateur du serveur.

Ils déterminent si un utilisateur a le droit de modifier la configuration du serveur grâce à des astuces .htaccess.

Si oui, celui-ci peut alors créer et modifier des fichiers .htaccess pour chaque nouveau répertoire et écraser quelques parties de la configuration via des répertoires de niveau supérieur.

A chaque consultation de page, le serveur Web scanne la totalité de ces répertoires supérieurs sans en sauvegarder les informations (le .htaccess d’un sous répertoire écrase donc celui d’un supérieur).

Les réglages du serveur qui ont été réalisés avec un fichier .htaccess sont valables dès que celui-ci est déposé sur le répertoire approprié, sans nécessiter de redémarrer le serveur.

L’écriture ne doit comporter aucune erreur car elle pourrait empêcher l’accès à tout le serveur.

L’application de ces astuces .htaccess à la lettre peut vraiment faciliter la gestion d’un serveur. 

Étant donné l’aisance et la rapidité de leur insertion dans la structure existante, on parle aussi souvent d’astuces .htaccess.

# Comment créer un fichier .htaccess ?

Étant donné qu’il s’agit de fichiers textes purs, il est possible de les créer et de les modifier avec n’importe quel éditeur. 

Le processus de création d’un fichier .htaccess est différent en fonction des accès disponibles sur le serveur Web.

Les serveurs Telnet ou SSH proposent de le créer et de le modifier directement sur la plateforme serveur. Si vous n'avez qu’un accès FTP à disposition, le fichier devra alors être créé localement et ensuite être téléchargé.

Si le nom commence par un point, c’est qu’il s’agit d’un fichier de répertoire de système Unix.

Celui-ci sera alors considéré comme « caché » et apparaîtra invisible lors de l’utilisation de clients FTP.

Ce point peut engendrer un problème lors de la création d’un .htaccess local sur un système Windows mais se résout rapidement. Ainsi, l’éditeur n’attachera pas l’extension .txt si le fichier est enregistré sous « tout fichier ». Si le fichier .htaccess contient la bonne directive, il sera expédié dans le bon répertoire et sera tout de suite valide. Cela concerne aussi tout le sous-répertoire.

