<a name="Create_VirtualHost.md"></a>
![Apache_logo](./images/Apache_logo.png)

# Création d'un VirtualHost.

Explications sur la structure de base.

```
<VirtualHost *:80> # Virtualhost écoutant sur le port 80
        ServerName dev.CyberLiTech.fr                                  # Nom du serveur auquel le vhost doit répondre
        ServerAlias dev.CyberLiTech.fr                                 # Eventuel alias supplémentaire
        ServerAdmin webmaster@CyberLiTech.fr                           # Mail du webmaster 
        ErrorLog /var/log/apache2/dev.CyberLiTech.fr-error_log         # Délocaliser pour ce vhost les logs d'erreur
        TransferLog /var/log/apache2/dev.CyberLiTech.fr-access_log     # Délocaliser pour ce vhost les logs d'accès
        DocumentRoot "/var/www/localhost/htdocs/dev/"                  # Racile des fichiers du site
        <Directory "/var/www/localhost/htdocs/dev/">                   # Définition des droits d'un répertoire
                Options Indexes FollowSymLinks                         # Options choisies
                AllowOverride All                                      # Permet d'utiliser le htaccess dans un site
                Require all granted                                    # On autorise tout le monde
        </Directory>                                                   # Fin de la définition des droits
</VirtualHost>                                                         # Fin de la définition du vhost
```
- Pour les droits, on a :

  - Require all denied => Tout refuser
  - Require all granted => Tout accepter
  - Require host example.org => Accepter example.org
  - Require ip 1.2.3.4 => Accepter 1.2.3.4
  - Require not ip 1.2.3.4 => Refuser 1.2.3.4

- Pour AllowOverride, on peut utiliser :
  - None : les fichiers .htaccess sont ignorés
  - All : tout type de redéfinition est autorisé dans le .htaccess
  - AuthConfig : autorise l’authentification d’utilisateurs
  - FileInfo : autorise les directives liées aux types de documents
  - Indexes : autorise l’indexation des répertoires
  - Limit : autorise les directives de gestion d’accès
  - ExecCGI : autorise les programmes CGI
  - FollowSymLinks : autorise le suivi des liens symboliques rencontrés dans le répertoire

- Pour Options : OOn peut utiliser
  - All : tout type de redéfinition est autorisé dans le .htaccess
  -  Includes : Inclusions côté serveur (mod_include) autorisées
  - Indexes : autorise l’indexation des répertoires
  - ExecCGI : autorise les programmes CGI
  - FollowSymLinks : autorise le suivi des liens symboliques rencontrés dans le répertoire

- Exemples avec 2 Noms de domaines

Voici l'exemple avec 2 VirtualHosts représentant 2 sites hébergés sur la même machine : dev.CyberLiTech.fr et OxCLT.CyberLiTech.fr. On peut avoir autant de VirtualHosts qu'on le souhaite sur une même machine.

Pour me repérer facilement, je nomme chaque fichier nomdedomaine.conf :

```
nano /etc/apache2/vhosts.d/dev.CyberLiTech.fr.conf

<VirtualHost *:80>
        ServerName dev.CyberLiTech.fr
        ServerAlias dev.CyberLiTech.fr
        ServerAdmin webmaster@CyberLiTech.fr
        ErrorLog /var/log/apache2/dev.CyberLiTech.fr-error_log
        TransferLog /var/log/apache2/dev.CyberLiTech.fr-access_log
        DocumentRoot "/var/www/localhost/htdocs/dev/"
        <Directory "/var/www/localhost/htdocs/dev/">
                Options Indexes FollowSymLinks
                AllowOverride All
                Require all granted
        </Directory>
</VirtualHost>
```
```
nano /etc/apache2/vhosts.d/OxCLT.CyberLiTech.fr.conf

<VirtualHost *:80>
        ServerName OxCLT.CyberLiTech.fr
        ServerAlias OxCLT.CyberLiTech.fr
        ServerAdmin webmaster@CyberLiTech.fr
        ErrorLog /var/log/apache2/OxCLT.CyberLiTech.fr-error_log
        TransferLog /var/log/apache2/OxCLT.CyberLiTech.fr-access_log
        DocumentRoot "/var/www/localhost/htdocs/OxCLT/"
        <Directory "/var/www/localhost/htdocs/OxCLT/">
                Options Indexes FollowSymLinks
                AllowOverride All
                Require all granted
        </Directory>
</VirtualHost>
```
