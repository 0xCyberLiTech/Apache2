<div align="center">

  <br></br>

  <p align="center">
    <a href="https://github.com/0xCyberLiTech">
      <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ELAMP_" alt="Titre dynamique LAMP" />
    </a>
  </p>

  <br></br>

  <h2>Laboratoire numérique pour la cybersécurité, Linux & IT.</h2>

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

<div align="center">
  
## À propos & Objectifs.

</div>

Ce projet propose des solutions innovantes et accessibles en cybersécurité, avec une approche centrée sur la simplicité d’utilisation et l’efficacité. Il vise à accompagner les utilisateurs dans la protection de leurs données et systèmes, tout en favorisant l’apprentissage et le partage des connaissances.

Le contenu est structuré, accessible et optimisé SEO pour répondre aux besoins de :
- 🎓 Étudiants : approfondir les connaissances
- 👨‍💻 Professionnels IT : outils et pratiques
- 🖥️ Administrateurs système : sécuriser l’infrastructure
- 🛡️ Experts cybersécurité : ressources techniques
- 🚀 Passionnés du numérique : explorer les bonnes pratiques

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

<div align="center">

<table>
<tr>
<td align="center"><b>🖥️ Infrastructure &amp; Sécurité</b></td>
<td align="center"><b>💻 Développement &amp; Web</b></td>
<td align="center"><b>🤖 Intelligence Artificielle</b></td>
</tr>
<tr>
<td align="center">
  <a href="https://www.kernel.org/"><img src="https://skillicons.dev/icons?i=linux" width="48" title="Linux" /></a>
  <a href="https://www.debian.org"><img src="https://skillicons.dev/icons?i=debian" width="48" title="Debian" /></a>
  <a href="https://www.gnu.org/software/bash/"><img src="https://skillicons.dev/icons?i=bash" width="48" title="Bash" /></a>
  <br/>
  <a href="https://nginx.org"><img src="https://skillicons.dev/icons?i=nginx" width="48" title="Nginx" /></a>
  <a href="https://www.docker.com"><img src="https://skillicons.dev/icons?i=docker" width="48" title="Docker" /></a>
  <a href="https://git-scm.com"><img src="https://skillicons.dev/icons?i=git" width="48" title="Git" /></a>
</td>
<td align="center">
  <a href="https://www.python.org"><img src="https://skillicons.dev/icons?i=python" width="48" title="Python" /></a>
  <a href="https://flask.palletsprojects.com"><img src="https://skillicons.dev/icons?i=flask" width="48" title="Flask" /></a>
  <a href="https://developer.mozilla.org/docs/Web/HTML"><img src="https://skillicons.dev/icons?i=html" width="48" title="HTML5" /></a>
  <br/>
  <a href="https://developer.mozilla.org/docs/Web/CSS"><img src="https://skillicons.dev/icons?i=css" width="48" title="CSS3" /></a>
  <a href="https://developer.mozilla.org/docs/Web/JavaScript"><img src="https://skillicons.dev/icons?i=js" width="48" title="JavaScript" /></a>
  <a href="https://code.visualstudio.com"><img src="https://skillicons.dev/icons?i=vscode" width="48" title="VS Code" /></a>
</td>
<td align="center">
  <a href="https://pytorch.org"><img src="https://skillicons.dev/icons?i=pytorch" width="48" title="PyTorch" /></a>
  <a href="https://www.tensorflow.org"><img src="https://skillicons.dev/icons?i=tensorflow" width="48" title="TensorFlow" /></a>
  <a href="https://www.raspberrypi.com"><img src="https://skillicons.dev/icons?i=raspberrypi" width="48" title="Raspberry Pi" /></a>
  <br/><br/>
  <a href="https://ollama.com"><img src="https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white" alt="Ollama" /></a>
  &nbsp;
  <a href="https://anthropic.com"><img src="https://img.shields.io/badge/Anthropic-D97757?style=for-the-badge&logo=anthropic&logoColor=white" alt="Anthropic" /></a>
</td>
</tr>
</table>

<br/>

<b>🔒 Un projet proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Développé en collaboration avec <a href="https://claude.ai">Claude AI</a> (Anthropic) 🔒</b>

</div>


