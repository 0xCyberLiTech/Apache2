<div align="center">

  ![Apache_logo](./images/Apache_logo.png)

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
> 🎯 **Objectif :** proposer un contenu clair, structuré et accessible pour étudiants, curieux et professionnels de l’IT.  
> 🔗 [Mon GitHub principal](https://github.com/0xCyberLiTech)

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim" alt="Skills" />
  </a>
</p>

---

### 🎯 **Objectif de ce dépôt.**

> Ce dépôt a pour vocation de centraliser un ensemble de notions clés concernant la pile LAMP (Linux, Apache, MySQL/MariaDB, PHP/Perl/Python). Il s’adresse aux passionnés, étudiants et professionnels souhaitant
> mieux comprendre cette architecture web open-source, apprendre à déployer et gérer des applications basées sur LAMP, et se familiariser avec les concepts et outils essentiels à son bon fonctionnement et à son
> optimisation.

---

## Protéger l’accès d’un répertoire, d’une page par (.htaccess), (.htpasswd).
 
Il est parfois nécessaire de protéger l’accès à une page, à un répertoire sur un serveur web (Ex : répertoire d’administration, contenant des données sensibles) afin d’éviter que n’importe qui puisse y accéder.

Il y a différentes méthodes, on peut avoir recours à des langages comme le PHP, ASP, PERL …)

Mais la méthode la plus simple est d’utiliser le mécanisme de protection du serveur apache.

C’est-à-dire effectuer une protection à l’aide des fichiers (.htaccess et .htpasswd.) on estime ici que l’on n’a pas accès au fichier de configuration http.conf, ce qui est le cas chez un fournisseur d’accès.

Le fichier (.htaccess) est un fichier texte contenant des commandes Apache.

Voici un exemple, nous allons protéger l'accès au sous-dossier /var/www/html.

Nous allons créer le fichier suivant :
```
touch /var/www/html/.htaccess
```
Nous y déposerons le contenu suivant :
```
AuthType Basic
AuthName "Zone protégée par mot de passe."
AuthUserFile /var/www/.htpasswd
Require valid-user
```
Quelques explications :

AuthUserFile : c’est le nom et le chemin d’accès du fichier qui contiendra les noms des utilisateurs et les mots de passe associés. Ce chemin doit partir de la racine du site.

Ici, les mots de passe seront dans (/var/www/.htpasswd).

On peut, et il est même conseillé de choisir un autre nom que .htpasswd pour le fichier qui contiendra le couple utilisateur/mot de passe.

Le point précédent le nom de fichier permettra de cacher (au sens Unix /linux du terme).
Il est également recommandé de mettre le fichier des mots de passe en dehors de l’arborescence du site si l’on en a la possibilité.

AuthGroupFile : permet de définir un droit d’accès à un groupe d’utilisateur.
Cette solution n’est que rarement utilisée pour un site Web.

Le reste du temps, il pointe vers (/dev/null). Il faut que cette ligne soit présente.

AuthName : c’est le texte qui apparaîtra dans la fenêtre demandant le mot de passe.

AuthType : l’authentification est en général « basic ». Les mots de passe sont alors envoyés en clair sur le réseau.

Ce système n’est supporté que par certains navigateurs.

Limit : c’est ici qu’on va indiquer ce qui est autorisé et interdit dans le répertoire.

Les commandes GET et POST indiquent la récupération de pages web et la réponse à certains formulaires.

POST est utilisé pour autoriser l’upload de fichiers sous le protocole http.

Require valid-user : accepte tous les utilisateurs qui ont un login : mot de passe dans (.htpasswd).

Require herve jacques : limite l’accès à un ou plusieurs utilisateurs précis, ici herve et jacques.

A noter que les utilisateurs sont séparés par des espaces.

Une fois le fichier (.htaccess) créé, il faut le placer dans le répertoire à protéger.

Maintenant, il nous faut créer le fichier (.htpasswd)

Sous unix et inux il existe un l’utilitaire : (htpasswd).
```
htpasswd -Bc [Nom de fichier] [Nom d'utilisateur]
```
```
htpasswd -Bc /var/www/.htpasswd 0xCLT
```
Votre mot de passe vous sera demandé, puis une deuxième fois pour confirmation.
```
    @0xCLT:~# htpasswd -Bc /var/www/.htpasswd 0xCLT
New password:
Re-type new password:
Adding password for user 0xCLT
```
Le mot de passe est stocké crypté avec bcrypt dans le fichier que vous avez créé.
```
cat /var/www/.htpasswd
```
Si l’on édite le fichier .htpasswd obtient une ligne du style :
```
0xCLT:$2ypopojmlm$05$RxuLau6X2SbRidfsdfzpFLKheEeXfgdylsVBWgI
```
Notez que l'option -c crée un nouveau fichier et supprime les entrées existantes.

Si vous souhaitez modifier une entrée existante ou ajouter une nouvelle entrée, utilisez uniquement l'option -B.
```
htpasswd -B [Nom de fichier] [Nom d'utilisateur]
```
Ce qui correspond au nom d’utilisateur (login) et son mot de passe crypté.

Il y aura une ligne pour chaque utilisateur.

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
