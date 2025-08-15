<div align="center">

  <br></br>
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ELAMP_" alt="Titre dynamique LAMP" />
  </a>
  <br></br>

  <p align="center">
    <em>HTACCESS – 10 astuces que tout le monde devrait connaître.</em><br>
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

# 🔐 HTACCESS – 10 astuces que tout le monde devrait connaître.
### ✅ Compatible Apache 2.4+ sur Debian 12 & 13

---

## 📑 Sommaire

| Nº  | Astuce                                     | Lien vers la section                           |
|-----|--------------------------------------------|-----------------------------------------------|
| 01  | Les pages d’erreur personnalisables        | [![Voir](https://img.shields.io/badge/Voir-01-blue)](#balise-01)       |
| 02  | Redirection                                | [![Voir](https://img.shields.io/badge/Voir-02-blue)](#balise-02)       |
| 03  | Protection par mot de passe                | [![Voir](https://img.shields.io/badge/Voir-03-blue)](#balise-03)       |
| 04  | Augmenter la mémoire PHP                   | [![Voir](https://img.shields.io/badge/Voir-04-blue)](#balise-04)       |
| 05  | Changer le fuseau horaire                  | [![Voir](https://img.shields.io/badge/Voir-05-blue)](#balise-05)       |
| 06  | Bloquer des adresses IP                    | [![Voir](https://img.shields.io/badge/Voir-06-blue)](#balise-06)       |
| 07  | Rediriger HTTP vers HTTPS                  | [![Voir](https://img.shields.io/badge/Voir-07-blue)](#balise-07)       |
| 08  | Afficher un répertoire                     | [![Voir](https://img.shields.io/badge/Voir-08-blue)](#balise-08)       |
| 09  | Bloquer le Hotlinking                      | [![Voir](https://img.shields.io/badge/Voir-09-blue)](#balise-09)       |
| 10  | Définir la police de caractères            | [![Voir](https://img.shields.io/badge/Voir-10-blue)](#balise-10)       |

---

## ❓ Qu’est-ce qu’un fichier `.htaccess` ?

Un fichier `.htaccess` permet de configurer finement le comportement d’un serveur Apache, répertoire par répertoire. C’est un fichier texte caché (préfixé d’un point) interprété automatiquement par le serveur **sans redémarrage**. Il peut être utilisé pour sécuriser un répertoire, faire des redirections, afficher des erreurs personnalisées, etc.

---

## 🛠️ Création du fichier `.htaccess`

- Utilisez n’importe quel éditeur texte : `nano`, `vim`, ou via FTP/SFTP.
- Le fichier doit s’appeler **exactement** `.htaccess`
- Il est **caché** (fichier commençant par un point)
- Placez-le dans le répertoire que vous souhaitez configurer (ex. `/var/www/html/`)

---

<a name="balise-01"></a>
## 01 – Les pages d’erreur personnalisables

```apache
# Page d’erreur 404 personnalisée
ErrorDocument 404 /erreur/404.html

# Variante avec URL externe
ErrorDocument 404 http://www.monsite.com/erreur/404.html
```

---

<a name="balise-02"></a>
## 02 – Redirection

```apache
# Redirection complète vers un autre domaine
Redirect / http://www.nouveau-domaine.fr/

# Redirection d’une page spécifique
Redirect /ancienne-page.html nouvelle-page.html
```

---

<a name="balise-03"></a>
## 03 – Protection par mot de passe

### `.htaccess`

```apache
AuthType Basic
AuthName "Accès réservé"
AuthUserFile /chemin/vers/.htpasswd
Require valid-user
```

### Exemple de `.htpasswd`

```text
User1:duCmo1zxkKx6Y
User2:mou3IYjSLpGWI
User3:HGKS9XzDXXAXQ
```

> Utilisez `htpasswd` pour générer les entrées chiffrées.

---

<a name="balise-04"></a>
## 04 – Augmenter la mémoire PHP

```apache
# Limite mémoire PHP à 128 Mo
php_value memory_limit 128M
```

---

<a name="balise-05"></a>
## 05 – Changer le fuseau horaire

```apache
# Fuseau horaire pour PHP
SetEnv TZ Europe/Paris
```

---

<a name="balise-06"></a>
## 06 – Bloquer des adresses IP

```apache
Order deny,allow
Deny from .aol.com
Deny from 192.168
Allow from 192.168.220.102
```

> Bloque tous sauf une adresse IP spécifique.

---

<a name="balise-07"></a>
## 07 – Rediriger HTTP vers HTTPS

### Variante 1

```apache
RewriteEngine On
RewriteCond %{Server_Port} !=443
RewriteRule ^(.*)$ https://votre-domaine.fr/$1 [R=301,L]
```

### Variante 2 (recommandée)

```apache
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}
```

---

<a name="balise-08"></a>
## 08 – Afficher un répertoire (index)

```apache
# Autoriser l'affichage de l'arborescence
Options +Indexes
```

---

<a name="balise-09"></a>
## 09 – Bloquer le Hotlinking

```apache
RewriteEngine on
RewriteCond %{HTTP_REFERER} !^$
RewriteCond %{HTTP_REFERER} !^https?://(www\.)?votre-domaine.fr/ [NC]
RewriteRule \.(gif|jpg|png|bmp|mp3|mp4|avi)$ - [F]
```

> Empêche d’autres sites d’afficher vos images ou fichiers multimédia.

---

<a name="balise-10"></a>
## 10 – Définir la police de caractères

```apache
# Par défaut UTF-8
AddDefaultCharset utf-8

# UTF-8 uniquement pour certains fichiers
AddDefaultCharset utf-8 .css .html .php
```

---

## ✅ Conclusion

Ces 10 astuces `.htaccess` vous permettent d’améliorer la sécurité, la performance, la personnalisation et l’ergonomie de votre site Web, tout en restant facilement déployables sans redémarrage de serveur.  
Elles sont **simples, efficaces** et adaptées à tout hébergement Apache sous **Debian 12 et 13**.

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
