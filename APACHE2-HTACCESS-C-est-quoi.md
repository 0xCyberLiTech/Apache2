<div align="center">
  <br>
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ELAMP_" alt="Titre dynamique LAMP" />
  </a>
  <br>
  <p align="center">
    <em>Qu’est-ce qu’un fichier <b>.htaccess</b>.</em><br>
    <b>🌐 Web – 🔐 Sécurité – 🚀 Performance</b>
  </p>
  <!-- Badges -->
  [![🔗 Profil GitHub](https://img.shields.io/badge/Profil-GitHub-181717?logo=github&style=flat-square)](https://github.com/0xCyberLiTech)
  [![📦 Dernière version](https://img.shields.io/github/v/release/0xCyberLiTech/Apache2?label=version&style=flat-square&color=blue)](https://github.com/0xCyberLiTech/Apache2/releases/latest)
  [![📄 CHANGELOG](https://img.shields.io/badge/📄%20Changelog-Apache2-blue?style=flat-square)](https://github.com/0xCyberLiTech/Apache2/blob/main/CHANGELOG.md)
  [![📂 Dépôts publics](https://img.shields.io/badge/Dépôts-publics-blue?style=flat-square)](https://github.com/0xCyberLiTech?tab=repositories)
  [![👥 Contributeurs](https://img.shields.io/badge/👥%20Contributeurs-cliquez%20ici-007ec6?style=flat-square)](https://github.com/0xCyberLiTech/Apache2/graphs/contributors)
</div>


### 👨‍💻 À propos de moi

> Bienvenue dans mon **laboratoire numérique personnel** dédié à l’apprentissage et à la vulgarisation de la cybersécurité.  
> Passionné par **Linux**, la **cryptographie** et les **systèmes sécurisés**, je partage ici mes notes, expérimentations et fiches pratiques.  
>  
> Proposer un contenu clair, structuré et accessible pour étudiants, curieux et professionnels de l’IT.  
> 🔗 [Mon GitHub principal](https://github.com/0xCyberLiTech)

<p align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim" alt="Skills" width="300">
  </a>
</p>


### 🎯 Objectif du dépôt

> Ce dépôt centralise des notions clés sur la pile LAMP (Linux, Apache, MySQL/MariaDB, PHP/Perl/Python).  
> Il s’adresse aux passionnés, étudiants et professionnels souhaitant mieux comprendre cette architecture open-source, apprendre à déployer et gérer des applications LAMP, et maîtriser les outils essentiels à son bon fonctionnement.


## Sommaire rapide

| Nº  | Sujet                                  | Lien                                |
|------|---------------------------------------|------------------------------------|
| 01   | Qu’est-ce qu’un fichier `.htaccess` ? | [![Voir](https://img.shields.io/badge/Voir-01-blue)](#quest-ce-quun-fichier-htaccess)  |
| 02   | Comment créer un fichier `.htaccess` ? | [![Voir](https://img.shields.io/badge/Voir-02-blue)](#comment-créer-un-fichier-htaccess) |


## 01 - Qu’est-ce qu’un fichier `.htaccess` ? <a name="quest-ce-quun-fichier-htaccess"></a>

Un fichier `.htaccess` est un fichier texte utilisé par l’administrateur d’un serveur Apache pour configurer certains paramètres de façon fine, répertoire par répertoire.


**Attention :** une erreur dans ce fichier peut provoquer des erreurs sur le site.

Cette méthode facilite la gestion rapide et ciblée des paramètres du serveur.


## 02 - Comment créer un fichier `.htaccess` ? <a name="comment-créer-un-fichier-htaccess"></a>

  - En SSH ou Telnet : créez-le directement sur le serveur dans le répertoire souhaité.
  - En FTP : créez-le localement, puis envoyez-le sur le serveur.


## Exemple pédagogique simple

Imaginons que vous souhaitiez interdire l’affichage de la liste des fichiers dans un dossier `/var/www/html/mon-site/` :

1. Créez un fichier `.htaccess` dans ce dossier.

2. Ajoutez la ligne suivante :

   ```apache
   Options -Indexes
   ```

3. Sauvegardez et déposez le fichier sur le serveur (si localement).

4. À présent, si quelqu’un visite ce dossier sans page index, il verra une erreur plutôt qu’une liste de fichiers.


**💡 Cette simplicité permet de gérer finement votre serveur web, dossier par dossier, en toute sécurité.**


## Pour aller plus loin

Découvrez d’autres astuces pratiques avec `.htaccess` dans ce tuto complémentaire :  

| Nº  | Sujet                                  | Lien                                   |
|------|---------------------------------------|---------------------------------------|
| 01   | Les 10 astuces `.htaccess` indispensables | [![Voir](https://img.shields.io/badge/Voir-HTACCESS--astuces-blue)](./HTACCESS-dix-astuces-que-tout-le-monde-devrait-connaître.md) |


<!-- ===== FOOTER ===== -->
<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>
<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>

