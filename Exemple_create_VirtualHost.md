<a name="Exemple_create_VirtualHost.md"></a>
![Apache_logo](./images/Apache_logo.png)

# Exemples concernant la mise en place de deux VirtualHosts (HTTP & HTTPS) sur DEBIAN 11 & 12.
```
nano /etc/apache2/sites-available/000-default.conf
```
```
# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 29-06-2023
# Date de modification : le 29-06-2023
# 000-default.conf - Exemple concernant le VirtualHost 000-default.conf
# /etc/apache2/sites-available/
# --------------------------------------------------------------------------
<VirtualHost *:80>

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        <Directory /var/www/>
                Options -Indexes +FollowSymLinks
                Options +ExecCGI
                AllowOverride All
                # Apache 2.4
                Require all granted
                # Apache 2.2
                # Order allow,deny
                # Allow from all
        </Directory>

        RewriteEngine On
        RewriteCond %{HTTPS} off
        RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}

</VirtualHost>
```
```
nano /etc/apache2/sites-available/default-ssl.conf
```
```
# --------------------------------------------------------------------------
# 0xCyberLiTech
# Date de création : le 29-06-2023
# Date de modification : le 29-06-2023
# default_ssl.conf - Exemple concernant le VirtualHost default-ssl.conf
# /etc/apache2/sites-available/
# --------------------------------------------------------------------------
<VirtualHost *:443>

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        <Directory /var/www/>
                Options -Indexes +FollowSymLinks
                Options +ExecCGI
                AllowOverride All
                # Apache 2.4
                Require all granted
                # Apache 2.2
                # Order allow,deny
                # Allow from all
        </Directory>

        # SSL Engine Switch:
        # Enable/Disable SSL for this virtual host.
        SSLEngine on

        # A self-signed (snakeoil) certificate can be created by installing
        # the ssl-cert package. See
        # /usr/share/doc/apache2/README.Debian.gz for more info.
        # If both key and certificate are stored in the same file, only the
        # SSLCertificateFile directive is needed.
        SSLCertificateFile      /etc/ssl/certs/certfile.crt
        SSLCertificateKeyFile   /etc/ssl/private/keyfile.key

        # SSL Engine Options:
        # Set various options for the SSL engine.
        # o FakeBasicAuth:
        #   Translate the client X.509 into a Basic Authorisation.  This means that
        #   the standard Auth/DBMAuth methods can be used for access control.  The
        #   user name is the `one line' version of the client's X.509 certificate.
        #   Note that no password is obtained from the user. Every entry in the user
        #   file needs this password: `xxj31ZMTZzkVA'.
        # o ExportCertData:
        #   This exports two additional environment variables: SSL_CLIENT_CERT and
        #   SSL_SERVER_CERT. These contain the PEM-encoded certificates of the
        #   server (always existing) and the client (only existing when client
        #   authentication is used). This can be used to import the certificates
        #   into CGI scripts.
        # o StdEnvVars:
        #   This exports the standard SSL/TLS related `SSL_*' environment variables.
        #   Per default this exportation is switched off for performance reasons,
        #   because the extraction step is an expensive operation and is usually
        #   useless for serving static content. So one usually enables the
        #   exportation for CGI and SSI requests only.
        # o OptRenegotiate:
        #   This enables optimized SSL connection renegotiation handling when SSL
        #   directives are used in per-directory context.
        #SSLOptions +FakeBasicAuth +ExportCertData +StrictRequire

        <FilesMatch "\.(?:cgi|shtml|phtml|php)$">
                SSLOptions +StdEnvVars
        </FilesMatch>
        <Directory /usr/lib/cgi-bin>
                SSLOptions +StdEnvVars
        </Directory>

</VirtualHost>
```
All steps on Debian require to run as root. To become root simply run :

All commands from this point onwards will be as root.

- Prerequisites.

Perform these steps to install the pre-requisite packages.
```
apt-get update
apt-get install -y openssl
```
All of the remaining steps will be performed from within the root user's home directory to ensure the files you create are not accessible to anyone except the root user. Change into the home directory with this command: 
```
cd ~
```
- Generate Private Key File.

The first step is to generate the private key file, execute the following command :
```
openssl genrsa -out keyfile.key 2048
```
That would have generated some random text.

- Generate Certificate Request File.

Next you will generate the certificate request file by executing the following command:
```
openssl req -new -key keyfile.key -out certrequest.csr
```
You will need to supply some values, some can be left blank, however the most important value is the Common Name. In the example below you can see that core-033.domain.local has been used which means that when you access the Nagios Core server in your web browser, this is the address you will need to use. This is particularly important, if these don't match then you will get warnings in your web browser. More detailed information about this can be found in the following KB article: https://support.nagios.com/kb/article.php?id=598

The following is an example:

You are about to be asked to enter information that will be incorporated into your certificate request.

What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank 
For some fields there will be a default value,
If you enter '.', the field will be left blank.

```
Country Name (2 letter code) [AU]:AU
State or Province Name (full name) [Some-State]:NSW
Locality Name (eg, city) []:Sydney
Organization Name (eg, company) [Internet Widgits Pty Ltd]:My Company Pty Ltd
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:core-033.domain.local
Email Address []:

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
```
As you can see above a password was not supplied, it is not necessary.

- Sign Certificate Request.

At this point you have created a certificate request that needs to be signed by a CA.

- Using A Trusted CA Company.

If you are going to use a trusted company like VeriSign to provide you with a certificate you will need to send them a copy of the certificate request. This can be viewed by executing the following command:
```
cat certrequest.csr
 
You'll get a lot of random text, this is what you will need to provide to your trusted CA. You must provide the CA with everything including the -----BEGIN CERTIFICATE REQUEST----- and -----END CERTIFICATE REQUEST----- lines.

Once they send you the signed certificate you will need to copy the certificate into a new file called certfile.crt. The certificate you receive will also be a lot of random text, so you can just paste that text into the new file which you can open with the vi editor:
```
```
nano certfile.crt
```
You must paste everything including the -----BEGIN CERTIFICATE----- and -----END CERTIFICATE----- lines when pasting them into the file.

Save the file and close nano.

You can now proceed to the Copy Files step.

- Using A Microsoft Windows CA

If you are going to use a Microsoft Windows CA to sign your certificate request please follow the steps in this KB article :

https://support.nagios.com/kb/article.php?id=597

After following the KB article you will have the certfile.crt file and you can proceed to the Copy Files step.

- Self Signing The Certificate.

You can also self-sign the certificate by executing the following command :
```
openssl x509 -req -days 365 -in certrequest.csr -signkey keyfile.key -out certfile.crt
```
Which should produce output saying the Signature was OK and it was Getting Private Key.

Note: When you self sign a certificate you will get warnings in your web browser. More detailed information about this can be found in the following KB article: https://support.nagios.com/kb/article.php?id=598

- Copy Files

You need to copy the certificate files to the correct location and set permissions, execute the following commands:
```
cp certfile.crt /etc/ssl/certs/
cp keyfile.key /etc/ssl/private/
chmod go-rwx /etc/ssl/certs/certfile.crt
chmod go-rwx /etc/ssl/private/keyfile.key
```
- Update Apache Configuration.

Enable the mod_ssl module in Apache by executing the following command :
```
a2enmod ssl
a2enmod rewrite
```
Now you have to tell the Apache web server where to look for it. Open the following file in vi by executing the following command :
```
nano /etc/apache2/sites-available/default-ssl.conf
```
Find these lines and update them as follows :
```
SSLCertificateFile    /etc/ssl/certs/certfile.crt
SSLCertificateKeyFile /etc/ssl/private/keyfile.key
```
Tip: typing /eFile and pressing Enter in vi should take you directly to this section in the file.

Save the changes, you have finished editing this file. 

Open the following file in vi by executing the following command:
```
nano /etc/apache2/sites-available/000-default.conf
```
Navigate to the end of the file (press SHIFT + G), and before </VirtualHost> add the following::
```
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}
```
Save the changes, you have finished editing this file.

Now you have to enable this configuration in Apache by executing the following command:
```
a2ensite default-ssl.conf
```
- Reload Apache Web Server.

You need to reload Apache for the new certificate key to be used.
```
systemctl reload apache2.service
```
- Firewall Rules.

You need to allow port 443 inbound traffic on the local firewall so you can reach the Nagios Core web interface.
```
iptables -I INPUT -p tcp --destination-port 443 -j ACCEPT
apt-get install -y iptables-persistent
If prompted, answer yes to saving existing rules
```
- Test Certificate.

Now test your connection to the server by directing your web browser to https://yourservername/.

Note: There is no nagios/ extension in the URL, you are just testing a connection to Apache to see if the certificate works.

You may get a self signed certificate warning, but that is OK, you can just add a security exception. If is working you'll see the Apache test web page. You will now be able to access your Nagios Core server by directing your web browser to https://yourservername/nagios/. More detailed information about this can be found in the following KB article: https://support.nagios.com/kb/article.php?id=598

If it returns an error check your firewall and backtrack through this document, making sure you've performed all the steps listed.

- Notes On Redirecting.

With this configuration, if a user types http://yourservername in their web browser, it will redirect them to https://yourservername which can cause certificate warnings. If you wanted to redirect them to https://yourservername.yourdomain.com then you simply need to change the RewriteRule.
```
RewriteRule (.*) https://yourservername.yourdomain.com%{REQUEST_URI}
```
Then reload the apache2 service.

More detailed information about this can be found in the following KB article: https://support.nagios.com/kb/article.php?id=598 
