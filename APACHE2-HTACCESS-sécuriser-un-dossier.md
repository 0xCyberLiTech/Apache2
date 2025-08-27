<div align="center">

  <br></br>

  <p align="center">
    <a href="https://github.com/0xCyberLiTech">
      <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ELAMP_" alt="Titre dynamique LAMP" />
    </a>
  </p>

  <br></br>

  <p align="center">
    <em>Protéger l’accès d’un répertoire ou d’une page avec (.htaccess) et (.htpasswd).</em><br>
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

</div>

---

### 👨‍💻 **À propos de moi**

> Bienvenue sur le dépôt <strong>0xCyberLiTech</strong>, votre laboratoire numérique pour l'<strong>apprentissage</strong> et la <strong>vulgarisation</strong> de la <strong>cybersécurité</strong>, de l'<strong>administration Linux Debian</strong> et de la <strong>sécurité informatique</strong>.
> Passionné par <strong>Linux</strong>, la <strong>cryptographie</strong>, la <strong>supervision réseau</strong> et les <strong>systèmes sécurisés</strong>, je partage ici des <strong>tutoriels</strong>, <strong>guides pratiques</strong>, <strong>fiches techniques</strong> et <strong>retours d'expérience</strong> pour renforcer vos compétences IT.
>
> 🎯 <strong>Objectif :</strong> Offrir un contenu structuré, accessible et optimisé pour le référencement naturel, destiné aux étudiants, professionnels, administrateurs système, experts en sécurité et curieux du monde numérique.

<p align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim,python,markdown" alt="Skills" width="420">
  </a>
</p>

---

### 🎯 **Objectif de ce dépôt.**

> Ce dépôt a pour vocation de centraliser un ensemble de notions clés concernant la pile LAMP (Linux, Apache, MySQL/MariaDB, PHP/Perl/Python). Il s’adresse aux passionnés, étudiants et professionnels souhaitant
> mieux comprendre cette architecture web open-source, apprendre à déployer et gérer des applications basées sur LAMP, et se familiariser avec les concepts et outils essentiels à son bon fonctionnement et à son
> optimisation.

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

<p align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim,python,markdown" alt="Skills" width="420">
  </a>
</p>

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
