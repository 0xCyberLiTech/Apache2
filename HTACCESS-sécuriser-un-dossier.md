![Apache_logo](./images/Apache_logo.png)

# - C. HTACCESS sécuriser l'accès à un dossier.

Exemple : /var/www/html/

Nous allons protéger l'accès au dossier /var/www/html/

Créer un fichier caché nommé (.htaccess) dans /var/www/html.

touch /var/www/html/.htaccess

Saisir le code ci-dessous dans /var/www/html/.htaccess
```
AuthType Basic
AuthName "Zone protégée par mot de passe."
AuthUserFile /var/www/.htpasswd
Require valid-user
```
Créer un fichier caché nommé (.htpasswd) dans /var/www/.

Générer une clé de protection :

https://hostingcanada.org/htpasswd-generator/

Puis coller celle-ci dans le fichier caché .htpasswd.
