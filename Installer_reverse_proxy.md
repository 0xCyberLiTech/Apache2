<a name="Reverse_Proxy.md"></a>
![Apache_logo](./images/Apache_logo.png)

# - E. Installer un Reverse Proxy sur Debian 11 & 12 :

Depuis une machine Debian 11 ou Debian 12 qui ne va servir qu’a ça (recommandation mais pas obligé), nous allons saisir les instructions suivantes :

Mise à jour du système :
```
apt update && apt full-upgrade -y
```
Installation du paquet pour Apache2 :
```
apt-get install apache2
```
Afin de bénéficier du mode reverse sur Apache2, il faut activer les module : 

- proxy
- proxy_http.

Pour activer ces 2 modules saisissez la commande :
```
a2enmod proxy proxy_http
```
Pour que l’activation de ces modules soient pris en compte redémarrer le service apache2 :
```
systemctl restart apache2
```
Créer un fichier de configuration Apache :
```
nano /etc/apache2/conf-available/votre-conf.conf
```
Voici un fichier de configuration d’exemple :
```
<VirtualHost *:80>
    ServerName votre-domaine.fr
    ServerAdmin postmaster@domaine.fr
 
    ProxyPass / http://127.0.0.1/
    ProxyPassReverse / http://127.0.0.1/
    ProxyRequests Off
</VirtualHost>
```
    ServerName correspond à votre domaine
    ProxyPass et ProxyPassReverse correspondent au serveur de destination.
    ProxyRequests est en off pour des raison de sécurité.

Activer la configuration :
```
a2ensite votre-conf.conf
```
Puis redémarrer apache2 :
```
systemctl restart apache2
```
