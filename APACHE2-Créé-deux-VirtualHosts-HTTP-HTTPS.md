<div align="center">

  <br></br>

  <p align="center">
    <a href="https://github.com/0xCyberLiTech">
      <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ELAMP_" alt="Titre dynamique LAMP" />
    </a>
  </p>

  <br></br>

  <h2>Laboratoire numérique pour la cybersécurité, Linux & IT</h2>

  <p align="center">
    <a href="https://github.com/0xCyberLiTech">
      <img src="https://img.shields.io/badge/Profil-GitHub-181717?logo=github&style=flat-square" alt="Profil GitHub" />
    </a>
    <a href="https://github.com/0xCyberLiTech/Apache2/releases/latest">
      <img src="https://img.shields.io/github/v/release/0xCyberLiTech/Apache2?label=version&style=flat-square&color=blue" alt="Dernière version" />
    </a>
    <a href="https://github.com/0xCyberLiTech/Apache2/blob/main/CHANGELOG.md">
      <img src="https://img.shields.io/badge/📄%20Changelog-Apache2-blue?style=flat-square" alt="CHANGELOG" />
    </a>
    <a href="https://github.com/0xCyberLiTech?tab=repositories">
      <img src="https://img.shields.io/badge/Dépôts-publics-blue?style=flat-square" alt="Dépôts publics" />
    </a>
    <a href="https://github.com/0xCyberLiTech/Apache2/graphs/contributors">
      <img src="https://img.shields.io/badge/👥%20Contributeurs-cliquez%20ici-007ec6?style=flat-square" alt="Contributeurs" />
    </a>
  </p>

</div>

<div align="center">
  <img src="https://img.icons8.com/fluency/96/000000/cyber-security.png" alt="CyberSec" width="80"/>
</div>

<div align="center">
  <p>
    <strong>Cybersécurité</strong> <img src="https://img.icons8.com/color/24/000000/lock--v1.png"/> • <strong>Linux Debian</strong> <img src="https://img.icons8.com/color/24/000000/linux.png"/> • <strong>Sécurité informatique</strong> <img src="https://img.icons8.com/color/24/000000/shield-security.png"/>
  </p>
</div>

---

## 🚀 À propos & Objectifs

Ce projet propose des solutions innovantes et accessibles en cybersécurité, avec une approche centrée sur la simplicité d’utilisation et l’efficacité. Il vise à accompagner les utilisateurs dans la protection de leurs données et systèmes, tout en favorisant l’apprentissage et le partage des connaissances.

Le contenu est structuré, accessible et optimisé SEO pour répondre aux besoins de :
- 🎓 Étudiants : approfondir les connaissances
- 👨‍💻 Professionnels IT : outils et pratiques
- 🖥️ Administrateurs système : sécuriser l’infrastructure
- 🛡️ Experts cybersécurité : ressources techniques
- 🚀 Passionnés du numérique : explorer les bonnes pratiques

---

## 🛠️ Configuration de VirtualHosts HTTP & HTTPS avec SSL (auto-signé) sur Apache2.
### ✅ Compatible Debian 12 (Bookworm) & Debian 13 (Trixie)

> **Auteur** : 0xCyberLiTech  
> **Date de création** : 30‑07‑2025  
> **Public visé** : administrateurs Linux, étudiants, pentesters, etc.  
> **Objectif** : déployer Apache avec support SSL via certificat auto‑signé

---

## 📌 Objectif

Configurer deux VirtualHosts :

- 🧩 un pour **HTTP** (port 80)  
- 🔐 un pour **HTTPS** (port 443) avec certificat **auto‑signé**

---

## 🧩 Prérequis

### 🔐 Connexion root

```bash
su -
```

### 📦 Mise à jour et dépendances

```bash
apt update && apt upgrade -y
apt install -y apache2 openssl iptables-persistent
```

---

## 🏗️ Étape 1 – VirtualHost HTTP (`000‑default.conf`)

```bash
nano /etc/apache2/sites-available/000-default.conf
```

```apache
# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 30-07-2025
# Date de modification : le 30-07-2025
# 000-default.conf - Exemple concernant le VirtualHost 000-default.conf
# /etc/apache2/sites-available/
# --------------------------------------------------------------------------
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    <Directory /var/www/>
        Options -Indexes +FollowSymLinks +ExecCGI
        AllowOverride All
        Require all granted
    </Directory>

    # Redirection vers HTTPS (à activer après le SSL)
    #RewriteEngine On
    #RewriteCond %{HTTPS} off
    #RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}
</VirtualHost>
```

---

## 🔒 Étape 2 – Sécurisation Apache (facultatif)

```bash
nano /etc/apache2/conf-available/security.conf
```

Ajoutez :

```apache
ServerTokens Prod
ServerSignature Off
```

---

## 🔐 Étape 3 – Génération du certificat SSL auto‑signé

```bash
cd ~
mkdir -p Certs && cd Certs
```

### 🔑 Clé privée

```bash
openssl genrsa -out keyfile.key 2048
```

### 📄 Demande de certificat (CSR)

```bash
openssl req -new -key keyfile.key -out certrequest.csr
```

Exemple de réponses :

```
Country Name (2 letter code) [FR]:FR
State or Province Name (full name):Hauts-de-Seine
Locality Name (eg, city):Paris
Organization Name (eg, company):CyberLiTech
Common Name (FQDN ou nom du serveur):tonserveur.local
```

### ✍️ Signature auto‑signée

```bash
openssl x509 -req -days 365 -in certrequest.csr -signkey keyfile.key -out certfile.crt
```

---

## 📁 Étape 4 – Installation du certificat

```bash
cp certfile.crt /etc/ssl/certs/
cp keyfile.key /etc/ssl/private/
chmod go-rwx /etc/ssl/certs/certfile.crt
chmod go-rwx /etc/ssl/private/keyfile.key
```

---

## 🌐 Étape 5 – VirtualHost HTTPS (`default-ssl.conf`)

### 🔧 Activation des modules

```bash
a2enmod ssl
a2enmod rewrite
```

### 📄 Configuration

```bash
nano /etc/apache2/sites-available/default-ssl.conf
```

```apache
# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 30-07-2025
# Date de modification : le 30-07-2025
# 000-default.conf - Exemple concernant le VirtualHost default-ssl.conf
# /etc/apache2/sites-available/
# --------------------------------------------------------------------------
<VirtualHost *:443>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    <Directory /var/www/>
        Options -Indexes +FollowSymLinks +ExecCGI
        AllowOverride All
        Require all granted
    </Directory>

    SSLEngine on
    SSLCertificateFile    /etc/ssl/certs/certfile.crt
    SSLCertificateKeyFile /etc/ssl/private/keyfile.key

    <FilesMatch "\.(cgi|shtml|phtml|php)$">
        SSLOptions +StdEnvVars
    </FilesMatch>
    <Directory /usr/lib/cgi-bin>
        SSLOptions +StdEnvVars
    </Directory>
</VirtualHost>
```

---

## 🔁 Étape 6 – Redirection HTTP → HTTPS

Édite `000-default.conf` :

```bash
nano /etc/apache2/sites-available/000-default.conf
```

Dans le bloc `<VirtualHost>`, ajoute à la fin :

```apache
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}
```

➡️ Pour redirection vers un domaine spécifique :

```apache
RewriteRule (.*) https://votreserveur.tondomaine.tld%{REQUEST_URI}
```

---

## ⚙️ Étape 7 – Activation & rechargement Apache

```bash
a2ensite default-ssl.conf
systemctl reload apache2.service
```

---

## 🧪 Étape 8 – Vérification de la configuration

```bash
apachectl configtest
# ou
apachectl -t
```

✅ Doit renvoyer : `Syntax OK`

---

## 🔥 Étape 9 – Pare‑feu : autoriser le port 443

```bash
iptables -I INPUT -p tcp --dport 443 -j ACCEPT
apt install -y iptables-persistent
```

✅ Réponds **yes** pour sauvegarder les règles.

---

## 🌍 Étape 10 – Tester l’accès en HTTPS

Ouvre ton navigateur et va sur :

```
https://tonserveur/
```

- Un **avertissement** est normal avec certificat auto‑signé : ajoute une exception.
- Si HTTP→HTTPS est activée : `http://tonserveur` redirige vers `https://...`

Tu peux ensuite accéder à Nagios (ou ton application) via :

```
https://tonserveur/nagios/
```

---

## 📝 Récapitulatif des fichiers

| Fichier                                       | Rôle                           |
|----------------------------------------------|--------------------------------|
| `/etc/apache2/sites-available/000-default.conf` | VirtualHost HTTP              |
| `/etc/apache2/sites-available/default-ssl.conf` | VirtualHost HTTPS             |
| `/etc/ssl/certs/certfile.crt`                 | Certificat SSL                |
| `/etc/ssl/private/keyfile.key`                | Clé privée SSL                |
| `/etc/apache2/conf-available/security.conf`    | Sécurisation Apache (option) |

---

## ✅ Résultat final

- 🌐 HTTP redirigé automatiquement vers HTTPS  
- 🔐 Certificat SSL (auto‑signé) fonctionnel  
- 📦 Compatible Debian 12 & Debian 13  
- ✅ Apache validé via `configtest`

---

<div align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim,python,markdown" alt="Skills" width="440">
  </a>
</div>

<div align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</div>
