Hola,


para poner https://

Con xampp 1.7.7: Apache 2.2.21 + PHP 5.3.8 + OpenSSL 1.0.0e (Lo pone en C:\xampp\readme_en.txt)


## EXISTENTE -> MEJOR SI SE COMENTA PARA QUE NO ENTRE POR http://

<VirtualHost *:80>
   DocumentRoot "C:/proyectos/html/eurotaller/app/webroot"
   ServerName eurotaller.xxx.desa
</VirtualHost>


## NUEVO

<VirtualHost *:443>
    DocumentRoot "C:/proyectos/html/eurotaller/app/webroot"
    ServerName eurotaller.xxx.desa

    SSLEngine on
    SSLCertificateFile "conf/ssl.crt/server.crt"
    SSLCertificateKeyFile "conf/ssl.key/server.key"
</VirtualHost>

Las líneas del final copiar de C:\xampp\apache\conf\extra\httpd-ssl.conf
(Revisar que se carga httpd-ssl.conf en C:\xampp\apache\conf\httpd.conf y el modulo LoadModule ssl_module modules/mod_ssl.so)

Si queréis afinar los certificados

https://mozilla.github.io/server-side-tls/ssl-config-generator/

Y con la versión puesta

https://mozilla.github.io/server-side-tls/ssl-config-generator/?server=apache-2.2.21&openssl=1.0.0e&hsts=yes&profile=intermediate

# intermediate configuration, tweak to your needs
SSLProtocol             all -SSLv2 -SSLv3
SSLCipherSuite          ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES256-SHA:ECDHE-ECDSA-DES-CBC3-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:DES-CBC3-SHA:!DSS
SSLHonorCipherOrder     on

Esta entrada se puede poner pero hay que tener cuidado, creo que dice al navegador que no se conecte al sitio por http (solo https) y que lo recuerde durante 6 meses (además requiere tener el modulo LoadModule headers_module modules/mod_headers.so en httpd.conf)

    # HSTS (mod_headers is required) (15768000 seconds = 6 months)
    Header always set Strict-Transport-Security "max-age=15768000"

Con XAMPP mas modernos es parecido (Los nuevos proyectos debiéramos ponerlos en php72 pero depende de donde se vaya a alojar luego no podemos)

http://php.net/supported-versions.php
