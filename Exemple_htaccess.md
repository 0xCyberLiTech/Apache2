<a name="Exemple_htaccess.md"></a>
![Apache_logo](./images/Apache_logo.png)

# .HTACCESS

Exemple :

Prérequis :
```
apt-get update && apt upgrade -y
apt-get install apache2
```
Nous allons sécuriser l'accès au dossier /var/www/dowsloads

1 Activer la prise en charge .htaccess sur DeBian 11 & Debian 12.
2 Redémarrer apache2 et créer le dossier downloads vers /var/www/.
3 Créer le fichier .htaccess dans le dossier /var/www/downloads.
4 Créer le fichier .htpasswd dans le dossier /var/www/downloads.

# - 1 Activer la prise en charge .htaccess sur DeBian 11 & Debian 12.

Se rendre sur cd /etc/apache2/sites-available/
Sauvegarder votre fichier default par mesure de sécurité

tar -cvzf défault.org.tar.gz default.conf

editer la le fichier default.conf

Avant modifications :

```
# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 01-07-2023
# Date de modification : le 01-07-2023
# 000-default.conf - Exemple concernant le VirtualHost 000-default.conf
# /etc/apache2/sites-available/
# --------------------------------------------------------------------------
<VirtualHost *:80>

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        <Directory />
                Options FollowSymLinks
                AllowOverride None
        </Directory>

        <Directory /var/www/>
                Options -Indexes +FollowSymLinks
                Options +ExecCGI
                AllowOverride none
                # Apache 2.4
                Require all granted
                # Apache 2.2
                # Order allow,deny
                # Allow from all
        </Directory>
</VirtualHost>
```
Après modifications

```
# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 01-07-2023
# Date de modification : le 01-07-2023
# 000-default.conf - Exemple concernant le VirtualHost 000-default.conf
# /etc/apache2/sites-available/
# --------------------------------------------------------------------------
<VirtualHost *:80>

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        <Directory />
                Options FollowSymLinks
                AllowOverride all
        </Directory>

        <Directory /var/www/>
                Options -Indexes +FollowSymLinks
                Options +ExecCGI
                AllowOverride all
                # Apache 2.4
                Require all granted
                # Apache 2.2
                # Order allow,deny
                # Allow from all
        </Directory>
</VirtualHost>
```
Sauvegarder les modifications.

Lancer la commande suivante.
```
a2enmod rewrite
```
# - 2 Redémarrer apache2.
```
/etc/init.d/apache2 restart
```
Créer le dossier downloads vers /var/www/.
```
mkdir -p /var/www/downloads
```
# - 3 Créer le fichier .htaccess dans le dossier /var/www/downloads.

```
AuthUserFile /var/www/downloads/.htpasswd
AuthGroupFile /dev/null
AuthName "Saisir vos identifiants"
AuthType Basic
<LIMIT GET POST>
      Require valid-user
</LIMIT>
```
# -4 Créer le fichier .htpasswd dans le dossier /var/www/downloads.

générer le fichier .htpasswd à l'aide de la commande suivante :
```
htpasswd -c .htpasswd mmalet
```
Pour ajouter un utilisateur.
```
htpasswd -b .htpasswd vmalet xxxxxxxx
```
Test d'accès vers http://x.x.x.x/downloads.
