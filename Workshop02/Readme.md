# Workshop 02

## Que necesitamos para desplegar una aplicación web?

- Servidor web
- Almacenamiento
- Dominio
- Una IP
- Una App (backend, frontend, fullstack)
- Base de datos
- Presupuesto
- Seguridad
    - Firewall
- SEO
    - Analytics

## Se realizará un servidor con LAMP (Linux, Apache, MySQL y PHP)

### Para iniciar la máquina vagrant en el anfitrión

´´´bash
cd ISW811/VMs/webserver
vagrant up
´´´

### Para iniciar la máquina vagrant con ssh

´´´bash
cd ISW811/VMs/webserver
vagrant ssh
´´´

### Para cambiar el nombre de host se debe ejecutar este comando, al final va el nombre del server, en este caso es webserver, luego salimos y volvemos a ingresar

´´´bash
sudo hostnamectl set-hostname webserver
exit
vagrant ssh
´´´

### Antes de continuar se deben actualizar la lista de paquetes elegibles, con el siguiente comando se descargan los paquetes disponibles. Seguidamente con las últimas 4 líneas se instalan los paquetes necesarios

´´´bash
sudo apt-get update

sudo apt-get install vim vim-nox \
curl git apache2 mariadb-server mariadb-client \
php7.4 php7.4-bcmath php7.4-curl php7.4-json \
php7.4-mbstring php7.4-mysql php7.4-xml
´´´

### Ahora se comprobará la dirección de IP desde la máquina anfitriona, se encuentra en el archivo Vagrantfile con el parámetro private_network y se sle hace ping

´´´bash
code Vagrantfile
ping 192.168.56.10
´´´

### Se modifica el archivo hosts de la máquina anfitriona desde un cmd y utilizando los siguientes comandos.

´´´bash
cd \
cd Windows\System32\drivers\etc
notepad hosts
´´´

### dentro del archivo hosts se agrega la línea con la IP y el nombre del dominio, en este caso es 192.168.56.10 javier.isw811.xyz
![img](Images/Captura%20de%20pantalla%202023-05-30%20202556.png)

### Ya guardado se hace ping para verificar que todo funcione y luego se puede acceder a la página desde un navegador ingresando a javier.isw811.xyz

´´´bash
ping javier.isw811.xyz
´´´

![img](Images/page.png)

## Se activan los módulos para habilitar host virtuales y certiificados ssl dentro de la máquina virtual

´´´bash
sudo a2enmod vhost_alias rewrite ssl
sudo systemctl restart apache2
´´´