![Apache_logo](./images/Apache_logo.png)

# Fondamentaux sur la configuration des serveurs virtuels (Apache) :

| Cat | Etapes |
|------|------|
| - A. | [Configurations sur les serveurs virtuels.](Configurations_serveurs_virtuels.md) |
| - A. | [Acces en HTTP & HTTPS.](Acces_HTTP_HTTPS.md) |
| - B. | [Forcer HTTP vers HTTPS.](Forcer_HTTP_vers_HTTPS.md) |
| - C. | [Exemple create VirtualHost.](Exemple_create_VirtualHost.md) |



Le but de ce document est d'essayer de répondre aux questions les plus répandues sur la configuration des serveurs virtuels. Les scénarios présentés ici se rencontrent quand plusieurs serveurs Webs doivent tourner sur une seule et même machine au moyen de serveurs virtuels par nom ou par IP.

## Fonctionnement de plusieurs serveurs virtuels par nom sur une seule adresse IP.

Votre serveur ne dispose que d'une seule adresse IP, et de nombreux alias (CNAMES) pointent vers cette adresse dans le DNS. Pour l'exemple, www.example.com et www.example.org doivent tourner sur cette machine.
Note :

La configuration de serveurs virtuels sous Apache ne provoque pas leur apparition magique dans la configuration du DNS. Il faut que leurs noms soient définis dans le DNS, et qu'ils y soient résolus sur l'adresse IP du serveur, faute de quoi personne ne pourra visiter votre site Web. Il est possible d'ajouter des entrées dans le fichier hosts pour tests locaux, mais qui ne fonctionneront que sur la machine possédant ces entrées :

Configuration du serveur.

Note complémentaire concernant l'instruction <-- NameVirtualHost -->

Pour que cette méthode de reconnaissance du site via l’adresse URL (domaine ou sous-domaine) entrée fonctionne, il faut faire très attention que l’instruction NameVirtualHost qui se trouve parfois dans ports.conf, httpd.conf ou apache2.conf ai bien pour valeur, la même valeur que vous avez entrer dans <VirtualHost>, soit *:80 dans l’exemple précédent. Vous devez donc avoir :
```
NameVirtualHost *:80
```
Exemple ficfier de .portsconf.
```
# If you just change the port or add more ports here, you will likely also
# have to change the VirtualHost statement in
# /etc/apache2/sites-enabled/000-default
# This is also true if you have upgraded from before 2.2.9-3 (i.e. from
# Debian etch). See /usr/share/doc/apache2.2-common/NEWS.Debian.gz and
# README.Debian.gz

NameVirtualHost *:80
Listen 80

<IfModule mod_ssl.c>
    # If you add NameVirtualHost *:443 here, you will also have to change
    # the VirtualHost statement in /etc/apache2/sites-available/default-ssl
    # to <VirtualHost *:443>
    # Server Name Indication for SSL named virtual hosts is currently not
    # supported by MSIE on Windows XP.
    Listen 443
</IfModule>

<IfModule mod_gnutls.c>
    Listen 443
</IfModule>
```
On n'y retrouve l'instruction "NameVirtualHost *:80".
```
# Apache doit écouter sur le port 80
Listen 80

# Toutes les adresses IP doivent répondre aux requêtes sur les
# serveurs virtuels

NameVirtualHost *:80

<VirtualHost *:80>
	DocumentRoot /www/example.com
	ServerName www.example1.com

	# Autres directives ici

</VirtualHost>
```
```
<VirtualHost *:80>
	DocumentRoot /www/example.org
	ServerName www.example2.org

	# Autres directives ici

</VirtualHost> 
```
Les astérisques correspondent à toutes les adresses, si bien que le serveur principal ne répondra jamais à aucune requête. 
Comme www.example.com se trouve en premier dans le fichier de configuration, il a la plus grande priorité et peut être vu comme serveur par défaut ou primaire ; ce qui signifie que toute requête reçue ne correspondant à aucune des directives ServerName sera servie par ce premier VirtualHost.

Note :

Si vous le souhaitez, vous pouvez remplacer * par l'adresse IP du système. 
Dans ce cas, l'argument de VirtualHost doit correspondre à l'argument de NameVirtualHost :
```
NameVirtualHost 172.20.30.40

<VirtualHost 172.20.30.40>
# etc ... 
```
En général, il est commode d'utiliser * sur les systèmes dont l'adresse IP n'est pas constante - par exemple, pour des serveurs dont l'adresse IP est attribuée dynamiquement par le FAI, et où le DNS est géré au moyen d'un DNS dynamique quelconque. Comme * signifie n'importe quelle adresse, cette configuration fonctionne sans devoir être modifiée quand l'adresse IP du système est modifiée.

La configuration ci-dessus est en pratique utilisée dans la plupart des cas pour les serveurs virtuels par nom. En fait, le seul cas où cette configuration ne fonctionne pas est lorsque différents contenus doivent être servis en fonction de l'adresse IP et du port contactés par le client.

## Serveurs virtuels par nom sur plus d'une seule adresse IP.

Note :

Toutes les techniques présentées ici peuvent être étendues à un plus grand nombre d'adresses IP.

Le serveur a deux adresses IP. Sur l'une (172.20.30.40), le serveur "principal" server.domain.com doit répondre, et sur l'autre (172.20.30.50), deux serveurs virtuels (ou plus) répondront.

Configuration du serveur.

```
Listen 80

# Serveur "principal" sur 172.20.30.40
ServerName server.domain.com
DocumentRoot /www/mainserver

# l'autre adresse
NameVirtualHost 172.20.30.50

<VirtualHost 172.20.30.50>
	DocumentRoot /www/example.com
	ServerName www.example.com

	# D'autres directives ici ...

</VirtualHost>

<VirtualHost 172.20.30.50>
	DocumentRoot /www/example.org
	ServerName www.example.org

	# D'autres directives ici ...

</VirtualHost>
```
Toute requête arrivant sur une autre adresse que 172.20.30.50 sera servie par le serveur principal. Les requêtes vers 172.20.30.50 avec un nom de serveur inconnu, ou sans en-tête Host:, seront servies par www.example.com.

## Servir le même contenu sur des adresses IP différentes (telle qu'une adresse interne et une externe).

La machine serveur dispose de deux adresses IP (192.168.1.1 et 172.20.30.40). Cette machine est placée à la fois sur le réseau interne (l'Intranet) et le réseau externe (Internet). Sur Internet, le nom server.example.com pointe vers l'adresse externe (172.20.30.40), mais sur le réseau interne, ce même nom pointe vers l'adresse interne (192.168.1.1).

Le serveur peut être configuré pour répondre de la même manière aux requêtes internes et externes, au moyen d'une seule section VirtualHost.

Configuration du serveur.
```
NameVirtualHost 192.168.1.1
NameVirtualHost 172.20.30.40

<VirtualHost 192.168.1.1 172.20.30.40>
	DocumentRoot /www/server1
	ServerName server.example.com
	ServerAlias server
</VirtualHost>
```
Ainsi, les requêtes en provenance de chacun des deux réseaux seront servies par le même VirtualHost.
Note :

Sur le réseau interne, il est possible d'utiliser le nom raccourci server au lieu du nom complet server.example.com.

Notez également que dans l'exemple précédent, vous pouvez remplacer la liste des adresses IP par des * afin que le serveur réponde de la même manière sur toutes ses adresses.

## Servir différents sites sur différents ports.

Vous disposez de plusieurs domaines pointant sur la même adresse IP et vous voulez également servir de multiples ports. Vous y parviendrez en définissant les ports dans la directive "NameVirtualHost". Si vous tentez d'utiliser <VirtualHost name:port> sans directive NameVirtualHost name:port, ou tentez d'utiliser la directive Listen, votre configuration ne fonctionnera pas.

Configuration du serveur.
```
Listen 80
Listen 8080

NameVirtualHost 172.20.30.40:80
NameVirtualHost 172.20.30.40:8080

<VirtualHost 172.20.30.40:80>
	ServerName www.example.com
	DocumentRoot /www/domain-80
</VirtualHost>

<VirtualHost 172.20.30.40:8080>
	ServerName www.example.com
	DocumentRoot /www/domain-8080
</VirtualHost>

<VirtualHost 172.20.30.40:80>
	ServerName www.example.org
	DocumentRoot /www/otherdomain-80
</VirtualHost>

<VirtualHost 172.20.30.40:8080>
	ServerName www.example.org
	DocumentRoot /www/otherdomain-8080
</VirtualHost> 
```
## Hébergement virtuel basé sur IP.

Le serveur dispose de deux adresses IP (172.20.30.40 et 172.20.30.50) correspondant respectivement aux noms www.example.com et www.example.org.

Configuration du serveur
```
Listen 80

<VirtualHost 172.20.30.40>
	DocumentRoot /www/example.com
	ServerName www.example1.com
</VirtualHost>

<VirtualHost 172.20.30.50>
	DocumentRoot /www/example.org
	ServerName www.example2.org
</VirtualHost>
```
Les requêtes provenant d'adresses non spécifiées dans l'une des directives <VirtualHost> (comme pour localhost par exemple) seront dirigées vers le serveur principal, s'il en existe un.

## Hébergements virtuels mixtes basés sur les ports et sur les IP.

Le serveur dispose de deux adresses IP (172.20.30.40 et 172.20.30.50) correspondant respectivement aux noms www.example.com et www.example.org. Pour chacun d'eux, nous voulons un hébergement sur les ports 80 et 8080.

Configuration du serveur.
```
Listen 172.20.30.40:80
Listen 172.20.30.40:8080
Listen 172.20.30.50:80
Listen 172.20.30.50:8080

<VirtualHost 172.20.30.40:80>
	DocumentRoot /www/example.com-80
	ServerName www.example.com
</VirtualHost>

<VirtualHost 172.20.30.40:8080>
	DocumentRoot /www/example.com-8080
	ServerName www.example.com
</VirtualHost>

<VirtualHost 172.20.30.50:80>
	DocumentRoot /www/example.org-80
	ServerName www.example.org
</VirtualHost>

<VirtualHost 172.20.30.50:8080>
	DocumentRoot /www/example.org-8080
	ServerName www.example.org
</VirtualHost>
```
## Hébergements virtuels mixtes basé sur les noms et sur IP.

Pour certaines adresses, des serveurs virtuels seront définis par nom, et pour d'autres, ils seront définis par IP.

Configuration du serveur.
```
Listen 80

NameVirtualHost 172.20.30.40

<VirtualHost 172.20.30.40>
	DocumentRoot /www/example.com
	ServerName www.example.com
</VirtualHost>

<VirtualHost 172.20.30.40>
	DocumentRoot /www/example.org
	ServerName www.example.org
</VirtualHost>

<VirtualHost 172.20.30.40>
	DocumentRoot /www/example.net
	ServerName www.example.net
</VirtualHost>

# "par-IP"
<VirtualHost 172.20.30.50>
	DocumentRoot /www/example.edu
	ServerName www.example.edu
</VirtualHost>

<VirtualHost 172.20.30.60>
	DocumentRoot /www/example.gov
	ServerName www.example.gov
</VirtualHost>
```
## Utilisation simultanée de Virtual_host et de mod_proxy.

L'exemple suivant montre comment une machine peut mandater un serveur virtuel fonctionnant sur le serveur d'une autre machine. Dans cet exemple, un serveur virtuel de même nom est configuré sur une machine à l'adresse 192.168.111.2. La directive ProxyPreserveHost On est employée pour permette au nom de domaine d'être préservé lors du transfert, au cas où plusieurs noms de domaines cohabitent sur une même machine.
```
<VirtualHost *:*>
ProxyPreserveHost On
ProxyPass / http://192.168.111.2
ProxyPassReverse / http://192.168.111.2/
ServerName hostname.example.com
</VirtualHost>
```
## Utilisation de serveurs virtuels _default_

Serveurs virtuels _default_ pour tous les ports.

Exemple de capture de toutes les requêtes émanant d'adresses IP ou de ports non connus, c'est-à-dire, d'un couple adresse/port non traité par aucun autre serveur virtuel.

Configuration du serveur.
```
<VirtualHost _default_:*>
DocumentRoot /www/default
</VirtualHost> 
```
L'utilisation d'un tel serveur virtuel avec un joker pour le port empêche de manière efficace qu'une requête n'atteigne le serveur principal.

Un serveur virtuel par défaut ne servira jamais une requête qui est envoyée vers un couple adresse/port utilisée par un serveur virtuel par nom. Si la requête contient un en-tête Host: inconnu, ou si celui-ci est absent, elle sera toujours servie par le serveur virtuel primaire par nom (celui correspondant à ce couple adresse/port trouvé en premier dans le fichier de configuration).

Vous pouvez utiliser une directive AliasMatch ou RewriteRule afin de réécrire une requête pour une unique page d'information (ou pour un script).
Serveurs virtuels _default_ pour des ports différents

La configuration est similaire à l'exemple précédent, mais le serveur écoute sur plusieurs ports et un second serveur virtuel _default_ pour le port 80 est ajouté.

Configuration du serveur.
```
<VirtualHost _default_:80>
	DocumentRoot /www/default80
	# ...
</VirtualHost>

<VirtualHost _default_:*>
	DocumentRoot /www/default
	# ...
</VirtualHost> 
```
Le serveur virtuel par défaut défini pour le port 80 (il doit impérativement être placé avant un autre serveur virtuel par défaut traitant tous les ports grâce au joker *) capture toutes les requêtes envoyées sur une adresse IP non spécifiée. Le serveur principal n'est jamais utilisé pour servir une requête.
Serveurs virtuels _default_ pour un seul port

Nous voulons créer un serveur virtuel par défaut seulement pour le port 80.

Configuration du serveur.
```
<VirtualHost _default_:80>
	DocumentRoot /www/default
	...
</VirtualHost>
```
Une requête vers une adresse non spécifiée sur le port 80 sera servie par le serveur virtuel par défaut, et toute autre requête vers une adresse et un port non spécifiés sera servie par le serveur principal.

## Migration d'un serveur virtuel par nom en un serveur virtuel par IP.

Le serveur virtuel par nom avec le nom de domaine www.example.org (de notre exemple par nom) devrait obtenir sa propre adresse IP. Pendant la phase de migration, il est possible d'éviter les problèmes avec les noms de serveurs et autres serveurs mandataires qui mémorisent les vielles adresses IP pour les serveurs virtuels par nom.

La solution est simple, car il suffit d'ajouter la nouvelle adresse IP (172.20.30.50) dans la directive VirtualHost.

Configuration du serveur.
```
Listen 80
ServerName www.example.com
DocumentRoot /www/example.com

NameVirtualHost 172.20.30.40

<VirtualHost 172.20.30.40 172.20.30.50>
	DocumentRoot /www/example.org
	ServerName www.example.org
	# ...
</VirtualHost>

<VirtualHost 172.20.30.40>
	DocumentRoot /www/example.net	
	ServerName www.example.net
	ServerAlias *.example.net
	# ...
</VirtualHost>
```
Le serveur virtuel peut maintenant être joint par la nouvelle adresse (comme un serveur virtuel par IP) et par l'ancienne adresse (comme un serveur virtuel par nom).

Utilisation de la directive ServerPath.

Dans le cas où vous disposez de deux serveurs virtuels par nom, le client doit transmettre un en-tête Host: correct pour déterminer le serveur concerné. Les vieux clients HTTP/1.0 n'envoient pas un tel en-tête et Apache n'a aucun indice pour connaître le serveur virtuel devant être joint (il sert la requête à partir d'un serveur virtuel primaire). Dans un soucis de préserver la compatibilité descendante, il suffit de créer un serveur virtuel primaire chargé de retourner une page contenant des liens dont les URLs auront un préfixe identifiant les serveurs virtuels par nom.

Configuration du serveur.
```
NameVirtualHost 172.20.30.40

<VirtualHost 172.20.30.40>
	# Serveur virtuel primaire
	DocumentRoot /www/subdomain
	RewriteEngine On
	RewriteRule ^/.* /www/subdomain/index.html
	# ...
</VirtualHost>

<VirtualHost 172.20.30.40>
	DocumentRoot /www/subdomain/sub1
	ServerName www.sub1.domain.tld
	ServerPath /sub1/
	RewriteEngine On
	RewriteRule ^(/sub1/.*) /www/subdomain$1
	# ...
</VirtualHost>

<VirtualHost 172.20.30.40>
	DocumentRoot /www/subdomain/sub2
	ServerName www.sub2.domain.tld
	ServerPath /sub2/
	RewriteEngine On
	RewriteRule ^(/sub2/.*) /www/subdomain$1
	# ...
</VirtualHost>
```
À cause de la directive ServerPath, une requête sur une URL http://www.sub1.domain.tld/sub1/ est toujours servie par le serveur sub1-vhost.
Une requête sur une URL http://www.sub1.domain.tld/ n'est servie par le serveur sub1-vhost que si le client envoie un en-tête Host: correct. Si aucun en-tête Host: n'est transmis, le serveur primaire sera utilisé.

Notez qu'il y a une singularité : une requête sur http://www.sub2.domain.tld/sub1/ est également servie par le serveur sub1-vhost si le client n'envoie pas d'en-tête Host:.

Les directives RewriteRule sont employées pour s'assurer que le client qui envoie un en-tête Host: correct puisse utiliser d'autres variantes d'URLs, c'est-à-dire avec ou sans préfixe d'URL.
