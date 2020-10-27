## ¿Sigues usando CMD en 2020? Te presento a WSL - Parte 1

# A todos nos ha pasado
Si estas empezando en el desarrollo web y tu computadora es Windows, seguramente te haz cruzado con diversos cursos o tutoriales en los que el instructor o instructora tenía una terminal que se veía más o menos así 🤩:

![Terminal.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1603748720519/yfPQtr-1W.png)

O ejecutaba comandos como `clear` o `ls`, los cuales tratabas de ejecutar en tu terminal pero no funcionaban e imprimían un error. Bueno si tienes este problema, déjame decirte que estas usando la terminal equivocada 😅.

![Cmd.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1603748851899/qS9v7N5il.png)

Tal vez pienses que estos son solo "detalles" o que no tienen importancia, pero no hay nada más alejado de la realidad.

>Como dice un dicho muy popular y **muy cierto**: **"La terminal es la mejor amiga 💙 del programador"**

La terminal es de suma importancia para un desarrollador y las preferidas por la mayoría de estos son las de Linux o macOS, los cuales son sistemas operativos basados en UNIX.

¡Hola! Soy Ernesto y en este post voy a enseñarte a obtener todo el poder 💪 de una **terminal Linux dentro de Windows con WSL** (sí, **sin nada de particiones de disco**). Y, por qué no, en el siguiente post, también te enseñaré como hacer que tu terminal se vea como la de un pro, para que dejes de usar esa terminal tan horrenda 🤢 llamada `cmd`.

---
# Tabla de contenidos
1. [¿Qué es WSL?](#que-es-wsl)
2. [Instalación de WSL](#instalacion-de-wsl)
  1. [Habilitar WSL](#habilitar-wsl)
  2. [Instalar una distro de Linux](#instalar-una-distro-de-linux)
  3. [Actualizar a WSL 2](#actualizar-a-wsl-2)
    1. [Habilitar VMP *(Virtual Machine Plataform)*](#habilitar-vmp-virtual-machine-plataform)
    2. [Instalar el kernel de Linux](#instalar-el-kernel-de-linux)
    3. [Configura WSL 2 como la versión por defecto](#configura-wsl-2-como-la-version-por-defecto)
  4. [Instalar Windows Terminal](#instalar-windows-terminal)
3. [Siguientes pasos](#siguientes-pasos)
---


# ¿Qué es WSL?
Antes de empezar, debemos hablar de WSL *(Windows Subsystem for Linux)* que es una pieza muy importante para poder correr Linux dentro de Windows.

WSL es una capa de compatibilidad desarrollada por Microsoft para correr ejecutables de Linux nativamente en Windows. En otras palabras, nos permite **instalar distros de Linux REALES como Ubuntu en Windows**. Lo que significa que podemos utilizar herramientas como `bash` o `zsh` para administrar nuestros archivos de Windows 🤯.

>Con WSL podremos ejecutar Adobe Photoshop (no disponible en Linux) en una ventana y Ubuntu en otra, todo al mismo tiempo.


# Instalación de WSL
Para poder instalar WSL en tu computadora, primero debes asegurarte de cumplir estos requisitos:
* Tener Windows 10
* Tener como mínimo la versión 1607 para WSL 1. Para WSL 2 la versión mínima es la 1903.
 * *Para ver la versión de Windows que posees sigue estos pasos:*
   1. Presiona la combinación de teclas `Windows + R`.
   2. Escribe `winver` y presiona enter.
* Para WSL 2 también es necesario tener la virtualización habilitada
 * *Para habilitar la virtualización te invito a ver [este video](https://www.youtube.com/watch?v=B1oCkcOHXPA&list=LL&index=12&ab_channel=%EA%A7%81Tut%E2%9C%BFsVicky34%EA%A7%82).*

### Habilitar WSL
Abre PowerShell como administrador y ejecuta el siguiente comando:
```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
*Una vez el proceso termina, debes reiniciar tu computadora.*

### Instalar una distro de Linux
Abre la tienda de Microsoft *(Microsoft Store)* y busca "Linux". Puedes instalar la distro que prefieras y si no te puedes decidir, te recomiendo que instales Ubuntu.

![Ubuntu-microsoft-store.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1603759079236/WWDXckXTv.png)

Cuando termine la instalación, abre la terminal Ubuntu en donde se mostrará el mensaje de que se esta instalando, al terminar pedirá la siguiente información:
* Nombre de usuario
* Contraseña de superusuario *(root)* y confirmación de la misma


![Installing-Ubuntu.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1603751635842/kyk9uQSJX.png)

***No olvides guardar esta contraseña en un lugar seguro.***

### Actualizar a WSL 2
WSL 2 es la segunda versión de WSL. Es muy superior en rendimiento, ofrece mayor compatibilidad y es la recomendada por Microsoft.

*Si quieres ver la comparación entre WSL 1 y 2 con mayor detalle, te invito a leer [este blog de Microsoft](https://docs.microsoft.com/en-us/windows/wsl/compare-versions).*

> Para este paso es importante cumplir los requisitos mencionados al [principio la instalación **(versión y virtualización)**](#instalacion-de-wsl). Si no cumples con estos requisitos, salta este paso y ve al [siguiente](#instalar-windows-terminal).

Antes de actualizar, revisa la versión de WSL que tienes actualmente. Abre PowerShell y ejecuta el siguiente comando:

```powershell
wsl -l -v
```

Este comando muestra las distribuciones que tenemos instaladas y la versión de WSL en la que están corriendo.

![WSL-version.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1603753788729/tqP7rgcj9.jpeg)

#### Habilitar VMP *(Virtual Machine Plataform)*
Ahora, para actualizar a la versión 2, debes ejecutar el siguiente comando en PowerShell para habilitar la plataforma de maquina virtual:

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

*Una vez el proceso termina, debes reiniciar tu computadora.*

#### Instalar el kernel de Linux
Descarga el kernel en este [link](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi), ejecuta el instalador descargado e instala el kernel aceptando todos los permisos solicitados.

#### Configura WSL 2 como la versión por defecto
Ejecuta el siguiente comando en PowerShell:

```powershell
wsl --set-default-version 2
```

Con esta configuración todas las distros que se instalen posteriormente correran en WSL 2 por defecto.

*Si ya tenías una distro instalada antes de actualizar a WSL 2, el cual es nuestro caso, debes actualizarla de manera manual con el siguiente comando:*

```powershell
wsl --set-version Ubuntu 2
```

### Instalar Windows Terminal
Microsoft tiene una aplicación que nos facilita el trabajo con la terminal y también movernos entre terminales PowerShell, CMD, Ubuntu o incluso Azure.

![Windows-terminal.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1603754651476/ECEFKMVG9.png)

En la tienda busca "terminal" e instálala. Una vez instalada, abre la aplicación, y selecciona la terminal de Ubuntu (también podrás seleccionar PowerShell o CMD).

¡Y listo! Ya tienes instalado WSL en tu computadora 😁.


![Windows-terminal-installed.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1603756300419/51SkhpkK-.jpeg)


# Siguientes pasos
Felicitaciones! ⭐ Ya tienes instalado WSL y ya eres capaz de usar la toda poderosa terminal de Linux en tu computadora Windows sin la necesidad de una partición de disco 😎. Técnicamente ya tienes todo el poder de la terminal en tus manos. Sin embargo, aún tenemos un pequeño problema, nuestra terminal no se ve tan bonita 😥.

No te preocupes. En el siguiente post te enseñaré, como lo prometí, a transformar tu terminal en toda una hermosura. Todo esto gracias a `zsh` y `oh-my-zsh` 😉.

Si tienes algún aporte, comentario o recomendación, escríbela en los comentarios. Me es de gran ayuda para mejorar mi contenido 😃. Nos vemos en el siguiente post 👋.

---
# Recursos
* [https://docs.microsoft.com/en-us/windows/wsl/install-win10](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
* [https://es.wikipedia.org/wiki/Windows_Subsystem_for_Linux](https://es.wikipedia.org/wiki/Windows_Subsystem_for_Linux)
* [https://fireship.io/lessons/windows-10-for-web-dev/](https://fireship.io/lessons/windows-10-for-web-dev/)
---