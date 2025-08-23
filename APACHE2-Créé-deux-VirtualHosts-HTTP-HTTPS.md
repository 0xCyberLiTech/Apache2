<div align="center">

  <br></br>

  <p align="center">
    <a href="https://github.com/0xCyberLiTech">
      <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ELAMP_" alt="Titre dynamique LAMP" />
    </a>
  </p>

  <br></br>

  <p align="center">
    <em>Configuration de VirtualHosts HTTP & HTTPS avec SSL (auto-signé) sur Apache2.</em><br>
    <b>🌐 Web – 🔐 Sécurité – 🚀 Performance</b>
  </p>

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

<div align="center">

---

### 👨‍💻 **À propos de moi.**

> Bienvenue dans mon **laboratoire numérique personnel** dédié à l’apprentissage et à la vulgarisation de la cybersécurité.  
> Passionné par **Linux**, la **cryptographie** et les **systèmes sécurisés**, je partage ici mes notes, expérimentations et fiches pratiques.  
>  
 > Proposer un contenu clair, structuré et accessible pour étudiants, curieux et professionnels de l’IT.  

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

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
