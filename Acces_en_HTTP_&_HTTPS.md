<a name="Acces_en_HTTP_&_HTTPS.md"></a>
![Apache_logo](./images/Apache_logo.png)

# - B. Acces en HTTP & HTTPS.

Exemple concernant le VirtualHost 000-default.conf
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
Exemple concernant le VirtualHost default-ssl.conf
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
L'accès en HTTP reste en HTTP.
L'accès HTTPS reste HTTPS.
