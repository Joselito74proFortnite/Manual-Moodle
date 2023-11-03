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

![paVosfree](/Imagenes/7.png)

2. Crea els següents cursos: un curs anomenat A (sense categoria) que estigui format per 3 temes i un altre anomenat B (també sense categoria) que estigui format per 5 temes. Tot això ho pots fer des de Administració del lloc->Gestiona cursos i categories o també des del quadre Navegació anant a Cursos > Afegeix curs

![paVosfree](/Imagenes/8.png)
![paVosfree](/Imagenes/9.png)

3. Vés a algun dels cursos creats al punt anterior (simplement seleccionant-lo dins del quadre Navegació) i fes que contingui en algun del seus temes algun tipus de material (un document PDF, per exemple), canvia el títol d'algun tema i, en general, investiga les possibilitats que et dóna el botó Activar edició en un curs.
NOTA: Aquestes possibilitats no les estudiarem a fons perquè són una tasca més pròpia del professor que no pas de l'administrador del Moodle, però sempre va bé tenir-ne alguna idea.

![paVosfree](/Imagenes/10.png)

4. Creació d’usuaris i alumnes.
a) Crea manualment un usuari anomenat Bob que ha de fer servir el mètode d'autenticació manual. Això es pot fer des de Administració del lloc > Usuaris > Comptes > Afegeix un usuari

![paVosfree](/Imagenes/11.png)

b) Genera deu alumnes que ho seran dels dos cursos A i B . Fes servir un arxiu CSV per realitzar aquesta creació en bloc. Vés a Administració del lloc > Usuaris > Comptes > Carrega usuaris i segueix els passos que et marca.
NOTA: Per saber el contingut que hauria de tenir aquest fitxer, consulteu més abaix a la secció Usuaris.

![paVosfree](/Imagenes/11.png)

c) Elimina dos dels deu alumnes creats a l'apartat anterior fent servir l'opció Administració del lloc > Usuaris > Accions amb usuaris en bloc

![paVosfree](/Imagenes/12.png)
![paVosfree](/Imagenes/13.png)

5. Ara matricula aquests usuaris als diferents cursos.
a) Fes que al curs A no hi hagi possibilitat d'inscripció (és a dir, que només es permeti l'accés de visitant de manera que el curs sigui totalment públic sense control d'usuaris -ni alumnes ni professors-). 

![paVosfree](/Imagenes/14.png)

**He borrado todos los metodos de matriculacion**

D'altra banda, fes que al curs B es necessiti registre manual d'usuaris (és a dir, que sigui l'administrador -tu- qui matriculi cada usuari al curs, ja sigui com a professor o com a alumne).
Tot això ho pots fer des de Administració del curs > Ususaris > Mètodes d'inscripció. 
Si no surt algun mètode d'inscripció disponible, has d'activar-lo a: Administració de lloc > Connectors > Autenticació > Gestió de l'autenticació


**GRUPO B (SIN METODO DE MATRICULACION)**

![paVosfree](/Imagenes/15.png)
![paVosfree](/Imagenes/16.png)
![paVosfree](/Imagenes/17.png)

**Grupo A (El Profesor Matricula)**

![paVosfree](/Imagenes/18.png)
![paVosfree](/Imagenes/19.png)

b) Assigna com a professor del curs B l'usuari "Bob" i com a alumnes a tots els que fas afegir des de l'arxiu CSV Tot això ho pots fer anant a Administració del curs > Usuaris inscrits > Inscriure.

![paVosfree](/Imagenes/20.png)

c) Comprova que efectivament, el contingut del curs A (afegit per l'administrador del sistema -és a dir, tu- estigui disponible públicament i que per accedir al curs B s'hagi d'iniciar sessió amb un usuari registrat (alumne o professor)

![paVosfree](/Imagenes/21.png)
![paVosfree](/Imagenes/22.png)

6. Canvia l'aparença estètica del teu lloc. Concretament, descarrega't i activa un tema diferent dels que venen per defecte i prova de canviar també la capçalera i el peu de pàgina del lloc. Això ho pots fer primer anant a Administració del lloc > Connectors > Instal·lar complement i després a Administració del lloc > Aparença > Temes > Selector de temes 
Sempre pots fer servir l'enllaç Canvi de rol del menú de la dreta per observar com es veuria el lloc sent alumne, professor, etc.

![paVosfree](/Imagenes/23.png)

7. Assigna un professor i matricula alumnes al curs A

![paVosfree](/Imagenes/24.png)

8. Amb el professor afegeix contingut al curs A. Afegeix diferents tipus d’activitats i recursos. Crea una tasca amb data d’entrega oberta que demani la càrrega d’un fitxer PDF.

![paVosfree](/Imagenes/25.png)
![paVosfree](/Imagenes/26.png)

9. Entra amb un alumne i comprova que pots lliurar la tasca.

![paVosfree](/Imagenes/27.png)

![paVosfree](/Imagenes/28.png)

![paVosfree](/Imagenes/29.png)

![paVosfree](/Imagenes/30.png)

![paVosfree](/Imagenes/31.png)

![paVosfree](/Imagenes/32.png)

![paVosfree](/Imagenes/33.png)

![paVosfree](/Imagenes/34.png)

![paVosfree](/Imagenes/35.png)

![paVosfree](/Imagenes/36.png)

![paVosfree](/Imagenes/37.png)

![paVosfree](/Imagenes/38.png)

![paVosfree](/Imagenes/39.png)
