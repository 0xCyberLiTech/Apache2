<div align="center">

  <br></br>
  
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ELAMP_" alt="Titre dynamique LAMP" />
  </a>
  
  <br></br>

  <p align="center">
    <em>Qu’est-ce qu’un fichier **.htaccess**.</em><br>
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

# 🎯 Objectif de ce dépôt

> Ce dépôt centralise des notions clés sur la pile LAMP (Linux, Apache, MySQL/MariaDB, PHP/Perl/Python).  
> Il s’adresse aux passionnés, étudiants et professionnels souhaitant mieux comprendre cette architecture open-source, apprendre à déployer et gérer des applications LAMP, et maîtriser les outils essentiels à son bon fonctionnement.

---

## Sommaire rapide

| Nº  | Sujet                                  | Lien                                |
|------|---------------------------------------|------------------------------------|
| 01   | Qu’est-ce qu’un fichier `.htaccess` ? | [![Voir](https://img.shields.io/badge/Voir-01-blue)](#quest-ce-quun-fichier-htaccess)  |
| 02   | Comment créer un fichier `.htaccess` ? | [![Voir](https://img.shields.io/badge/Voir-02-blue)](#comment-créer-un-fichier-htaccess) |

---

## 01 - Qu’est-ce qu’un fichier `.htaccess` ? <a name="quest-ce-quun-fichier-htaccess"></a>

Un fichier `.htaccess` est un fichier texte utilisé par l’administrateur d’un serveur Apache pour configurer certains paramètres de façon fine, répertoire par répertoire.

- Cette technique date des années 90 avec le serveur NCSA HTTPD.
- Aujourd’hui, elle est principalement utilisée avec Apache.
- Le serveur Apache possède des fichiers de configuration principaux (`httpd.conf`), mais permet aussi aux utilisateurs autorisés de surcharger certains paramètres grâce aux fichiers `.htaccess`.
- Ces fichiers sont placés dans des répertoires spécifiques et sont lus à chaque requête, **sans nécessiter de redémarrage du serveur**.
- Le `.htaccess` d’un sous-répertoire remplace ou complète celui d’un répertoire supérieur.

**Attention :** une erreur dans ce fichier peut provoquer des erreurs sur le site.

Cette méthode facilite la gestion rapide et ciblée des paramètres du serveur.

---

## 02 - Comment créer un fichier `.htaccess` ? <a name="comment-créer-un-fichier-htaccess"></a>

- Le fichier `.htaccess` est un simple fichier texte.  
- Vous pouvez le créer/modifier avec n’importe quel éditeur (nano, vim, Notepad++, VSCode, etc.).
- Selon vos accès serveur :
  - En SSH ou Telnet : créez-le directement sur le serveur dans le répertoire souhaité.
  - En FTP : créez-le localement, puis envoyez-le sur le serveur.
- Le fichier doit **commencer par un point** (`.`), ce qui le rend caché sous Unix/Linux.
- Sous Windows, faites attention à ne pas ajouter l’extension `.txt` en sauvegardant, sinon le serveur ne le reconnaîtra pas.
- Le fichier `.htaccess` sera valide dès sa mise en place, sans redémarrage.

---

## Exemple pédagogique simple

Imaginons que vous souhaitiez interdire l’affichage de la liste des fichiers dans un dossier `/var/www/html/mon-site/` :

1. Créez un fichier `.htaccess` dans ce dossier.

2. Ajoutez la ligne suivante :

   ```apache
   Options -Indexes
   ```

3. Sauvegardez et déposez le fichier sur le serveur (si localement).

4. À présent, si quelqu’un visite ce dossier sans page index, il verra une erreur plutôt qu’une liste de fichiers.

---

**💡 Cette simplicité permet de gérer finement votre serveur web, dossier par dossier, en toute sécurité.**

---

## Pour aller plus loin

Découvrez d’autres astuces pratiques avec `.htaccess` dans ce tuto complémentaire :  

| Nº  | Sujet                                  | Lien                                   |
|------|---------------------------------------|---------------------------------------|
| 01   | Les 10 astuces `.htaccess` indispensables | [![Voir](https://img.shields.io/badge/Voir-01-blue)](https://github.com/0xCyberLiTech/Apache2/blob/main/APACHE2-HTACCESS-dix-astuces-que-tout-le-monde-devrait-conna%C3%AEtre.md) |

---

<p align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</p>

