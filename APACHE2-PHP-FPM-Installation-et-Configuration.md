<!-- MASTER-HEADER-START -->
<div align="center">

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/headers/header-apache2.svg" alt="0xCyberLiTech // Apache2" width="100%" />
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


# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="20" height="20" align="absmiddle" alt="" /> Comprendre, Installer et Sécuriser PHP & PHP-FPM avec Apache2 (Debian 13 & 14)

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 01 // QU'EST-CE QUE PHP ET POURQUOI UTILISER PHP-FPM ?
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

**PHP** (*Hypertext Preprocessor*) est le langage de script côté serveur le plus répandu pour générer dynamiquement des pages Web et interagir avec les bases de données **MariaDB / PostgreSQL**.

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> A. L'évolution majeure sous Debian 13 (Trixie) et Debian 14 (Forky) : `mod_php` vs `PHP-FPM`

Historiquement, Apache2 exécutait PHP via le module embarqué `libapache2-mod-php`, ce qui forçait Apache à fonctionner en mode multiprocessus lourd (`mpm_prefork`) et chargeait l'interpréteur PHP dans chaque processus, même pour servir une simple image statique.

Sous **Debian 13 (Trixie — PHP 8.4)** et **Debian 14 (Forky)**, l'état de l'art repose sur **PHP-FPM** (*FastCGI Process Manager*) :
- **Séparation stricte des rôles :** Apache2 (`mpm_event`) gère uniquement les connexions réseau HTTPS/HTTP2 à très haute vitesse et transmet les scripts `.php` au démon `php-fpm` via une socket Unix locale (`/run/php/php8.4-fpm.sock`).
- **Isolation de sécurité :** Chaque site peut tourner sous son propre pool PHP-FPM avec un utilisateur Linux distinct.
- **Performances accrues :** Cache d'opcodes **OPcache** partagé et consommation mémoire divisée par 3.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 02 // INSTALLATION DE PHP-FPM & EXTENSIONS COURANTES
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Installez le démon `php-fpm` ainsi que les extensions indispensables aux applications modernes :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt update
> sudo apt install -y php-fpm php-cli php-common php-mysql php-pgsql php-curl php-gd php-intl php-mbstring php-soap php-xml php-zip php-opcache libapache2-mod-fcgid
> ```
<!-- CODE-WINDOW-END -->

Vérifiez la version installée et l'état du service `php-fpm` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> php -v
> sudo systemctl status php*-fpm --no-pager
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 03 // COUPLAGE D'APACHE2 AVEC PHP-FPM (`proxy_fcgi`)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Activez les modules `proxy_fcgi` et `setenvif` ainsi que la configuration FPM dans Apache2 :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo a2enmod mpm_event proxy_fcgi setenvif
> sudo a2enconf php*-fpm
> sudo apache2ctl configtest
> sudo systemctl restart apache2
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 04 // DURCISSEMENT DU FICHIER `php.ini` EN PRODUCTION
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Le fichier de configuration principal de PHP-FPM se situe dans `/etc/php/8.4/fpm/php.ini` (sous Debian 13 Trixie) ou `/etc/php/*/fpm/php.ini`. Appliquez systématiquement ces directives de sécurité pour masquer la bannière PHP et bloquer les fonctions système dangereuses :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```ini
> ; Masquer la version de PHP dans les en-têtes HTTP (X-Powered-By)
> expose_php = Off
>
> ; Désactiver l'affichage des erreurs techniques aux visiteurs (journaliser en interne)
> display_errors = Off
> log_errors = On
>
> ; Empêcher l'inclusion de fichiers distants via URL (protection RFI)
> allow_url_include = Off
> allow_url_fopen = On
>
> ; Durcissement des cookies de session PHP
> session.cookie_httponly = 1
> session.cookie_secure = 1
> session.use_strict_mode = 1
> session.cookie_samesite = "Strict"
>
> ; Limites de ressources et d'envoi de fichiers
> memory_limit = 256M
> upload_max_filesize = 32M
> post_max_size = 32M
> max_execution_time = 60
> ```
<!-- CODE-WINDOW-END -->

Rechargez ensuite le démon PHP-FPM pour appliquer les paramètres sans coupure :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl reload php*-fpm
> sudo journalctl -u php*-fpm -n 25 --no-hostname
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
