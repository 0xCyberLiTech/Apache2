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

## Protéger l’accès d’un répertoire ou d’une page avec (.htaccess) et (.htpasswd).

Il est parfois nécessaire de protéger l’accès à une page ou à un répertoire sur un serveur web (par exemple, un répertoire d’administration contenant des données sensibles), afin d’éviter que n’importe qui puisse y accéder.

Différentes méthodes existent, notamment en utilisant des langages comme PHP, ASP, Perl, etc.  
Cependant, la méthode la plus simple consiste à utiliser le mécanisme de protection du serveur Apache.

Ici, on part du principe que vous **n’avez pas accès au fichier de configuration `httpd.conf`** (cas fréquent chez un hébergeur mutualisé).

## Principe

Le fichier `.htaccess` est un fichier texte contenant des directives Apache, placé dans le répertoire à protéger.

---

## Exemple : protéger le répertoire `/var/www/html`

On commence par créer le fichier `.htaccess` :

```bash
touch /var/www/html/.htaccess
```

Puis, on y dépose le contenu suivant :

```apache
AuthType Basic
AuthName "Zone protégée par mot de passe."
AuthUserFile /var/www/.htpasswd
Require valid-user
```

---

## Explications des directives

- **AuthUserFile** : chemin absolu vers le fichier contenant les couples utilisateurs / mots de passe.  
  Exemple ici : `/var/www/.htpasswd`.

  > Il est conseillé de choisir un nom différent de `.htpasswd` pour plus de sécurité.  
  > Ce fichier doit idéalement être **hors de la racine web** pour éviter toute exposition.

- **AuthGroupFile** : permet de définir un fichier contenant des groupes d’utilisateurs (peu utilisé, souvent pointé vers `/dev/null`).

- **AuthName** : message qui s’affiche dans la fenêtre d’authentification.

- **AuthType** : type d’authentification. Le plus courant est `Basic`, qui transmet les mots de passe en clair (non chiffrés) — attention à ne pas l’utiliser sur un site non sécurisé en HTTPS.

- **Require valid-user** : accepte tous les utilisateurs définis dans le fichier `.htpasswd`.  
  On peut restreindre à des utilisateurs précis avec :  
  ```apache
  Require user herve jacques
  ```
  (séparer les noms d’utilisateur par des espaces).

---

## Exemple complet avec `.htaccess` placé dans le répertoire à protéger

```apache
AuthType Basic
AuthName "Zone protégée par mot de passe."
AuthUserFile /var/www/.htpasswd
Require valid-user
```

---

## Création du fichier `.htpasswd`

Sous Linux/Unix, on utilise l’utilitaire `htpasswd` :

```bash
htpasswd -Bc /var/www/.htpasswd utilisateur
```

Exemple :

```bash
htpasswd -Bc /var/www/.htpasswd 0xCLT
```

- `-B` : utilise bcrypt (plus sécurisé) pour le chiffrement du mot de passe  
- `-c` : crée un nouveau fichier `.htpasswd` (attention : écrase l’ancien fichier)

Le système vous demandera le mot de passe deux fois.

---

## Contenu du fichier `.htpasswd`

Pour voir le contenu (crypté) :

```bash
cat /var/www/.htpasswd
```

Exemple de ligne :

```
0xCLT:$2y$10$RxuLau6X2SbRidfsdfzpFLKheEeXfgdylsVBWgI
```

---

## Ajouter ou modifier un utilisateur

Pour ajouter un utilisateur sans écraser le fichier existant, ne pas utiliser `-c` :

```bash
htpasswd -B /var/www/.htpasswd nouvel_utilisateur
```
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

