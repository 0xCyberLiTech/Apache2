<a name="Create_SSL.md"></a>
![Apache_logo](./images/Apache_logo.png)

# - C. Accès au site en HTTP et HTTPS.

Exemple concernant le VirtualHost 000-default.conf
```
# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 29-06-2023
# Date de modification : le 29-06-2023
# 000-default.conf - Exemple concernant le VirtualHost 000-default.conf
# /etc/apache2/sites-available/
# --------------------------------------------------------------------------
<VirtualHost *:80>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        <Directory /var/www/>
                Options -Indexes +FollowSymLinks
                Options +ExecCGI
                AllowOverride All
                # Apache 2.4
                Require all granted
                # Apache 2.2
                # Order allow,deny
                # Allow from all
        </Directory>

        RewriteEngine On
        RewriteCond %{HTTPS} off
        RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}

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
