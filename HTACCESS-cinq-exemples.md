![Apache_logo](./images/Apache_logo.png)

# - HTACCESS, cinq exemples.

| Cat | Etapes |
|------|------|
| - 1. | [](#balise_02) |
| - 2. | [](#balise_02) |
| - 3. | [](#balise_03) |
| - 4. | [](#balise_04) |
| - 5. | [](#balise_05) |


Dix astuces .htaccess que tout le monde devrait connaître

Les fichiers de configuration .htaccess (en français : accès hypertexte) permettent aux Webmasters de paramétrer leurs règles relatives aux répertoires de leurs sites sur des serveurs NCSA tels que le HTTP d’Apache. Ces fichiers définissent par exemple quels utilisateurs ont le droit d’accès à certaines données. Un autre exemple typique d’astuce .htaccess serait la mise en place d’une redirection automatique.  
C’est quoi exactement un fichier .htaccess ?

Le terme .htaccess désigne un fichier texte dont l’utilisateur ayant les droits d’administration se sert pour configurer un serveur Web compatible à NCSA. Cette technique a été inventée dans les années 90 pour le serveur Web NCSA HTTPD, très innovant pour l’époque. Actuellement, elle intervient avant tout sur le serveur HTTP Apache dont l’exploitation est gérée par plusieurs fichiers centraux, les « httpd.conf ». Ces données de configuration supérieures sont enregistrées en règle générale dans un répertoire du programme du serveur Web et définis par l’administrateur du serveur. Ils déterminent si un utilisateur a le droit de modifier la configuration du serveur grâce à des astuces .htaccess. Si oui, celui-ci peut alors créer et modifier des fichiers .htaccess pour chaque nouveau répertoire et écraser quelques parties de la configuration via des répertoires de niveau supérieur.

A chaque consultation de page, le serveur Web scanne la totalité de ces répertoires supérieurs sans en sauvegarder les informations (le .htaccess d’un sous répertoire écrase donc celui d’un supérieur). Les réglages du serveur qui ont été réalisés avec un fichier .htaccess sont valables dès que celui-ci est déposé sur le répertoire approprié, sans nécessiter de redémarrer le serveur. L’écriture ne doit comporter aucune erreur car elle pourrait empêcher l’accès à tout le serveur. L’application de ces astuces .htaccess à la lettre peut vraiment faciliter la gestion d’un serveur. Étant donné l’aisance et la rapidité de leur insertion dans la structure existante, on parle aussi souvent d’astuces .htaccess.
Comment créer un fichier .htaccess

Étant donné qu’il s’agit de fichiers textes purs, il est possible de les créer et de les modifier avec n’importe quel éditeur. Le processus de création d’un fichier .htaccess est différent en fonction des accès disponibles sur le serveur Web. Les serveurs Telnet ou SSH proposent de le créer et de le modifier directement sur la plateforme serveur. Si vous n'avez qu’un accès FTP à disposition, le fichier devra alors être créé localement et ensuite être téléchargé. Si le nom commence par un point, c’est qu’il s’agit d’un fichier de répertoire de système Unix. Celui-ci sera alors considéré comme « caché » et apparaîtra invisible lors de l’utilisation de clients FTP.

Ce point peut engendrer un problème lors de la création d’un .htaccess local sur un système Windows mais se résout rapidement. Ainsi, l’éditeur n’attachera pas l’extension .txt si le fichier est enregistré sous « tout fichier ». Si le fichier .htaccess contient la bonne directive, il sera expédié dans le bon répertoire et sera tout de suite valide. Cela concerne aussi tout le sous-répertoire.
Configurer un serveur via une astuce (.htaccess).

Les utilisateurs autorisés par les administrateurs ont la possibilité via les fichiers .htaccess d’influencer rapidement la configuration de serveurs Web. Ils peuvent par exemple protéger des répertoires entiers d’accès illégaux via une authentification HTTP. Par ailleurs, des pages d’erreurs ou de redirection peuvent s’afficher. Il existe un certain nombre de conseils avec .htaccess. En voici les dix principaux.
1. Les pages d’erreur personnalisables.

Les serveurs Web peuvent afficher par défaut des fichiers HTML standards voire des avertissements codés si une erreur survient lors d’un accès à un site Internet. Ces messages d’erreurs sont souvent bruts et ne sont pas agréables pour les utilisateurs. Il est possible avec le fichier .htaccess de créer des pages personnalisées qui se marieront mieux avec la charte graphique de votre site Internet. Voici le code à intégrer dans ce cas :


