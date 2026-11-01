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


# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-crypto.svg" width="18" height="18" align="absmiddle" alt="" /> HTACCESS – 10 astuces que tout le monde devrait connaître.
### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Compatible Apache 2.4+ sur Debian 12 (Bookworm), Debian 13 (Trixie) & Debian 14 (Forky)

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> Sommaire
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

| Nº  | Astuce                                     | Lien vers la section                           |
|-----|--------------------------------------------|-----------------------------------------------|
| 01  | Les pages d’erreur personnalisables        | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#balise-01)       |
| 02  | Redirection                                | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#balise-02)       |
| 03  | Protection par mot de passe                | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#balise-03)       |
| 04  | Augmenter la mémoire PHP                   | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#balise-04)       |
| 05  | Changer le fuseau horaire                  | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#balise-05)       |
| 06  | Bloquer des adresses IP                    | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#balise-06)       |
| 07  | Rediriger HTTP vers HTTPS                  | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#balise-07)       |
| 08  | Afficher un répertoire                     | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#balise-08)       |
| 09  | Bloquer le Hotlinking                      | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#balise-09)       |
| 10  | Définir la police de caractères            | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Accéder" />](#balise-10)       |

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Qu’est-ce qu’un fichier `.htaccess` ?
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Un fichier `.htaccess` permet de configurer finement le comportement d’un serveur Apache, répertoire par répertoire. C’est un fichier texte caché (préfixé d’un point) interprété automatiquement par le serveur **sans redémarrage**. Il peut être utilisé pour sécuriser un répertoire, faire des redirections, afficher des erreurs personnalisées, etc.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> Création du fichier `.htaccess`
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- Utilisez n’importe quel éditeur texte : `nano`, `vim`, ou via FTP/SFTP.
- Le fichier doit s’appeler **exactement** `.htaccess`
- Il est **caché** (fichier commençant par un point)
- Placez-le dans le répertoire que vous souhaitez configurer (ex. `/var/www/html/`)

---

<a name="balise-01"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 04 // 01 – Les pages d’erreur personnalisables
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```apache
> # Page d’erreur 404 personnalisée
> ErrorDocument 404 /erreur/404.html
>
> # Variante avec URL externe
> ErrorDocument 404 http://www.monsite.com/erreur/404.html
> ```
<!-- CODE-WINDOW-END -->

---

<a name="balise-02"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 05 // 02 – Redirection
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```apache
> # Redirection complète vers un autre domaine
> Redirect / http://www.nouveau-domaine.fr/
>
> # Redirection d’une page spécifique
> Redirect /ancienne-page.html nouvelle-page.html
> ```
<!-- CODE-WINDOW-END -->

---

<a name="balise-03"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 06 // 03 – Protection par mot de passe
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> `.htaccess`

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```apache
> AuthType Basic
> AuthName "Accès réservé"
> AuthUserFile /chemin/vers/.htpasswd
> Require valid-user
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Exemple de `.htpasswd`

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> User1:duCmo1zxkKx6Y
> User2:mou3IYjSLpGWI
> User3:HGKS9XzDXXAXQ
> ```
<!-- CODE-WINDOW-END -->

> Utilisez `htpasswd` pour générer les entrées chiffrées.

---

<a name="balise-04"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 07 // 04 – Augmenter la mémoire PHP
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```apache
> # Limite mémoire PHP à 128 Mo
> php_value memory_limit 128M
> ```
<!-- CODE-WINDOW-END -->

---

<a name="balise-05"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 08 // 05 – Changer le fuseau horaire
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```apache
> # Fuseau horaire pour PHP
> SetEnv TZ Europe/Paris
> ```
<!-- CODE-WINDOW-END -->

---

<a name="balise-06"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 09 // 06 – Bloquer des adresses IP
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```apache
> Order deny,allow
> Deny from .aol.com
> Deny from 192.168
> Allow from 192.168.220.102
> ```
<!-- CODE-WINDOW-END -->

> Bloque tous sauf une adresse IP spécifique.

---

<a name="balise-07"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 10 // 07 – Rediriger HTTP vers HTTPS
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Variante 1

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```apache
> RewriteEngine On
> RewriteCond %{Server_Port} !=443
> RewriteRule ^(.*)$ https://votre-domaine.fr/$1 [R=301,L]
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Variante 2 (recommandée)

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```apache
> RewriteEngine On
> RewriteCond %{HTTPS} off
> RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}
> ```
<!-- CODE-WINDOW-END -->

---

<a name="balise-08"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 11 // 08 – Afficher un répertoire (index)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```apache
> # Autoriser l'affichage de l'arborescence
> Options +Indexes
> ```
<!-- CODE-WINDOW-END -->

---

<a name="balise-09"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 12 // 09 – Bloquer le Hotlinking
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```apache
> RewriteEngine on
> RewriteCond %{HTTP_REFERER} !^$
> RewriteCond %{HTTP_REFERER} !^https?://(www\.)?votre-domaine.fr/ [NC]
> RewriteRule \.(gif|jpg|png|bmp|mp3|mp4|avi)$ - [F]
> ```
<!-- CODE-WINDOW-END -->

> Empêche d’autres sites d’afficher vos images ou fichiers multimédia.

---

<a name="balise-10"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 13 // 10 – Définir la police de caractères
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```apache
> # Par défaut UTF-8
> AddDefaultCharset utf-8
>
> # UTF-8 uniquement pour certains fichiers
> AddDefaultCharset utf-8 .css .html .php
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Conclusion
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Ces 10 astuces `.htaccess` vous permettent d’améliorer la sécurité, la performance, la personnalisation et l’ergonomie de votre site Web, tout en restant facilement déployables sans redémarrage de serveur.  
Elles sont **simples, efficaces** et adaptées à tout hébergement Apache sous **Debian 12 (Bookworm), Debian 13 (Trixie) & Debian 14 (Forky) et 13**.

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
