<a name="Exemple_create_VirtualHost.md"></a>
![Apache_logo](./images/Apache_logo.png)

# - Créé deux VirtualHosts HTTP & HTTPS.

```
nano /etc/apache2/sites-available/000-default.conf
```
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
nano /etc/apache2/sites-available/default-ssl.conf
```
```
# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 29-06-2023
# Date de modification : le 29-06-2023
# default_ssl.conf - Exemple concernant le VirtualHost default-ssl.conf
# /etc/apache2/sites-available/
# --------------------------------------------------------------------------
<VirtualHost *:443>

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

        # SSL Engine Switch:
        # Enable/Disable SSL for this virtual host.
        SSLEngine on

        # A self-signed (snakeoil) certificate can be created by installing
        # the ssl-cert package. See
        # /usr/share/doc/apache2/README.Debian.gz for more info.
        # If both key and certificate are stored in the same file, only the
        # SSLCertificateFile directive is needed.
        SSLCertificateFile      /etc/ssl/certs/certfile.crt
        SSLCertificateKeyFile   /etc/ssl/private/keyfile.key

        # SSL Engine Options:
        # Set various options for the SSL engine.
        # o FakeBasicAuth:
        #   Translate the client X.509 into a Basic Authorisation.  This means that
        #   the standard Auth/DBMAuth methods can be used for access control.  The
        #   user name is the `one line' version of the client's X.509 certificate.
        #   Note that no password is obtained from the user. Every entry in the user
        #   file needs this password: `xxj31ZMTZzkVA'.
        # o ExportCertData:
        #   This exports two additional environment variables: SSL_CLIENT_CERT and
        #   SSL_SERVER_CERT. These contain the PEM-encoded certificates of the
        #   server (always existing) and the client (only existing when client
        #   authentication is used). This can be used to import the certificates
        #   into CGI scripts.
        # o StdEnvVars:
        #   This exports the standard SSL/TLS related `SSL_*' environment variables.
        #   Per default this exportation is switched off for performance reasons,
        #   because the extraction step is an expensive operation and is usually
        #   useless for serving static content. So one usually enables the
        #   exportation for CGI and SSI requests only.
        # o OptRenegotiate:
        #   This enables optimized SSL connection renegotiation handling when SSL
        #   directives are used in per-directory context.
        #SSLOptions +FakeBasicAuth +ExportCertData +StrictRequire

        <FilesMatch "\.(?:cgi|shtml|phtml|php)$">
                SSLOptions +StdEnvVars
        </FilesMatch>
        <Directory /usr/lib/cgi-bin>
                SSLOptions +StdEnvVars
        </Directory>

</VirtualHost>
```
Toutes les étapes doivent être exécutées en tant que root. 

Pour devenir root lancez simplement :

```
su - root
```
- Conditions préalables.

Effectuez ces étapes pour installer les packages prérequis.
```
apt-get update && apt upgrade -y
```
```
apt-get install -y openssl
```
Toutes les étapes restantes seront effectuées à partir du répertoire de base de l'utilisateur root pour s'assurer que les fichiers que vous créez ne sont accessibles à personne d'autre qu'à l'utilisateur root.

Accédez au répertoire personnel avec cette commande :
```
cd ~
```
- Générer un fichier de clé privée.

La première étape consiste à générer le fichier de clé privée, exécutez la commande suivante :
```
openssl genrsa -out keyfile.key 2048
```
- Générer un fichier de demande de certificat.

Ensuite, vous allez générer le fichier de demande de certificat en exécutant la commande suivante :
```
openssl req -new -key keyfile.key -out certrequest.csr
```
Vous devrez fournir certaines valeurs, certaines peuvent être laissées vides, mais la valeur la plus importante est le nom commun. Dans l'exemple ci-dessous, vous pouvez voir que core-033.domain.local a été utilisé, ce qui signifie que lorsque vous accédez au serveur Nagios Core dans votre navigateur Web, c'est l'adresse que vous devrez utiliser. 

Ceci est particulièrement important, si ceux-ci ne correspondent pas, vous recevrez des avertissements dans votre navigateur Web.

Ce qui suit est un exemple :

Vous êtes sur le point d'être invité à saisir des informations qui seront intégrées à votre demande de certificat.

Ce que vous êtes sur le point d'entrer est ce qu'on appelle un nom distinctif ou un DN.
Il y a pas mal de champs mais vous pouvez en laisser des vides.
Pour certains champs, il y aura une valeur par défaut.
Si vous entrez '.', le champ sera laissé vide.

```
Country Name (2 letter code) [AU]:AU
State or Province Name (full name) [Some-State]:NSW
Locality Name (eg, city) []:Sydney
Organization Name (eg, company) [Internet Widgits Pty Ltd]:My Company Pty Ltd
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:core-033.domain.local
Email Address []:

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
```
Comme vous pouvez le voir ci-dessus un mot de passe n'a pas été fourni, il n'est pas nécessaire.

- Signer la demande de certificat.

À ce stade, vous avez créé une demande de certificat qui doit être signée par une autorité de certification.

- Utilisation d'une société CA de confiance.

Si vous envisagez d'utiliser une société de confiance telle que VeriSign pour vous fournir un certificat, vous devrez lui envoyer une copie de la demande de certificat. 
Cela peut être visualisé en exécutant la commande suivante :
```
cat certrequest.csr
```
You'll get a lot of random text, this is what you will need to provide to your trusted CA. You must provide the CA with everything including the -----BEGIN CERTIFICATE REQUEST----- and -----END CERTIFICATE REQUEST----- lines.
```
Une fois qu'ils vous ont envoyé le certificat signé, vous devrez copier le certificat dans un nouveau fichier appelé certfile.crt. Le certificat que vous recevrez contiendra également beaucoup de texte aléatoire, vous pouvez donc simplement coller ce texte dans le nouveau fichier que vous pouvez ouvrir avec l'éditeur nano :
```
nano certfile.crt
```
You must paste everything including the -----BEGIN CERTIFICATE----- and -----END CERTIFICATE----- lines when pasting them into the file.
```
Enregistrez le fichier et fermez nano.

Vous pouvez maintenant passer à l'étape Copier les fichiers.

- Auto-signature du certificat.

Vous pouvez également auto-signer le certificat en exécutant la commande suivante :
```
openssl x509 -req -days 365 -in certrequest.csr -signkey keyfile.key -out certfile.crt
```
Ce qui devrait produire une sortie indiquant que la signature était OK et qu'il s'agissait d'obtenir la clé privée.

Remarque : Lorsque vous signez vous-même un certificat, vous recevez des avertissements dans votre navigateur Web.

- Copier des fichiers

Vous devez copier les fichiers de certificat à l'emplacement correct et définir les autorisations, exécutez les commandes suivantes :

```
cp certfile.crt /etc/ssl/certs/
```
```
cp keyfile.key /etc/ssl/private/
```
```
chmod go-rwx /etc/ssl/certs/certfile.crt
```
```
chmod go-rwx /etc/ssl/private/keyfile.key
```
- Mettre à jour la configuration d'Apache.

Activez le module mod_ssl dans Apache en exécutant la commande suivante :
```
a2enmod ssl
```
```
a2enmod rewrite
```
Vous devez maintenant indiquer au serveur Web Apache où le rechercher. 
Ouvrez le fichier suivant dans vi en exécutant la commande suivante :
```
nano /etc/apache2/sites-available/default-ssl.conf
```
Trouvez ces lignes et mettez-les à jour comme suit :
```
SSLCertificateFile    /etc/ssl/certs/certfile.crt
SSLCertificateKeyFile /etc/ssl/private/keyfile.key
```
Enregistrez les modifications, vous avez terminé de modifier ce fichier.

Ouvrez le fichier suivant dans nano en exécutant la commande suivante :
```
nano /etc/apache2/sites-available/000-default.conf
```
Naviguez jusqu'à la fin du fichier et avant </VirtualHost> ajoutez ce qui suit :
```
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}
```
Enregistrez les modifications, vous avez terminé de modifier ce fichier.

Vous devez maintenant activer cette configuration dans Apache en exécutant la commande suivante :

```
a2ensite default-ssl.conf
```
- Rechargez le serveur Web Apache.

Vous devez recharger Apache pour que la nouvelle clé de certificat soit utilisée.

```
systemctl reload apache2.service
```
Une petite ligne de commande fort utile qui permet de tester sa conf apache2 sans le redemarer.
```
apachectl -t
```
```
Retour :
Syntax OK
```
Aussi,
```
apachectl configtest
```
```
Retour :
Syntax OK
```
- Règles de pare-feu.

Vous devez autoriser le trafic entrant du port 443 sur le pare-feu local afin de pouvoir accéder à l'interface Web de Nagios Core.
```
iptables -I INPUT -p tcp --destination-port 443 -j ACCEPT
```
```
apt-get install -y iptables-persistent
```
```
If prompted, answer yes to saving existing rules
```
- Test Certificate.

Testez maintenant votre connexion au serveur en dirigeant votre navigateur Web vers https://votrenomdeserveur/.

Remarque : il n'y a pas d'extension nagios/ dans l'URL, vous testez simplement une connexion à Apache pour voir si le certificat fonctionne.

Vous pouvez recevoir un avertissement de certificat auto-signé, mais ce n'est pas grave, vous pouvez simplement ajouter une exception de sécurité. 
Si cela fonctionne, vous verrez la page Web de test Apache.

Vous pourrez désormais accéder à votre serveur Nagios Core en dirigeant votre navigateur Web vers https://yourservername/nagios/.

S'il renvoie une erreur, vérifiez votre pare-feu et revenez en arrière dans ce document, en vous assurant que vous avez effectué toutes les étapes répertoriées.

- Remarques sur la redirection.

Avec cette configuration, si un utilisateur tape http://yourservername dans son navigateur Web, il le redirigera vers https://yourservername, ce qui peut provoquer des avertissements de certificat. 

Si vous souhaitez les rediriger vers https://votrenomdeserveur.votredomaine.com, il vous suffit de modifier la règle de réécriture.
```
RewriteRule (.*) https://yourservername.yourdomain.com%{REQUEST_URI}
```
Rechargez ensuite le service apache2.
```
systemctl restart apache2.service
```
