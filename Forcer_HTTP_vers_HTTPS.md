<a name="Forcer_HTTP_vers_HTTPS.md"></a>
![Apache_logo](./images/Apache_logo.png)

# - D. Forcer le HTTP en HTTPS.

Si on souhaite forcer le HTTP vers HTTPS, on ajoute ceci dans le bloc Virtualhost *:80.

Voici un exemple pour ce site www.CyberLiTech.fr :
```
RewriteEngine On
RewriteCond %{REQUEST_URI} !^/.well-known/acme-challenge/
RewriteCond %{HTTP:X-Forwarded-Proto} =http
RewriteRule (.*) https://www.CyberLiTech.fr$1 [R=301,L]
```
La première ligne RewriteCond permet de conserver du HTTP simple pour les requêtes Lets Encrypt (dossier .well-known/acme-challenge à la racine du site).
La deuxième ligne RewriteCond permet de vérifier en amont qu'on n'est pas en https.
