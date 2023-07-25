![Apache_logo](./images/Apache_logo.png)

# - HTACCESS, cinq exemples.

| Cat | Etapes |
|------|------|
| - 1. | [Rediriger les pages en http vers celles en https.](#balise_02) |
| - 2. | [Enlever le www.](#balise_02) |
| - 3. | [Rediriger une page spécifique d’un serveur sur une page spécifique d’un autre serveur.](#balise_03) |
| - 4. | [Rediriger toutes les URL d’un site lors d’un changement de nom de domaine.](#balise_04) |
| - 5. | [Rediriger toutes les URLs d’un site vers une seule et unique URL.](#balise_05) |

Dans tous nos exemples, nous allons utiliser le fichier .htaccess, qui permet de modifier la configuration de notre serveur. Pour y accéder, nous allons donc devoir nous connecter à notre projet web en FTP. Si vous utilisez WordPress, le fichier est créé automatiquement dans le répertoire racine de votre site. Sinon, à vous de l’ajouter manuellement..

<a name="balise_01"></a>
# - 1. Rediriger les pages en http vers celles en https.

Forcer les utilisateurs à utiliser la version https de votre site est important pour leur offrir une sécurité convenable.

Pour ce faire, il vous suffit d’insérer ci-dessous dans votre fichier .htaccess, en remplaçant « exemple.com » par votre nom de domaine :

Exemple : rediriger http://exemple.com vers httsp://exemple.com.
```
RewriteEngine on
RewriteCond %{HTTP:X-Forwarded-Proto} !https
RewriteRule (.*) https://exemple.com/$1 [R=301,L]
```
Si vous rencontrez une erreur de boucle, cela indique que le HTTP/2 est actif sur votre site.

Il vous suffit alors de remplacer la deuxième ligne par :
```
RewriteCond %{HTTPS} off
```
```
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}
```
<a name="balise_02"></a>
# - 2. Enlever le www.

La mode du www est clairement derrière nous. Cependant, il arrive encore que des personnes le tape dans la barre d’URL. 

Afin de ne pas les abandonner, redirigeons-les, et quel que soit la page désirée, en enlevant le www.

Exemple : rediriger www.exemple.com/test/03 vers exemple.com/test/03
```
RewriteEngine on
RewriteCond %{HTTP_HOST} ^www\.(.*)$ [NC]
RewriteRule ^(.*)$ http://%1%{REQUEST_URI} [R=301,QSA,NC,L]
```
<a name="balise_03"></a>
# - 3. Rediriger une page spécifique d’un serveur sur une page spécifique d’un autre serveur.

Depuis le panneau de configuration de votre hébergeur, évitez de créer une redirection 301.

Créez-y plutôt un alias lié au serveur dont IP est celle où se trouve notre fichier .htaccess.

Après que l’alias soit créé, attendez 10-15 minutes, puis contrôlez que la propagation d’DNS de cet alias est terminée. Pour ce faire, vous pouvez utiliser cet outil : https://www.whatsmydns.net/

Quand cela est fait, toujours dans votre panneau de gestion de votre hébergeur, mettez à jour le certificat SSL de votre site.

Si vous utilisez une solution WordPress, au moment où vous configurez un alias via le panneau de gestion de votre hébergeur, WordPress ajoutera automatiquement la redirection 301. Pratique non ?

Passons au code. Celui-ci doit être ajouté dans le fichier .htaccess de votre site de destination.

Exemple : rediriger exemple.com/non-final vers karac.ch/final

```
RewriteEngine On
RewriteCond %{HTTP_HOST} ^(www\.)? exemple.com
RewriteRule ^ non-final/? https://karac.ch/final/ [R=301,L]
```
<a name="balise_04"></a>
# - 4. Rediriger toutes les URL d’un site lors d’un changement de nom de domaine.

Vous devez changer le nom de domaine d’un de vos sites, et vous vous rendez compte que vous avez plus de 1000 URLs différentes ? 

Ne paniquez pas ! Il existe une méthode permettant de résoudre ce problème en 3 lignes. Et ça se passe toujours dans notre cher fichier .htaccess.

Exemple : rediriger exemple.com/post1 vers karac.ch/post1 mais également exemple.com/news1 vers karac.ch/news1, etc…
```
RewriteEngine On
RewriteCond %{HTTP_HOST} ^exemple.com$ [OR]
RewriteCond %{HTTP_HOST} ^www.exemple.com$
RewriteRule (.*)$ https://karac.ch/$1 [R=301,L]
```
<a name="balise_05"></a>
# - 5. Rediriger toutes les URLs d’un site vers une seule et unique URL.

Pour cela, il va falloir modifier le fichier .htaccess du site qui sera redirigé.

Exemple : rediriger exemple.com/post1 vers karac.ch mais également exemple.com/new1 vers karac.ch, etc…
```
Redirect 301 "/" "https://karac.ch"
```
