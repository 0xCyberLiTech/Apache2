<a name="Create_SSL.md"></a>
![Apache_logo](./images/Apache_logo.png)

# Accès au site en HTTP et HTTPS.

Je vais faire simple, je vous montre pour le miroir Calculate CyberLiTeck les 2 Virtualhosts configurés (simultanément) afin que vous voyiez les différences (ce qui a été ajouté). A savoir le port d'écoute et les 3 lignes commençant par SSL.

```
<VirtualHost *:80> 
   DocumentRoot /home/miroir/public_html/ 
   ServerName miroir.CyberLiTeck.fr 
   ServerAdmin OxCLT@CyberLiTech.org 
   ErrorLog /var/log/httpd/miroir.CyberLiTeck.fr-error_log 
   TransferLog /var/log/httpd/miroir.CyberLiTeck.fr-access_log 
   ServerSignature Off 
 
  <Directory /home/miroir/public_html> 
     Options Indexes +FollowSymLinks 
     AllowOverride All 
  </Directory> 
</VirtualHost> 
```
```
<VirtualHost *:443> 
   DocumentRoot /home/miroir/public_html/ 
   ServerName miroir.CyberLiTeck.fr 
   ServerAdmin OxCLT@CyberLiTech.org
   ErrorLog /var/log/httpd/miroir.CyberLiTeck.fr-error_log 
   TransferLog /var/log/httpd/miroir.CyberLiTeck.fr-access_log 
   ServerSignature Off 
 
   SSLEngine on 
   SSLCertificateFile /etc/letsencrypt/live/miroir.CyberLiTeck.fr/fullchain.pem 
   SSLCertificateKeyFile /etc/letsencrypt/live/miroir.CyberLiTeck.fr/privkey.pem 
 
  <Directory /home/miroir/public_html> 
     Options Indexes +FollowSymLinks 
     AllowOverride All 
  </Directory> 
</VirtualHost>
```
Dans ce cas, l'accès en HTTP reste en HTTP.

L'accès HTTPS reste HTTPS.

Forcer le HTTP en HTTPS.

Si on souhaite forcer le HTTP vers HTTPS, on ajoute ceci dans le bloc Virtualhost *:80.

Voici un exemple pour ce site www.CyberLiTeck.fr :

```
RewriteEngine On
RewriteCond %{REQUEST_URI} !^/.well-known/acme-challenge/
RewriteCond %{HTTP:X-Forwarded-Proto} =http
RewriteRule (.*) https://www.CyberLiTeck.fr$1 [R=301,L]
```
La première ligne RewriteCond permet de conserver du HTTP simple pour les requêtes Lets Encrypt (dossier .well-known/acme-challenge à la racine du site).

La deuxième ligne RewriteCond permet de vérifier en amont qu'on n'est pas en https.

## Ecouter sur plusieurs ports.

Si on souhaite ajouter un vhost qui écoute sur un autre port, il suffit d'ajouter une directive listen en plus dans le fichier de configuration du vhost :

```
Listen 8080
<VirtualHost *:8080>
   #Le contenu du vhost
</VirtualHost> 
```

## Les Virtualhosts qui doivent écouter que sur une seule IP.

Si on dispose de plusieurs adresses IP sur le serveur, on peut avoir besoin de spécifier que le VirtualHost n'écoute sur qu'une adresse IP.

```
<VirtualHost *:443>

</VirtualHost>
```
Le * signifie toutes les IP.

Filtrer avec une seule IPv4.

En IPv4, on procédera ainsi :
```
<VirtualHost 192.168.21.100:443>

</VirtualHost>
```
## Filtrer avec une seule IPv6.

En IPv6, on mettra l'IP entre crochets :
```
<VirtualHost [fe80::225:64ff:feb4:44fe]:443>

</VirtualHost>
```
Pour ceux qui voudront tester l'accès au VirtualHost en IPv6, il faut taper l'IPv6 entre crochets dans le navigateur internet :
```
https://[fe80::225:64ff:feb4:44fe]
```
