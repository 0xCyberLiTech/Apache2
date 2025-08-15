<div align="center">

  <br></br>
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ELAMP_" alt="Titre dynamique LAMP" />
  </a>
  <br></br>

  <p align="center">
    <em>Protéger l’accès d’un répertoire ou d’une page avec (.htaccess) et (.htpasswd).</em><br>
    <b>🌐 Web – 🔐 Sécurité – 🚀 Performance</b>
  </p>

  [![🔗 Profil GitHub](https://img.shields.io/badge/Profil-GitHub-181717?logo=github&style=flat-square)](https://github.com/0xCyberLiTech)
  [![📦 Dernière version](https://img.shields.io/github/v/release/0xCyberLiTech/Apache2?label=version&style=flat-square&color=blue)](https://github.com/0xCyberLiTech/Apache2/releases/latest)
  [![📄 CHANGELOG](https://img.shields.io/badge/📄%20Changelog-Apache2-blue?style=flat-square)](https://github.com/0xCyberLiTech/Apache2/blob/main/CHANGELOG.md)
  [![📂 Dépôts publics](https://img.shields.io/badge/Dépôts-publics-blue?style=flat-square)](https://github.com/0xCyberLiTech?tab=repositories)
  [![👥 Contributeurs](https://img.shields.io/badge/👥%20Contributeurs-cliquez%20ici-007ec6?style=flat-square)](https://github.com/0xCyberLiTech/Apache2/graphs/contributors)

</div>


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


### 🎯 **Objectif de ce dépôt.**

> Ce dépôt a pour vocation de centraliser un ensemble de notions clés concernant la pile LAMP (Linux, Apache, MySQL/MariaDB, PHP/Perl/Python). Il s’adresse aux passionnés, étudiants et professionnels souhaitant
> mieux comprendre cette architecture web open-source, apprendre à déployer et gérer des applications basées sur LAMP, et se familiariser avec les concepts et outils essentiels à son bon fonctionnement et à son
> optimisation.


## Protéger l’accès d’un répertoire ou d’une page avec (.htaccess) et (.htpasswd).

Il est parfois nécessaire de protéger l’accès à une page ou à un répertoire sur un serveur web (par exemple, un répertoire d’administration contenant des données sensibles), afin d’éviter que n’importe qui puisse y accéder.

Différentes méthodes existent, notamment en utilisant des langages comme PHP, ASP, Perl, etc.  
Cependant, la méthode la plus simple consiste à utiliser le mécanisme de protection du serveur Apache.

Ici, on part du principe que vous **n’avez pas accès au fichier de configuration `httpd.conf`** (cas fréquent chez un hébergeur mutualisé).

## Principe

Le fichier `.htaccess` est un fichier texte contenant des directives Apache, placé dans le répertoire à protéger.


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


## Explications des directives

  Exemple ici : `/var/www/.htpasswd`.

  > Il est conseillé de choisir un nom différent de `.htpasswd` pour plus de sécurité.  
  > Ce fichier doit idéalement être **hors de la racine web** pour éviter toute exposition.




  On peut restreindre à des utilisateurs précis avec :  
  ```apache
  Require user herve jacques
  ```
  (séparer les noms d’utilisateur par des espaces).


## Exemple complet avec `.htaccess` placé dans le répertoire à protéger

```apache
AuthType Basic
AuthName "Zone protégée par mot de passe."
AuthUserFile /var/www/.htpasswd
Require valid-user
```


## Création du fichier `.htpasswd`

Sous Linux/Unix, on utilise l’utilitaire `htpasswd` :

```bash
htpasswd -Bc /var/www/.htpasswd utilisateur
```

Exemple :

```bash
htpasswd -Bc /var/www/.htpasswd 0xCLT
```


Le système vous demandera le mot de passe deux fois.


## Contenu du fichier `.htpasswd`

Pour voir le contenu (crypté) :

```bash
cat /var/www/.htpasswd
```

Exemple de ligne :

```
0xCLT:$2y$10$RxuLau6X2SbRidfsdfzpFLKheEeXfgdylsVBWgI
```


## Ajouter ou modifier un utilisateur

Pour ajouter un utilisateur sans écraser le fichier existant, ne pas utiliser `-c` :

```bash
htpasswd -B /var/www/.htpasswd nouvel_utilisateur
```

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
