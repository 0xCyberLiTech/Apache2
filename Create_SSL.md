<a name="Create_SSL.md"></a>
![Apache_logo](./images/Apache_logo.png)

# - C. Accès au site en HTTP et HTTPS.

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
