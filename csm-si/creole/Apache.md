<!-- TITLE: Apache -->
<!-- SUBTITLE: A quick summary of Creole -->

# Configuration Apache 2.4

## Commandes

### Vérification de la syntaxe

`apachectl -t`

### Vérification des modules actifs

`apachectl -t -D DUMP_MODULES`

### Configuration Apache

#### Chemin pour la conf

Apache : `/usr/local/apache2/conf/`

Creole : `/r3a/r3aadmaa/donnees/configuration/httpd/`

#### Fichier /usr/local/apache2/conf/httpd.conf

Mettre cette ligne en actif:

```conf
#LoadModule proxy_module modules/mod_proxy.so
```

Ajouter cette ligne à la fin:

```conf
# Ajout de la configuration apache specifique a r3a Creole
Include conf/r3a.conf
```

#### Fichier /usr/local/apache2/conf/r3a.conf

```conf
# Definit le chemin vers la configuration apache de r3a
Include /r3a/r3aadmaa/donnees/configuration/httpd/*.conf
```

#### Fichier /r3a/r3aadmaa/donnees/configuration/httpd/creoleAPI.conf

```conf
# NameVirtualHost *:80
# NameVirtualHost *:443

<VirtualHost *:80>
    # RewriteEngine On
    # RewriteCond %{HTTPS} off
    # reactivate later
    # RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}

    LogFormat "%h %l %u %t \"%r\" %>s %b" common
    CustomLog /r3a/r3aadmaa/traces/httpd/access_log common
    ErrorLog /r3a/r3aadmaa/traces/httpd/error_log

    # SetOutputFilter DEFLATE
    # SSLProxyEngine on
    ProxyPass / http://localhost:5000
    ProxyPassReverse / http://localhost:5000
    ProxyPreserveHost On

    Timeout 6000
</VirtualHost>

# <VirtualHost *:443>
#     SetOutputFilter DEFLATE

#     SSLEngine on
#     SSLCertificateFile /etc/httpd/conf/ssl.crt/creoleAPI.cer
#     SSLCertificateKeyFile /etc/httpd/conf/ssl.crt/creoleAPI.key
#     SSLCertificateChainFile /etc/httpd/conf/ssl.crt/creoleAPI.pem

#     LogFormat "%h %l %u %t \"%r\" %>s %b" common
#     CustomLog /r3a/r3aadmaa/traces/httpd/access_log common
#     ErrorLog /r3a/r3aadmaa/traces/httpd/error_log

#     SSLProxyEngine on
#     ProxyPass / http://localhost:5000
#     ProxyPassReverse / http://localhost:5000
#     ProxyPreserveHost On

#     Timeout 6000
# </VirtualHost>
```
