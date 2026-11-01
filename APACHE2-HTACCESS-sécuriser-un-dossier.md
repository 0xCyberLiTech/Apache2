<!-- MASTER-HEADER-START -->
<div align="center">

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/headers/header-apache2.svg" alt="ATELIER APACHE2 & LAMP // SERVEUR WEB" width="100%" />
</a>

<p align="center">
  <a href="https://0xcyberlitech.com/"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-portal.svg" alt="Portail 0xCyberLiTech.com" width="24%" /></a>
  <a href="https://0xcyberlitech.com/soc-rd.html"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-soc-rd.svg" alt="Livre Blanc SOC Cockpit" width="24%" /></a>
  <a href="https://0xcyberlitech.com/jarvis-rd.html"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-jarvis-rd.svg" alt="Livre Blanc JARVIS IA" width="24%" /></a>
  <a href="https://github.com/0xCyberLiTech?tab=repositories"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-github.svg" alt="Catalogue des 23 Dépôts" width="24%" /></a>
</p>
<p align="center">
  <a href="README.md"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-back-readme.svg" alt="Retour au sommaire du dépôt" width="340" /></a>
</p>

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/divider-hud.svg" alt="" width="100%" />
</div>
<!-- MASTER-HEADER-END -->

<!-- DEBIAN-TRUTH-START -->
> [!IMPORTANT]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="18" height="18" align="absmiddle" alt="" /> ** Matrice Officielle Debian — `Debian 12 (Bookworm)` · `Debian 13 (Trixie)` · `Debian 14 (Forky)`**
> - **Sources Officielles Debian.org (`apache2`) :** `Bookworm (12)` : **`2.4.68-1~deb12u1`** &nbsp;·&nbsp; `Trixie (13 — Stable)` : **`2.4.68-1~deb13u1`** &nbsp;·&nbsp; `Forky (14 — Next-Gen)` : **`2.4.69-1`**
> - **Références Officielles :** [Paquet Debian Trixie (`apache2`)](https://packages.debian.org/trixie/apache2) &nbsp;·&nbsp; [Paquet Debian Forky (`apache2`)](https://packages.debian.org/forky/apache2) &nbsp;·&nbsp; [Documentation Officielle Debian](https://packages.debian.org/trixie/apache2)
> - **Note d'Ingénierie (Divergence 13 vs 14) :** Sous Debian 13 (Trixie), PHP passe en version 8.4 (`php8.4-fpm`). Sous Debian 14 (Forky), privilégiez le mode `proxy_fcgi` (`php-fpm`) avec HTTP/2 natif plutôt que le module monolithique `mod_php`.

<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Afficher les Encarts Ligne de Commande : Debian 13 (Trixie — Stable) vs Debian 14 (Forky — Next-Gen)</b></summary>

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Profil Production Stable — Commandes pour `Debian 13 (Trixie)`
```bash
sudo apt update && sudo apt install -y apache2 libapache2-mod-php8.4 php8.4-fpm
sudo a2enmod ssl rewrite headers http2 && sudo systemctl restart apache2
```

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-rd.svg" width="46" height="16" align="absmiddle" alt="[R&D]" /> Profil Anticipation Next-Gen — Commandes pour `Debian 14 (Forky)`
```bash
# Debian 14 (Forky) — Solveur APT 3.0 & metapaquets PHP independants de la sous-version :
sudo apt update && sudo apt install -y apache2 php-fpm libapache2-mod-fcgid
sudo a2enmod proxy_fcgi setenvif ssl http2 && sudo a2enconf php*-fpm && sudo systemctl reload apache2
```

</details>
<!-- DEBIAN-TRUTH-END -->

<!-- CIEL-PEDAGOGY-START -->
<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Synthèse d'Architecture, Standards Officiels &amp; Diagnostic (Niveau 1 : Fondamentaux · Niveau 2 : Repères · Niveau 3 : Diagnostic)</b></summary>

- **Niveau 1 — Fondamentaux &amp; Principe d'Architecture :** **Apache HTTP Server (`apache2`)** est le serveur Web modulaire de référence sous Debian : il assure la terminaison TLS 1.3, le routage multi-domaines par **VirtualHosts** (`ServerName`) et délègue l'exécution dynamique PHP au gestionnaire de processus `php-fpm`.
- **Niveau 2 — Repères Officiels (Ports IANA, Fichiers Debian &amp; Commandes de Validation) :** **Ports IANA :** `TCP 80` (HTTP) · `TCP 443` (HTTPS TLS 1.2/1.3) &nbsp;|&nbsp; **Arborescence Debian :** `/etc/apache2/sites-available/`, `/etc/apache2/conf-available/` &nbsp;|&nbsp; **Validation officielle :** `sudo apache2ctl configtest` (`Syntax OK`).
- **Niveau 3 — Diagnostic d'Incidents &amp; Ingénierie Avancée :** **Diagnostic & Architecture :** Tout nouveau site déclaré dans `sites-available/` doit être activé via `sudo a2ensite` avant rechargement (`sudo systemctl reload apache2`). En production, associez le moteur asynchrone **MPM `event`** au démon **`php-fpm`** (via `proxy_fcgi`) plutôt qu'à l'ancien module `mod_php` afin d'activer HTTP/2 et de réduire l'empreinte mémoire.
- **Sources de Vérité Officielles Éditeurs &amp; Standards :** [Documentation Officielle Apache HTTP Server 2.4](https://httpd.apache.org/docs/2.4/fr/) &nbsp;·&nbsp; [Wiki Officiel Debian Apache](https://wiki.debian.org/Apache)
- **Livres Blancs &amp; 67 Podcasts Audio R&amp;D :** [Portail 0xCyberLiTech](https://0xcyberlitech.com/) &nbsp;·&nbsp; [Livre Blanc SOC Cockpit v5.5](https://0xcyberlitech.com/soc-rd.html) &nbsp;·&nbsp; [Livre Blanc JARVIS Mark-VII](https://0xcyberlitech.com/jarvis-rd.html) &nbsp;·&nbsp; [Blueprint Logiciel &amp; Matériel RTX 5080](https://0xcyberlitech.com/blueprint-jarvis.html)

</details>
<!-- CIEL-PEDAGOGY-END -->


## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 01 // Protéger l’accès d’un répertoire ou d’une page avec (.htaccess) et (.htpasswd).
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Il est parfois nécessaire de protéger l’accès à une page ou à un répertoire sur un serveur web (par exemple, un répertoire d’administration contenant des données sensibles), afin d’éviter que n’importe qui puisse y accéder.

Différentes méthodes existent, notamment en utilisant des langages comme PHP, ASP, Perl, etc.  
Cependant, la méthode la plus simple consiste à utiliser le mécanisme de protection du serveur Apache.

Ici, on part du principe que vous **n’avez pas accès au fichier de configuration `httpd.conf`** (cas fréquent chez un hébergeur mutualisé).

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 02 // Principe
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Le fichier `.htaccess` est un fichier texte contenant des directives Apache, placé dans le répertoire à protéger.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 03 // Exemple : protéger le répertoire `/var/www/html`
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

On commence par créer le fichier `.htaccess` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> touch /var/www/html/.htaccess
> ```
<!-- CODE-WINDOW-END -->

Puis, on y dépose le contenu suivant :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```apache
> AuthType Basic
> AuthName "Zone protégée par mot de passe."
> AuthUserFile /var/www/.htpasswd
> Require valid-user
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 04 // Explications des directives
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- **AuthUserFile** : chemin absolu vers le fichier contenant les couples utilisateurs / mots de passe.  
  Exemple ici : `/var/www/.htpasswd`.

  > Il est conseillé de choisir un nom différent de `.htpasswd` pour plus de sécurité.  
  > Ce fichier doit idéalement être **hors de la racine web** pour éviter toute exposition.

- **AuthGroupFile** : permet de définir un fichier contenant des groupes d’utilisateurs (peu utilisé, souvent pointé vers `/dev/null`).

- **AuthName** : message qui s’affiche dans la fenêtre d’authentification.

- **AuthType** : type d’authentification. Le plus courant est `Basic`, qui transmet les mots de passe en clair (non chiffrés) — attention à ne pas l’utiliser sur un site non sécurisé en HTTPS.

- **Require valid-user** : accepte tous les utilisateurs définis dans le fichier `.htpasswd`.  
  On peut restreindre à des utilisateurs précis avec :  

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```apache
>   Require user herve jacques
> ```
<!-- CODE-WINDOW-END -->

  (séparer les noms d’utilisateur par des espaces).

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 05 // Exemple complet avec `.htaccess` placé dans le répertoire à protéger
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```apache
> AuthType Basic
> AuthName "Zone protégée par mot de passe."
> AuthUserFile /var/www/.htpasswd
> Require valid-user
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 06 // Création du fichier `.htpasswd`
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Sous Linux/Unix, on utilise l’utilitaire `htpasswd` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> htpasswd -Bc /var/www/.htpasswd utilisateur
> ```
<!-- CODE-WINDOW-END -->

Exemple :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> htpasswd -Bc /var/www/.htpasswd srv-linux-01
> ```
<!-- CODE-WINDOW-END -->

- `-B` : utilise bcrypt (plus sécurisé) pour le chiffrement du mot de passe  
- `-c` : crée un nouveau fichier `.htpasswd` (attention : écrase l’ancien fichier)

Le système vous demandera le mot de passe deux fois.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 07 // Contenu du fichier `.htpasswd`
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Pour voir le contenu (crypté) :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> cat /var/www/.htpasswd
> ```
<!-- CODE-WINDOW-END -->

Exemple de ligne :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> srv-linux-01:$2y$10$<HASH-BCRYPT>
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 08 // Ajouter ou modifier un utilisateur
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Pour ajouter un utilisateur sans écraser le fichier existant, ne pas utiliser `-c` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> htpasswd -B /var/www/.htpasswd nouvel_utilisateur
> ```
<!-- CODE-WINDOW-END -->

<!-- MASTER-FOOTER-START -->
<div align="center">
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/divider-hud.svg" alt="" width="100%" />

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/footer-master.svg" alt="0xCyberLiTech — Architecture Cyberdéfense, Ingénierie Déterministe & IA Souveraine" width="100%" />
</a>

<p align="center"><a href="https://0xcyberlitech.com/"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/badge-antigravity.svg" alt="Architecturé par Marc & Antigravity (Google DeepMind)" width="520" /></a></p>

<sub><b>Architecturé &amp; Forgé par Marc &amp; Antigravity (Google DeepMind)</b> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/"><b>0xcyberlitech.com</b></a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/soc-rd.html">Architecture SOC Cockpit v5.5</a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/jarvis-rd.html">Architecture JARVIS Mark-VII</a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/blueprint-jarvis.html">Blueprint Matériel RTX 5080</a></sub>

</div>
<!-- MASTER-FOOTER-END -->
