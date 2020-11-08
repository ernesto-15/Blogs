## Instalaciones que necesitarás para empezar a usar WSL en tus proyectos

Históricamente, Windows nunca fue el sistema operativo favorito de los desarrolladores web, de hecho, Windows llegó a ser odiado por muchos de estos. 😅 Pero gracias ***Windows Subsystem for Linux (WSL)*** las cosas están cambiando. WSL permite trabajar con Linux y Windows al mismo tiempo. 

Entonces, es posible usar la terminal de Ubuntu en una ventana y Microsoft Excel en otra, y todo **al mismo tiempo! 😍**

> Si aún no viste el post en el que hablo de WSL y como instalarlo, te lo dejo en [este enlace.](https://ernestoangulo.hashnode.dev/sigues-usando-cmd-en-2020-te-presento-a-wsl)

Si ya tienes instalado WSL, tal vez te estés preguntando ¿Ahora como empiezo a usarlo en mis proyectos? 🤔

¡Hola! Soy Ernesto y en este post voy a enseñarte como instalar, en WSL, **herramientas que son indispensables para un desarrollador web como Git o Node** para que puedas, desde ya, a empezar a usar WSL para tus proyectos.

---
# Tabla de contenidos

1. [Instalación de Git](#instalacion-de-git)
2. [Instalación de NodeJS](#instalacion-de-nodejs)
    1. [Instalar NVM](#instalar-nvm)
    2. [Instalar Node](#instalar-node)
3. [Instalación de MySQL](#instalacion-de-mysql)
    1. [Conectar MySQL](#conectar-mysql)
    2. [Crear contraseña](#crear-contrasena)
    3. [Conectar con MySQL Workbench](#conectar-con-mysql-workbench)
4. [Ya puedes empezar](#ya-puedes-empezar)
---

# Instalación de Git
Para instalar Git en WSL ejecuta el siguiente comando:
```bash
sudo apt install git
```
Si la distribución que instalaste en WSL es Ubuntu, notarás que al ejecutar el comando `git --version` para verificar la versión de Git instalada, esta no es la última versión ofrecida por Git.

Para actualizar a la última versión es necesario el PPA que ofrece Ubuntu, para agregarla ejecuta este comando:
```bash
sudo add-apt-repository ppa:git-core/ppa
```
*Recuerda que al usar sudo deberás ingresar tu contraseña de super usuario*

Una vez agregado el PPA, verifica si existen actualizaciones y, si existen, instalalas.:
```bash
# Verificar si existen actualizaciones disponibles
sudo apt update

# Instalar actualizaciones
sudo apt upgrade
```
Ahora si verificas la versión de Git instalada, esta debe ser la última.

***En la fecha de publicación de este post la última versión de Git es `2.29.2`***
```bash
git --version
# git version 2.29.2
```



# Instalación de NodeJS
Al igual que Git, Node es una herramienta indispensable para los desarrolladores web.

### Instalar NVM
La manera más recomendada de instalar Node en WSL es mediante NVM *(Node Package Manager)* que es un manejador de versiones de Node.

Si estas usando bash, instala NVM ejecutando este comando:
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```
Si estas usando zsh, solo abre el archivo `.zshrc` y agrega el plugin de NVM.
```bash
plugins=(git nvm)
```
*Si no sabes como ver que shell estas usando, ejecuta `echo $SHELL`*

> La ventaja de usar NVM es que es posible instalar más de una versión de Node y el intercambio entre ellas es muy fácil.

### Instalar Node
Una vez tienes NVM instalado, puedes instalar cualquier versión de Node ejecutando el siguiente comando.
```bash
nvm install 15.1.0
```
***En la fecha de publicación de este post la última versión de Node es `15.1.0`***

Puedes cambiar `15.1.0` por la versión de Node que desees instalar. Para intercambiar una versión por cualquier otra, ejectua el siguiente comando:
```bash
nvm use version_que_quieres_usar
```
Al instalar Node, también se instala NPM. Para comprobarlo, ejecuta los siguientes comandos:
```bash
node -v
# v14.12.0

npm -v
# 6.14.8
```

# Instalación de MySQL
Antes de instalar MySQL debes asegurarte que todos tus paquetes esten actualizados, mediante los siguiente comandos:
```bash
# Verificar si existen actualizaciones disponibles
sudo apt update

# Instalar actualizaciones
sudo apt upgrade
```
Una vez los paquetes estén actualizados, ejecuta el siguiente comando para instalar MySQL.
```bash
sudo apt install mysql-server
```
Puedes confirmar la instalación ejecutando el siguiente comando que debe imprimir la versión actual de MySQL.
```bash
mysql --version
# mysql  Ver 8.0.22-0ubuntu0.20.04.2 for Linux on x86_64 ((Ubuntu))
```

### Conectar MySQL
Antes de conectarse a MySQL, es necesario que primero se debe iniciar el servicio.
```bash
sudo /etc/init.d/mysql start
```
Una vez esta iniciado el servicio, conéctate a MySQL.
```bash
sudo mysql
```
*Y para cerrar la conexión ejecuta `exit`.*

### Crear contraseña
Es muy recomendado el tener una contraseña para proteger el acceso a MySQL.

Para crear una contraseña primero debes conectarte a MySQL y dentro de la consola debes ejecutar el siguiente comando.
```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'tu_contraseña';
```
Una vez la contraseña es creada, para volver a conectarte a MySQL deberás hacerlo mediante el siguiente comando:
```bash
mysql -h localhost -u root -p
```
*Te pedirá que ingreses la contraseña que acabas de crear, la ingresas y ya deberías poder conectarte de forma más segura.*

![mysql-console.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604869354480/KHl4CijDI.png)


### Conectar con MySQL Workbench
En este paso es donde se ve la magia de WSL. Podrás usar un programa instalado en Windows como lo es MySQL Workbench con un servidor MySQL instalado y conectado en Linux. 🤯
> Si no tienes MySQL Workbench instalado en tu computadora, lo puedes descargar e instalar en [este enlace](https://dev.mysql.com/downloads/workbench/).

Una vez instalado, ejecuta el programa y crea una nueva conexión.

![workbench-create-conecction.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604869506107/wgpcP34ez.png)

Ingresa el nombre de la conexión e ingresa la contraseña que creaste haciendo click en el botón *Store in Vault*.


![workbench-password.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604869658194/LCFMBxz-_.png)

Para probar la conexión dale click en Test Connection. Si la conexión es exitosa da click en *OK.*

![workbench-test-connection.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604869700626/fJKQ5Rg3z.png)

# Ya puedes empezar 🥳
Y listo eso es todo. Estas listo para empezar a usar WSL con tus proyectos. Solo abre VS Code o el editor de tu presencia y empieza a codear. 👩‍💻 👨‍💻

Existen muchísimas más herramientas que un desarrollador necesita, pero en este post quería cubrir solo las más básicas. Pero te recomiendo que si tienes alguna duda de como instalar cualquier herramienta, busques como instalarla en Ubuntu o la distribución que tengas instalada, después de todo estas ejecutando **Linux REAL dentro de Windows.** 😉

Si te gusto el post o te ayudó en algo dale like y si tienes algún aporte, comentario o recomendación, escríbela en los comentarios. Me es de gran ayuda para mejorar mi contenido. 😃 Nos vemos en el siguiente post. 👋

---

# Recursos
* [https://git-scm.com/download/linux](https://git-scm.com/download/linux)
* [https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-database](https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-database)
* [https://github.com/nvm-sh/nvm#about](https://github.com/nvm-sh/nvm#about)

---
