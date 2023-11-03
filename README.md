# Manual-Moodle

Crea una carpeta

## Vagrant
**Creamos vagrant con este comando:**

vagrant init ubuntu/jammy64

**Continuamos elevando las infraestructuras gracias a el siguientge comando:**

vagrant up --provider=virtualbox

**Y con estos pasos podemos hacer ssh a vagrant:**

vagrant ssh

**Podemos mirar los permisos y directorios con:**

ll /vagrant

## Apache2
1. Actualizacion

apt update

2. Instalacion de apache2

apt install -y apache2

3. Instalacion de la base de datos mysql-server

apt install -y mysql-server

4. Instalacion de librerias php

apt install -y php libapache2-mod-php

apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl

5. Reinicio de apache2

systemctl restart apache2

## MySQL
**Consola MySQL
En la terminal de forma root ponemos el siguiente comando:**

mysql

1. Creacion de la base de datos:
**Dentro de mysql cramos la base con nombre: bbdd**

CREATE DATABASE bbdd;

2. Creacion del usuario
Tingueu en compte que s'haurà d'identificar la IP des de la qual s'accedirà a la base de dades, en aquest cas, localhost.

CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

3. Dar permisos:

GRANT ALL ON bbdd.* to 'usuario'@'localhost';

4. *Salir de bbdd:

exit

5. Comprobar la conexion

mysql -u usuario -p

## Archivo ZIP
**Pasar el archivo zip**

1. Descargamos el ZIPY lo metemos en el directorio /vagrant/ y lo movemos a /var/www/html/:

mv /vagrant/arxiu.zip /var/www/html/

3. Instalamos el zip:

apt install zip

4. Utilizamos unzip para descomprimirlo

5. Eliminamos el index

rm index.html

6. Entramos a el directorio y lo copiamos

cd moodle 

cp -R * ..

Volvemos a el directorio anterior y eliminamos el archivo y moodle

cd .. 

rm arxiu.zip 

rm -r moodle

## Permisos per la web

**Per evitar errors deberiem copiar el zip amb cp -r si esta també amb un altre directori i eliminar el director amb rm -r. Per donar permisos anirem al directori /var/www/html i posarem les següents comandes:**

cd /var/www/html

chmod -R 775 . 

chown -R root:www-data .

systemctl restart apache2

exit

## Red pública
**Para hacer nuesta red publica tendremos que ir a vagrantfile y marcamos los siguentes comandos:**

config.vm.network "forwarded_port", guest: 80, host: 8080

config.vm.network "public_network"

vagrant reload




# CONFIGURACION MOODLE

1. Inicia sessió com a administrador del teu Moodle i realitza les següents tasques prèvies d'administració.

a) Canvia la teva direcció de correu electrònic i també la teva contrasenya per una altra. Afegeix-te a més un avatar. Tot això es pot fer anant al teu perfil (opció que apareix sota el teu nom que es veu a la part superior dreta de la finestra del Moodle) i clicant sobre l'enllaç Editar (o també anant a l'opció Preferències, situada al mateix lloc).

![paVosfree](/Imagenes/1.png)
![paVosfree](/Imagenes/2.png)

b) Canvia el nom del teu lloc (tant llarg com curt) i fes que la pàgina principal no mostri res pels usuaris que no estiguin autentificats. Això es pot fer anant a l'opció Administració del lloc > Primera plana > Paràmetres

![paVosfree](/Imagenes/3.png)
![paVosfree](/Imagenes/4.png)

c) Comprova que la franja horària del teu lloc sigui la correcta. Això es pot fer anant a l'opció Administració del lloc > Ubicació > Paràmetres.
NOTA: Aquesta configuració és important, per exemple, per les hores límit d'entregues d'exercicis

![paVosfree](/Imagenes/5.png)

d) Canvia l'idioma del teu lloc. Això es pot fer anant a l'opció Administració del lloc > Idioma > Paràmetres i tenint en compte tant el checkbox Detecció automàtica de l'idioma com el desplegable Idioma per defecte.
NOTA: Per disposar d'un determinat idioma, primer cal instal.lar-lo des de Administració del lloc > Idioma > Paquets d'idioma

![paVosfree](/Imagenes/6.png)

e) Canvia la política de contrasenyes de manera que els usuaris que es creiïn tinguin una contrasenya de com a mínim 4 caràcters incloent-hi, majúscules, minúscules i xifres. Això es pot fer anant a l'opció Administració del lloc > Seguretat >Normatives del lloc.

