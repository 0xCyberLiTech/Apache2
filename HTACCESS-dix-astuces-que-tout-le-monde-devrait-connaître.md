![Apache_logo](./images/Apache_logo.png)

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

## HTACCESS dix astuces que tout le monde devrait connaître.

👋 Sommaire des sujets abordés :

- [ 01 - Les pages d’erreur personnalisables.](#balise-01)
- [ 02 - Redirection.](#balise-02)
- [ 03 - Protection par mot de passe.](#balise-03)
- [ 04 - Augmenter la mémoire PHP.](#balise-04)
- [ 05 - Changer le fuseau horaire du serveur Web.](#balise-05)
- [ 06 - Bloquer des adresses IP.](#balise-06)
- [ 07 - Rediriger sa présence sur le Web de HTTP à HTTPS.](#balise-07)
- [ 08 - Activer l‘accès à des données sur un navigateur.](#balise-08)
- [ 09 - Interdire le Hotlinking d’images.](#balise-09)
- [ 10 - Définir la police de documents.](#balise-10)

Les fichiers de configuration .htaccess (en français : accès hypertexte) permettent aux Webmasters de paramétrer leurs règles relatives aux répertoires de leurs sites sur des serveurs NCSA tels que le HTTP d’Apache. Ces fichiers définissent par exemple quels utilisateurs ont le droit d’accès à certaines données. Un autre exemple typique d’astuce .htaccess serait la mise en place d’une redirection automatique.  

C’est quoi exactement un fichier .htaccess ?

Le terme .htaccess désigne un fichier texte dont l’utilisateur ayant les droits d’administration se sert pour configurer un serveur Web compatible à NCSA. Cette technique a été inventée dans les années 90 pour le serveur Web NCSA HTTPD, très innovant pour l’époque. Actuellement, elle intervient avant tout sur le serveur HTTP Apache dont l’exploitation est gérée par plusieurs fichiers centraux, les « httpd.conf ». Ces données de configuration supérieures sont enregistrées en règle générale dans un répertoire du programme du serveur Web et définis par l’administrateur du serveur. Ils déterminent si un utilisateur a le droit de modifier la configuration du serveur grâce à des astuces .htaccess. Si oui, celui-ci peut alors créer et modifier des fichiers .htaccess pour chaque nouveau répertoire et écraser quelques parties de la configuration via des répertoires de niveau supérieur.

A chaque consultation de page, le serveur Web scanne la totalité de ces répertoires supérieurs sans en sauvegarder les informations (le .htaccess d’un sous répertoire écrase donc celui d’un supérieur). Les réglages du serveur qui ont été réalisés avec un fichier .htaccess sont valables dès que celui-ci est déposé sur le répertoire approprié, sans nécessiter de redémarrer le serveur. L’écriture ne doit comporter aucune erreur car elle pourrait empêcher l’accès à tout le serveur. L’application de ces astuces .htaccess à la lettre peut vraiment faciliter la gestion d’un serveur. Étant donné l’aisance et la rapidité de leur insertion dans la structure existante, on parle aussi souvent d’astuces .htaccess.
Comment créer un fichier .htaccess

Étant donné qu’il s’agit de fichiers textes purs, il est possible de les créer et de les modifier avec n’importe quel éditeur. Le processus de création d’un fichier .htaccess est différent en fonction des accès disponibles sur le serveur Web. Les serveurs Telnet ou SSH proposent de le créer et de le modifier directement sur la plateforme serveur. Si vous n'avez qu’un accès FTP à disposition, le fichier devra alors être créé localement et ensuite être téléchargé. Si le nom commence par un point, c’est qu’il s’agit d’un fichier de répertoire de système Unix. Celui-ci sera alors considéré comme « caché » et apparaîtra invisible lors de l’utilisation de clients FTP.

Ce point peut engendrer un problème lors de la création d’un .htaccess local sur un système Windows mais se résout rapidement. Ainsi, l’éditeur n’attachera pas l’extension .txt si le fichier est enregistré sous « tout fichier ». Si le fichier .htaccess contient la bonne directive, il sera expédié dans le bon répertoire et sera tout de suite valide. Cela concerne aussi tout le sous-répertoire.
Configurer un serveur via une astuce (.htaccess).

Les utilisateurs autorisés par les administrateurs ont la possibilité via les fichiers .htaccess d’influencer rapidement la configuration de serveurs Web. Ils peuvent par exemple protéger des répertoires entiers d’accès illégaux via une authentification HTTP. Par ailleurs, des pages d’erreurs ou de redirection peuvent s’afficher. Il existe un certain nombre de conseils avec .htaccess. En voici les dix principaux.

<a name="balise-01"></a>

## 01 - Les pages d’erreur personnalisables.

Les serveurs Web peuvent afficher par défaut des fichiers HTML standards voire des avertissements codés si une erreur survient lors d’un accès à un site Internet. Ces messages d’erreurs sont souvent bruts et ne sont pas agréables pour les utilisateurs. Il est possible avec le fichier .htaccess de créer des pages personnalisées qui se marieront mieux avec la charte graphique de votre site Internet. Voici le code à intégrer dans ce cas :
```
# Votre message d’erreur de l’emplacement local
ErrorDocument 404 / erreur/404.html
```
Si la page d’erreur se trouve au niveau supérieur du répertoire racine ou d’une URL externe, l’URL complète peut aussi être incorporée dans le .htaccess qui se trouve dans ce cas dans le répertoire racine :
```
# Votre message d’erreur de l’emplacement externe
ErrorDocument 404 / http://www.nom-de-votre-site.com/erreur/404.html
```
<a name="balise-02"></a>
## 02 - Redirection.

Une des possibilités d’action des fichiers .htaccess est de rediriger les utilisateurs vers d’autres pages. Vous pouvez par exemple transférer des données uniques à l’intérieur d’un même site Web mais aussi vers un autre domaine. C’est pratique avant tout si vous changez de site Internet. Le code suivant est enregistré dans le répertoire racine et veille à ce que les demandes au domaine premier soient redirigées vers le nouveau :
```
# Redirection simple
Redirect / http://www.nouveau-domaine.fr/
```
Les données uniques peuvent être transférées via la même méthode à l’intérieur d’un même site Internet, par exemple si celui-ci change de nom :
```
# Redirection de données uniques
Redirect /ancienne-page.html nouvelle-page.html
```
<a name="balise-03"></a>
## 03 - Protection par mot de passe.

Vous ne souhaitez pas écrire de scripts trop compliqués avec PHP mais vous avez besoin d’un répertoire ou de fichiers protégés sur votre serveur Web ? Vous pouvez alors à la place utiliser des astuces .htaccess pour la création de votre domaine. Pour bénéficier de cette protection de mots de passe, il vous faudra un deuxième fichier avec le nom .htpasswd dans lequel les mots de passe seront enregistrés. Ceux-ci peuvent être encodés sous le système Unix, il existe pour cela différents générateurs de .htpasswd sur la Toile. Ces répertoires protégés peuvent être créés ainsi :
```
# Protection simple de mot de passe avec .htaccess
AuthType Basic
AuthName "fichiers réservés"
AuthUserFile /< chemin absolu vers le fichier mot de passe >/.htpasswd
AuthPGAuthoritative Off
require user User1 User2 User3
```
Autre exemple :
```
AuthType Basic
AuthName "Zone protégée par mot de passe."
AuthUserFile /var/www/.htpasswd
Require valid-user
```
Le .htpasswd est créé en même temps que les nouveaux mots de passe codés des utilisateurs :
```
# données .htpasswd, identifiants et mots de passe
User1:duCmo1zxkKx6Y
User2:mou3IYjSLpGWI
User3:HGKS9XzDXXAXQ
```
Pendant que le fichier .htpasswd est classé en haut du répertoire racine, le .htaccess doit se trouver dans le celui qui est protégé.

<a name="balise-04"></a>
## 04 - Augmenter la mémoire PHP.

L’utilisation d’applications PHP est soumise à une limite de mémoire causée par les scripts PHP sur le serveur. Celle-ci peut être augmentée en fonction des besoins en utilisant la directive suivante :
```
# PHP Memory Limit
php_value memory_limit 128M
```
La valeur de 128 M équivaut dans ce cas à une limite de 128 MegaBytes. D’autres limites peuvent être réglées en tenant compte des besoins de stockage et des exigences en matière de serveurs.

<a name="balise-05"></a>
## 05 - Changer le fuseau horaire du serveur Web.

Il est possible d’adapter le fuseau horaire sur le .htaccess si le serveur Web est réglé sur une heure erronée :
```
# Insérer le fuseau horaire
SetEnv TZ Europe/Paris
```
<a name="balise-06"></a>
## 06 - Bloquer des adresses IP.

Il est possible de refuser l’accès de sites Internet à des adresses ou domaines IP. Avec le code adéquat, il est même possible d’interdire l’accès à toutes les adresses IP tout en le garantissant à une poignée. Ainsi, l’offre Internet peut être mise à la disposition de seulement quelques employés sur l’intranet d’une entreprise. La directive suivante résume certaines des limitations d’accès possibles :
```
# Fichiers pour réguler les zones IP
Order deny,allow
Deny from .aol.com
Deny from 192.168
Allow from 192.168.220.102`
```
L’entrée « Order » permet de définir l’ordre de l’interprétation des données, le sens n’est donc pas important. Les autres entrées communiquent au serveur que tous les utilisateurs de aol.com ainsi que ceux dont l’adresse de domaine est 192.168 n’ont pas le droit d’utiliser le site Internet. L’exception est pour l’utilisateur de l’adresse IP 192.168.220.102.

<a name="balise-07"></a>
## 07 - Rediriger sa présence sur le Web de HTTP à HTTPS.

Si vous utilisez un certificat SSL pour votre domaine, il est possible de le rediriger via une directive .htaccess sur une requête HTTPS codé.
```
# Activez HTTPS
RewriteEngine On
RewriteCond %{Server_Port} !=443
RewriteRule ^(.*)$ https://votre-domaine.fr/$1 [R=301,L]
```
Autre exemple :
```
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}
```
<a name="balise-08"></a>
## 08 - Activer l‘accès à des données sur un navigateur.

Grâce à cette directive, vous pouvez afficher le contenu du répertoire et proposer à d’autres utilisateurs de le télécharger :
```
# Montrez le contenu du répertoire
Options +Indexes
```
<a name="balise-09"></a>
## 09 - Interdire le Hotlinking d’images.

Le Hotlinking permet à une tierce personne d’utiliser l’adresse d’un fichier publié sur un site Internet, le plus souvent une image, et de l’afficher sur un autre site sans l’enregistrer sur son propre serveur. Cela entraîne une augmentation du volume de données sur le site d’origine, sans que son propriétaire ne puisse l’influencer. Cette astuce .htaccess permet de bloquer ces liens grâce à la directive suivante :
```
# Hotlinking interdit 
RewriteEngine on 
RewriteCond %{HTTP_REFERER} !^$ 
RewriteCond %{HTTP_REFERER} !^http:// www.votre-domaine-d-hebergement/.*$ [NC] [OR]
RewriteCond %{HTTP_REFERER} !^http://www.votre-domaine-d-hebergement /.*$ [NC] [OR]
RewriteRule .*\.(gif|GIF|jpg|JPG|bmp|BMP|wav|mp3|wmv|avi|mpeg)$ - [F]
```
<a name="balise-10"></a>
## 10 - Définir la police de documents.

Les accents peuvent poser problème si aucun codage de caractères n’existe. Il est possible de définir avec un fichier .htaccess quel codage de caractère doit être utilisé pour chaque document type. La directive suivante caractérise le codage UTF-8 pour tous les documents :
```
# Définir le codage de caractères
AddDefaultCharset utf-8
```
Voici la directive à intégrer au cas où seuls quelques types de documents doivent être définis par codage :
```
# Définir le codage de caractères pour certains fichiers 
AddDefaultCharset utf-8 .css .htm .html .xhtml .php 
```
Les astuces .htaccess : pratiques et simples à utiliser :

Voici une partie de la longue liste d’astuces .htaccess possibles. Ces fichiers pratiques servent à configurer les serveurs. Toutes les directives sont directement dirigées par le serveur Web sans nécessiter de redémarrage complet.

Source : https://www.ionos.fr/digitalguide/hebergement/aspects-techniques/les-meilleures-astuces-htaccess/

---

**Mise à jour :** Juillet 2025

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
