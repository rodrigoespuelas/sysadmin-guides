###### XAMPP configuración Servidor Virtual www.dominio.local

####### httpd-vhosts.conf que se encuentra en la carpeta \xampp\apache\conf\extra\httpd-vhosts.conf  
`
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
        AllowOverride All
        Require all Granted
        # En versiones anteriores de Apache 2.4 poner estas directivas en lugar de las 2 anteriores.
        # Order allow,deny
        # Allow from all
    </Directory>
</VirtualHost>
`
