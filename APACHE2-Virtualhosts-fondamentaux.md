
<div align="center">
<br></br>
<a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ELAMP_" alt="Titre dynamique LAMP" />
</a>
<br></br>
<p align="center">
    <em>VirtualHosts Fondamentaux (Apache2).</em><br>
    <b>🌐 Web – 🔐 Sécurité – 🚀 Performance</b>
</p>

[![🔗 Profil GitHub](https://img.shields.io/badge/Profil-GitHub-181717?logo=github&style=flat-square)](https://github.com/0xCyberLiTech)
[![📦 Dernière version](https://img.shields.io/github/v/release/0xCyberLiTech/Apache2?label=version&style=flat-square&color=blue)](https://github.com/0xCyberLiTech/Apache2/releases/latest)
[![📄 CHANGELOG](https://img.shields.io/badge/📄%20Changelog-Apache2-blue?style=flat-square)](https://github.com/0xCyberLiTech/Apache2/blob/main/CHANGELOG.md)
[![📂 Dépôts publics](https://img.shields.io/badge/Dépôts-publics-blue?style=flat-square)](https://github.com/0xCyberLiTech?tab=repositories)
[![👥 Contributeurs](https://img.shields.io/badge/👥%20Contributeurs-cliquez%20ici-007ec6?style=flat-square)](https://github.com/0xCyberLiTech/Apache2/graphs/contributors)

</div>

---

### 👨‍💻 À propos de moi

> Bienvenue dans mon **laboratoire numérique personnel** dédié à l’apprentissage et à la vulgarisation de la cybersécurité.  
> Passionné par **Linux**, la **cryptographie** et les **systèmes sécurisés**, je partage ici mes notes, expérimentations et fiches pratiques.  
>  
> Proposer un contenu clair, structuré et accessible pour étudiants, curieux et professionnels de l’IT.  
> 🔗 [Mon GitHub principal](https://github.com/0xCyberLiTech)

<p align="center">
    <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
        <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim" alt="Skills" alt="Logo techno" width="300">
    </a>
</p>

---

### 🎯 Objectif

> Ce guide couvre les concepts de base des VirtualHosts dans Apache2 et leurs différentes configurations.

---

## Sommaire

| N°  | Description du sujet                                         | Lien (bouton bleu)                                              |
|-----|-------------------------------------------------------------|----------------------------------------------------------------|
| 01  | Serveurs virtuels par nom sur une seule IP.                  | [Accéder](#balise_01)          |
| 02  | Serveurs virtuels par nom sur plusieurs IPs.                 | [Accéder](#balise_02)          |
| 03  | Même contenu sur plusieurs IPs (interne/externe).            | [Accéder](#balise_03)          |
| 04  | Sites sur différents ports.                                  | [Accéder](#balise_04)          |
| 05  | Hébergement virtuel basé sur IP.                             | [Accéder](#balise_05)          |
| 06  | Hébergements mixtes (IP + port).                             | [Accéder](#balise_06)          |
| 07  | Hébergements mixtes (nom + IP).                              | [Accéder](#balise_07)          |
| 08  | VirtualHost + mod_proxy.                                     | [Accéder](#balise_08)          |
| 09  | Serveurs virtuels _default.                                  | [Accéder](#balise_09)          |
| 10  | Migration nom → IP.                                          | [Accéder](#balise_10)          |
| 11  | Configuration HTTPS/SSL avec Let's Encrypt ou auto-signé.    | [Accéder](#balise_11)          |
| 12  | Certificat SSL gratuit avec Let's Encrypt.                   | [Accéder](#balise_12)          |

---

## Concepts et exemples

...existing code...
<div align="center">

  <br></br>
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ELAMP_" alt="Titre dynamique LAMP" />
  </a>
  <br></br>

  <p align="center">
    <em>VirtualHosts Fondamentaux (Apache2).</em><br>
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

# 🌐 VirtualHosts Fondamentaux (Apache2).

## 👋 Sommaire

| N°  | Description du sujet                                         | Lien (bouton bleu)                                              |
|-----|-------------------------------------------------------------|----------------------------------------------------------------|
| 01  | Serveurs virtuels par nom sur une seule IP.                  | [![Accéder](https://img.shields.io/badge/Accéder-01-blue?style=for-the-badge)](#balise_01)          |
| 02  | Serveurs virtuels par nom sur plusieurs IPs.                 | [![Accéder](https://img.shields.io/badge/Accéder-02-blue?style=for-the-badge)](#balise_02)          |
| 03  | Même contenu sur plusieurs IPs (interne/externe).            | [![Accéder](https://img.shields.io/badge/Accéder-03-blue?style=for-the-badge)](#balise_03)          |
| 04  | Sites sur différents ports.                                  | [![Accéder](https://img.shields.io/badge/Accéder-04-blue?style=for-the-badge)](#balise_04)          |
| 05  | Hébergement virtuel basé sur IP.                             | [![Accéder](https://img.shields.io/badge/Accéder-05-blue?style=for-the-badge)](#balise_05)          |
| 06  | Hébergements mixtes (IP + port).                             | [![Accéder](https://img.shields.io/badge/Accéder-06-blue?style=for-the-badge)](#balise_06)          |
| 07  | Hébergements mixtes (nom + IP).                              | [![Accéder](https://img.shields.io/badge/Accéder-07-blue?style=for-the-badge)](#balise_07)          |
| 08  | VirtualHost + mod_proxy.                                     | [![Accéder](https://img.shields.io/badge/Accéder-08-blue?style=for-the-badge)](#balise_08)          |
| 09  | Serveurs virtuels _default.                                  | [![Accéder](https://img.shields.io/badge/Accéder-09-blue?style=for-the-badge)](#balise_09)          |
| 10  | Migration nom ➜ IP.                                         | [![Accéder](https://img.shields.io/badge/Accéder-10-blue?style=for-the-badge)](#balise_10)          |
| 11  | Configuration HTTPS/SSL avec Let's Encrypt ou auto-signé.    | [![Accéder](https://img.shields.io/badge/Accéder-11-blue?style=for-the-badge)](#balise_11)          |
| 12  | Certificat SSL gratuit avec Let's Encrypt.                   | [![Accéder](https://img.shields.io/badge/Accéder-11-blue?style=for-the-badge)](#balise_12)          |

---

<a name="balise_01"></a>
## 01 - Serveurs virtuels par nom sur une seule adresse IP

Vous avez une IP unique mais plusieurs domaines (CNAMES) pointent vers elle.

🧠 Les noms doivent être résolus côté DNS ou via `/etc/hosts` pour les tests locaux.

### Exemple :

```apache
# ports.conf
NameVirtualHost *:80
Listen 80
```

```apache
<VirtualHost *:80>
    DocumentRoot /var/www/example.com
    ServerName www.example.com
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot /var/www/example.org
    ServerName www.example.org
</VirtualHost>
```

Le premier VirtualHost sera utilisé si aucune correspondance exacte n’est trouvée.

---

<a name="balise_02"></a>
## 02 - Serveurs virtuels par nom sur plusieurs IPs

Deux IPs, une utilisée comme principale, l’autre pour des VirtualHosts.

```apache
Listen 80

<VirtualHost 172.20.30.40>
    ServerName server.domain.com
    DocumentRoot /var/www/main
</VirtualHost>

NameVirtualHost 172.20.30.50

<VirtualHost 172.20.30.50>
    DocumentRoot /var/www/example.com
    ServerName www.example.com
</VirtualHost>

<VirtualHost 172.20.30.50>
    DocumentRoot /var/www/example.org
    ServerName www.example.org
</VirtualHost>
```

---

<a name="balise_03"></a>
## 03 - Même contenu sur des adresses IP internes et externes

```apache
NameVirtualHost 192.168.1.1
NameVirtualHost 172.20.30.40

<VirtualHost 192.168.1.1 172.20.30.40>
    DocumentRoot /var/www/site
    ServerName server.example.com
    ServerAlias server
</VirtualHost>
```

---

<a name="balise_04"></a>
## 04 - Différents sites sur différents ports

```apache
Listen 80
Listen 8080

NameVirtualHost 172.20.30.40:80
NameVirtualHost 172.20.30.40:8080

<VirtualHost 172.20.30.40:80>
    ServerName www.example.com
    DocumentRoot /var/www/site-80
</VirtualHost>

<VirtualHost 172.20.30.40:8080>
    ServerName www.example.com
    DocumentRoot /var/www/site-8080
</VirtualHost>
```

---

<a name="balise_05"></a>
## 05 - Hébergement virtuel basé sur IP

```apache
Listen 80

<VirtualHost 172.20.30.40>
    DocumentRoot /var/www/example.com
    ServerName www.example.com
</VirtualHost>

<VirtualHost 172.20.30.50>
    DocumentRoot /var/www/example.org
    ServerName www.example.org
</VirtualHost>
```

---

<a name="balise_06"></a>
## 06 - Hébergements virtuels mixtes (IP et ports)

```apache
Listen 172.20.30.40:80
Listen 172.20.30.40:8080
Listen 172.20.30.50:80
Listen 172.20.30.50:8080

<VirtualHost 172.20.30.40:80>
    DocumentRoot /var/www/site1-80
    ServerName www.site1.com
</VirtualHost>

<VirtualHost 172.20.30.40:8080>
    DocumentRoot /var/www/site1-8080
    ServerName www.site1.com
</VirtualHost>

<VirtualHost 172.20.30.50:80>
    DocumentRoot /var/www/site2-80
    ServerName www.site2.org
</VirtualHost>

<VirtualHost 172.20.30.50:8080>
    DocumentRoot /var/www/site2-8080
    ServerName www.site2.org
</VirtualHost>
```

---

<a name="balise_07"></a>
## 07 - Hébergements mixtes (nom et IP)

```apache
Listen 80

NameVirtualHost 172.20.30.40

<VirtualHost 172.20.30.40>
    DocumentRoot /var/www/domain1
    ServerName www.domain1.com
</VirtualHost>

<VirtualHost 172.20.30.40>
    DocumentRoot /var/www/domain2
    ServerName www.domain2.com
</VirtualHost>

<VirtualHost 172.20.30.50>
    DocumentRoot /var/www/dedicated
    ServerName www.dedicated.net
</VirtualHost>
```

---

<a name="balise_08"></a>
## 08 - VirtualHost et mod_proxy

```apache
<VirtualHost *:*>
    ProxyPreserveHost On
    ProxyPass / http://192.168.111.2/
    ProxyPassReverse / http://192.168.111.2/
    ServerName proxy.example.com
</VirtualHost>
```

---

<a name="balise_09"></a>
## 09 - Serveurs virtuels _default_

```apache
<VirtualHost _default_:80>
    DocumentRoot /var/www/default80
</VirtualHost>

<VirtualHost _default_:*>
    DocumentRoot /var/www/default
</VirtualHost>
```

---

<a name="balise_10"></a>
## 10 - Migration d’un VirtualHost par nom vers IP

```apache
Listen 80
NameVirtualHost 172.20.30.40

<VirtualHost 172.20.30.40 172.20.30.50>
    DocumentRoot /var/www/example.org
    ServerName www.example.org
</VirtualHost>

<VirtualHost 172.20.30.40>
    DocumentRoot /var/www/example.net
    ServerName www.example.net
    ServerAlias *.example.net
</VirtualHost>
```

### Compatibilité HTTP/1.0 via ServerPath

```apache
<VirtualHost 172.20.30.40>
    DocumentRoot /var/www/subdomain
    RewriteEngine On
    RewriteRule ^/.* /var/www/subdomain/index.html
</VirtualHost>

<VirtualHost 172.20.30.40>
    DocumentRoot /var/www/subdomain/sub1
    ServerName www.sub1.domain.tld
    ServerPath /sub1/
    RewriteEngine On
    RewriteRule ^(/sub1/.*) /var/www/subdomain$1
</VirtualHost>

<VirtualHost 172.20.30.40>
    DocumentRoot /var/www/subdomain/sub2
    ServerName www.sub2.domain.tld
    ServerPath /sub2/
    RewriteEngine On
    RewriteRule ^(/sub2/.*) /var/www/subdomain$1
</VirtualHost>
```

---

<a name="balise_11"></a>
## 11 - HTTPS / SSL avec Apache

### Certificat auto-signé

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /etc/ssl/private/selfsigned.key \
  -out /etc/ssl/certs/selfsigned.crt
```

```apache
<VirtualHost *:443>
    ServerName www.secure.local
    DocumentRoot /var/www/secure

    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/selfsigned.crt
    SSLCertificateKeyFile /etc/ssl/private/selfsigned.key
</VirtualHost>
```

```bash
sudo a2enmod ssl
sudo systemctl reload apache2
```

---

<a name="balise_12"></a>
## 12 - Certificat SSL gratuit avec Let's Encrypt.


# 🔐 Génération d’un certificat SSL gratuit avec Let's Encrypt

## Objectif
Sécuriser un site web avec HTTPS à l’aide d’un **certificat SSL/TLS gratuit** fourni par [Let’s Encrypt](https://letsencrypt.org/), via l’outil **Certbot** et son plugin Apache.

---

## 📦 Étape 1 – Installer Certbot avec le plugin Apache

```bash
sudo apt update
sudo apt install certbot python3-certbot-apache -y
```

> ✅ Cette commande installe Certbot ainsi que le module permettant de configurer automatiquement Apache pour HTTPS.

---

## 🚀 Étape 2 – Générer et installer le certificat SSL

```bash
sudo certbot --apache
```

- Le script vous guide pas à pas :
  - Choix du ou des domaines à sécuriser.
  - Redirection HTTP vers HTTPS (optionnelle mais recommandée).
  - Création automatique du certificat et configuration d’Apache.

> ✅ À la fin, le site est accessible en **HTTPS sécurisé**, avec un certificat valide.

---

## 🔁 Étape 3 – Renouvellement automatique

Les certificats Let’s Encrypt expirent tous les 90 jours. Heureusement, le système de renouvellement automatique est déjà mis en place via **`systemd`** ou **`cron`**.

> 📌 Pour tester le renouvellement sans attendre l’expiration :
```bash
sudo certbot renew --dry-run
```

---

## 🧠 Bon à savoir

- Les certificats sont stockés dans `/etc/letsencrypt/`.
- Le fichier de configuration Apache est automatiquement modifié pour inclure les directives HTTPS.
- Pour plusieurs VirtualHosts, Certbot peut être exécuté à nouveau en ciblant chaque domaine.

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
