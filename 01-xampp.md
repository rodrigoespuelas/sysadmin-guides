#### Conexion MySQL
~~~
cd \xampp\mysql\bin
mysql.exe -u root --password
~~~

#### Creación de usuario y base de datos MySQL
~~~
CREATE USER 'c25mysql'@'localhost' IDENTIFIED BY 'lacontraseña'; 
GRANT USAGE ON *.* TO 'c25mysql'@'localhost' REQUIRE NONE WITH MAX_QUERIES_PER_HOUR 0 MAX_CONNECTIONS_PER_HOUR 0 MAX_UPDATES_PER_HOUR 0 MAX_USER_CONNECTIONS 0;
CREATE DATABASE IF NOT EXISTS `c25base1`;
GRANT ALL PRIVILEGES ON `c25base1`.* TO 'c25mysql'@'localhost'; 
~~~

#### Version de apache
~~~
cd \xampp\apache\bin
httpd.exe -v
~~~

#### XAMPP configuración Virtual Host
https://httpd.apache.org/docs/2.4/vhosts/examples.html

###### httpd-vhosts.conf que se encuentra en la carpeta \xampp\apache\conf\extra\httpd-vhosts.conf    
~~~
# Esta acción nos permite trabajar con hosts virtuales basados en nombres. El * representa un número IP.
NameVirtualHost *:80

<VirtualHost *:80>
	DocumentRoot "E:/xampp/htdocs"
	ServerName localhost
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "E:/xampp/htdocs/web"
    ServerName www.veiga.local
    ServerAlias veiga.local
    <Directory "E:/xampp/htdocs/web">
        Options All
        AllowOverride All
        Require all Granted
        # En versiones anteriores de Apache 2.4 poner estas directivas en lugar de las 2 anteriores.
        # Order allow,deny
        # Allow from all
    </Directory>
</VirtualHost>
~~~

#### Confirm that all the syntax in the Apache configuration is correct
~~~
cd \xampp\apache\bin
httpd.exe -t
~~~

##### HTTPS with virtual hosts on XAMPP
https://florianbrinkmann.com/en/4215/https-virtual-hosts-xampp/
###### Creating an SSL certificate
- Go to the Apache directory \xampp\apache.
- Run makecert.
- Enter a PEM passphrase and the other information you are asked for. For Common Name, you should enter the domain you want to use for the virtual host, so the certificate is signed for that domain.
- After processing all steps, you maybe want to import the cert into your browser (it lives under /xampp/apache/conf/ssl.crt/server.crt). Nevertheless, you will get a warning about insecure self-signed certificate after loading your website – you need to add it as an exception.

