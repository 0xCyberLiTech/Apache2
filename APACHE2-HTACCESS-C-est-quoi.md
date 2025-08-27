<div align="center">

  <br></br>

  <p align="center">
    <a href="https://github.com/0xCyberLiTech">
      <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ELAMP_" alt="Titre dynamique LAMP" />
    </a>
  </p>

  <br></br>

  <h2>Laboratoire numérique pour la cybersécurité, Linux & IT</h2>

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

<!--
Optimisation SEO : mots-clés cybersécurité, Linux, administration système, sécurité informatique, tutoriels, guides, expertise, formation, supervision, Docker, OpenVAS, firewall, proxy, DNS, SSH, Debian, IT, réseau, cryptographie, open source, ressources techniques, étudiants, professionnels, passionnés.
-->

<div align="center">
  <img src="https://img.icons8.com/fluency/96/000000/cyber-security.png" alt="CyberSec" width="80"/>
</div>

<div align="center">
  <p>
    <strong>Cybersécurité</strong> <img src="https://img.icons8.com/color/24/000000/lock--v1.png"/> • <strong>Linux Debian</strong> <img src="https://img.icons8.com/color/24/000000/linux.png"/> • <strong>Sécurité informatique</strong> <img src="https://img.icons8.com/color/24/000000/shield-security.png"/>
  </p>
</div>

---

## 🚀 À propos & Objectifs

Ce projet propose des solutions innovantes et accessibles en cybersécurité, avec une approche centrée sur la simplicité d’utilisation et l’efficacité. Il vise à accompagner les utilisateurs dans la protection de leurs données et systèmes, tout en favorisant l’apprentissage et le partage des connaissances.

Le contenu est structuré, accessible et optimisé SEO pour répondre aux besoins de :
- 🎓 Étudiants : approfondir les connaissances
- 👨‍💻 Professionnels IT : outils et pratiques
- 🖥️ Administrateurs système : sécuriser l’infrastructure
- 🛡️ Experts cybersécurité : ressources techniques
- 🚀 Passionnés du numérique : explorer les bonnes pratiques

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

<div align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim,python,markdown" alt="Skills" width="440">
  </a>
</div>

<div align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</div>
