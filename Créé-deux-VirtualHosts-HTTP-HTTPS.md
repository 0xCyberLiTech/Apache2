<p align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="./images/Apache_logo.png" alt="Logo Apache" width="360">
  </a>
</p>

<div align="center">

  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=32&pause=1000&color=D14A4A&center=true&vCenter=true&width=700&lines=SERVEUR+WEB+APACHE2;VirtualHosts+•+.htaccess+•+Sécurité;Guides+et+Bonnes+Pratiques" alt="Typing SVG" />
  </a>

  <p align="center">
    <em>Guides et astuces pour la configuration du serveur web Apache2.</em><br>
    <b>🌐 Web – 🔐 Sécurité – 🚀 Performance</b>
  </p>

  [![🔗 Profil GitHub](https://img.shields.io/badge/Profil-GitHub-181717?logo=github&style=flat-square)](https://github.com/0xCyberLiTech)
  [![📦 Dernière version](https://img.shields.io/github/v/release/0xCyberLiTech/Apache2?label=version&style=flat-square&color=blue)](https://github.com/0xCyberLiTech/Apache2/releases/latest)
  [![📄 CHANGELOG](https://img.shields.io/badge/📄%20Changelog-Apache2-blue?style=flat-square)](https://github.com/0xCyberLiTech/Apache2/blob/main/CHANGELOG.md)
  [![📂 Dépôts publics](https://img.shields.io/badge/Dépôts-publics-blue?style=flat-square)](https://github.com/0xCyberLiTech?tab=repositories)
  [![👥 Contributeurs](https://img.shields.io/badge/👥%20Contributeurs-cliquez%20ici-007ec6?style=flat-square)](https://github.com/0xCyberLiTech/Apache2/graphs/contributors)

</div>

---

### 👨‍💻 **À propos de moi.**

> Bienvenue dans mon **laboratoire numérique personnel** dédié à l’apprentissage et à la vulgarisation de la cybersécurité.  
> Passionné par **Linux**, la **cryptographie** et les **systèmes sécurisés**, je partage ici mes notes, expérimentations et fiches pratiques.  
>  
> Pproposer un contenu clair, structuré et accessible pour étudiants, curieux et professionnels de l’IT.  
> 🔗 [Mon GitHub principal](https://github.com/0xCyberLiTech)

<p align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim" alt="Skills" alt="Logo techno" width="300">
  </a>
</p>

---

### 🎯 **Objectif de ce dépôt.**

> Ce dépôt a pour vocation de centraliser un ensemble de notions clés concernant la pile LAMP (Linux, Apache, MySQL/MariaDB, PHP/Perl/Python). Il s’adresse aux passionnés, étudiants et professionnels souhaitant
> mieux comprendre cette architecture web open-source, apprendre à déployer et gérer des applications basées sur LAMP, et se familiariser avec les concepts et outils essentiels à son bon fonctionnement et à son
> optimisation.

---

###  Créé deux VirtualHosts HTTP & HTTPS.

```
nano /etc/apache2/sites-available/000-default.conf
```

```
# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 12-12-2023
# Date de modification : le 12-12-2023
# 000-default.conf - Exemple concernant le VirtualHost 000-default.conf
# /etc/apache2/sites-available/
# --------------------------------------------------------------------------
<VirtualHost x.x.x.x:80>

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
# Date de création : le 12-12-2023
# Date de modification : le 12-12-2023
# default_ssl.conf - Exemple concernant le VirtualHost default-ssl.conf
# /etc/apache2/sites-available/
# --------------------------------------------------------------------------
<VirtualHost x.x.x.x:443>

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
ou

```
su -
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

```
mkdir -p Certs/
```

```
cd Certs/
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

Vous devrez fournir certaines valeurs, certaines peuvent être laissées vides, mais la valeur la plus importante est le nom commun.

Ceci est particulièrement important, si ceux-ci ne correspondent pas, vous recevrez des avertissements dans votre navigateur Web.

Ce qui suit est un exemple :

Vous êtes sur le point d'être invité à saisir des informations qui seront intégrées à votre demande de certificat.

Ce que vous êtes sur le point d'entrer est ce qu'on appelle un nom distinctif ou un DN.
Il y a pas mal de champs mais vous pouvez en laisser des vides.
Pour certains champs, il y aura une valeur par défaut.
Si vous entrez '.', le champ sera laissé vide.

```
Country Name (2 letter code) [FR]:FR
State or Province Name (full name) [Some-State]:departement
Locality Name (eg, city) []:Ville
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Mon entreprise Ltd
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:host.domain.local
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

- Cela peut être visualisé en exécutant la commande suivante :

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

- Si cela fonctionne, vous verrez la page Web de test Apache.

Vous pourrez désormais accéder à votre serveur Nagios Core en dirigeant votre navigateur Web vers https://yourservername/nagios/.

S'il renvoie une erreur, vérifiez votre pare-feu et revenez en arrière dans ce document, en vous assurant que vous avez effectué toutes les étapes répertoriées.

- Remarques sur la redirection.

Avec cette configuration, si un utilisateur tape http://yourservername dans son navigateur Web, il le redirigera vers https://yourservername, ce qui peut provoquer des avertissements de certificat. 

Si vous souhaitez les rediriger vers https://votrenomdeserveur.votredomaine.com, il vous suffit de modifier la règle de réécriture.

```
RewriteRule (.*) https://yourservername.yourdomain.com%{REQUEST_URI}
```

echargez ensuite le service apache2.

```
systemctl restart apache2.service
```

---

**Mise à jour :** Juillet 2025

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
