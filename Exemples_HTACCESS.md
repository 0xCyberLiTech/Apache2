![Apache_logo](./images/Apache_logo.png)

# HTACCESS, cinq exemples.

| Cat | Etapes |
|------|------|
| - 1. | [Rediriger les pages en http vers celles en https.](#balise_1) |
| - 2. | [Enlever le www.](#balise_02). |
| - 3. | [Rediriger une page spécifique d’un serveur sur une page spécifique d’un autre serveur.](#balise_03) |
| - 4. | [Rediriger toutes les URL d’un site lors d’un changement de nom de domaine.](#balise_04) |
| - 5. | [Rediriger toutes les URLs d’un site vers une seule et unique URL.](#balise_05) |

Dans tous nos exemples, nous allons utiliser le fichier .htaccess, qui permet de modifier la configuration de notre serveur. Pour y accéder, nous allons donc devoir nous connecter à notre projet web en FTP. Si vous utilisez WordPress, le fichier est créé automatiquement dans le répertoire racine de votre site. Sinon, à vous de l’ajouter manuellement..

# - 1. Rediriger les pages en http vers celles en https.

Forcer les utilisateurs à utiliser la version https de votre site est important pour leur offrir une sécurité convenable.

Pour ce faire, il vous suffit d’insérer ci-dessous dans votre fichier .htaccess, en remplaçant « exemple.com » par votre nom de domaine :

Exemple : rediriger http://exemple.com vers httsp://exemple.com.
```
RewriteEngine on
RewriteCond %{HTTP:X-Forwarded-Proto} !https
RewriteRule (.*) https://exemple.com/$1 [R=301,L]
```
Si vous rencontrez une erreur de boucle, cela indique que le HTTP/2 est actif sur votre site. Il vous suffit alors de remplacer la deuxième ligne par :
```
RewriteCond %{HTTPS} off
```
# - 2.


# - 3.


# - 4.


# - 5.

