## Zsh + Oh My Zsh = Una terminal hermosa y poderosa

En el [pasado post](https://ernestoangulo.hashnode.dev/sigues-usando-cmd-en-2020-te-presento-a-wsl) aprendiste a instalar WSL, lo que te permitió obtener todo el poder de la terminal Linux dentro de Windows. Lo cual es genial! 😉

Sin embargo, al abrir la terminal y al empezar a usarla, tal vez sientas que se ve un poco aburrida o fea. 🙃 Bueno, no tienes nada de que preocuparte 😃 porque te enseñaré a solucionar este problema de una forma fácil.

![Ubuntu-terminal.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604255915652/FHHVLVCr4.png)

¡Hola! Soy Ernesto y en este post, tal y como lo prometí en [el anterior](https://ernestoangulo.hashnode.dev/sigues-usando-cmd-en-2020-te-presento-a-wsl), voy a enseñarte a instalar el *shell* **`Zsh`** y personalizarlo con el *framework* **`Oh My Zsh`**. Gracias a estas herramientas le darás un poder extra a tu terminal mediante *plugins* y también ese toque que necesita para verse muy bonita y profesional. 😉



---
# Tabla de Contenidos
1. [¿Qué es Zsh?](#que-es-zsh)
2. [¿Qué es Oh My Zsh?](#que-es-oh-my-zsh)
3. [Instalación de Zsh](#instalacion-de-zsh)
  1. [Actualizar paquetes de Ubuntu](#actualizar-paquetes-de-ubuntu)
  2. [Instalar Zsh y hacerlo el shell por defecto](#instalar-zsh-y-hacerlo-el-shell-por-defecto)
4. [Instalación de Oh My Zsh](#instalacion-de-oh-my-zsh)
  1. [Instalar extensión de Visual Studio Code](#instalar-extension-de-visual-studio-code)
  2. [Acceder al archivo de configuración](acceder-al-archivo-de-configuracion)
  3. [Editar tema](#editar-tema)
  4. [Añadir plugins](#anadir-plugins)
5. [Instalación de Powerlevel10k](#instalacion-de-powerlevel10k)
  1. [Instalar NerdFonts](#instalar-nerdfonts) 
  2. [Clonar repositorio de GitHub](#clonar-repositorio-de-github)
  3. [Establecer Powelevel10k como tema por defecto](#establecer-powelevel10k-como-tema-por-defecto)
6. [Configuración de Windows Terminal](#configuracion-de-windows-terminal)
  1. [Cambiar fuente](#cambiar-fuente)
  2. [Cambiar tema (opcional)](#cambiar-tema-opcional)
7. [Configuración de fuente de Visual Studio Code](#configuracion-de-fuente-de-visual-studio-code)
8. [Conclusiones](#conclusiones)
---



*Antes de empezar la instalación necesitas conocer que es `Zsh` y `Oh My Zsh`.*



# ¿Qué es Zsh?
**Z shell** o también llamado **Zsh** es un *shell* o intérprete de comandos para sistemas operativos basados en UNIX, como los son Linux y macOS. Este *shell* incorpora muchas características de otros *shell* muy populares como `bash`, `ksh` o `tcsh`.
>En palabras más simples, Zsh te permite comunicarte con tu computadora mediante comandos.



# ¿Qué es Oh My Zsh?
Es un *framework open source* para manejar la configuración de **Zsh**. **Oh My Zsh** viene incluido con *plugins* y más de 150 temas que nos ayudarán a facilitar nuestro trabajo y harán que nuestra terminal se vea genial.
>Aparte de los 150 temas que vienen incluidos, también puedes instalar otros, de los cuales el más popular es **Powelevel10k**.

Antes de empezar recuerda que:

*Todo el proceso de instalación lo realizaré en Windows, con **WSL y Ubuntu**, los cuales aprendimos a instalar en el [post pasado](https://ernestoangulo.hashnode.dev/sigues-usando-cmd-en-2020-te-presento-a-wsl).*

Ahora sí, pasemos a lo divertido. 😄



# Instalación de Zsh
### Actualizar paquetes de Ubuntu
Para poder instalar Zsh, debes asegurarte de tener todos tus paquetes de Ubuntu actualizados.

*Si ya tienes actualizados todos los paquetes puedes pasar al [siguiente paso](#instalar-zsh-y-hacerlo-el-shell-por-defecto).*

Abre Windows Terminal, selecciona la terminal de Ubuntu y ejecuta el siguiente comando:

```
sudo apt update
```
Este comando verificará si existe alguna actualización disponible para tus paquetes.

*Recuerda que al usar sudo necesitarás introducir la **contraseña de super usuario** que creaste al [instalar Ubuntu](https://ernestoangulo.hashnode.dev/sigues-usando-cmd-en-2020-te-presento-a-wsl#instalar-una-distro-de-linux).*

Cuando el proceso termina se listarán todos los paquetes que necesitan una actualización. Para actualizarlos ejecuta este comando:

```
sudo apt upgrade
```
*Este proceso puede demorar muchos minutos en completarse.*

### Instalar Zsh y hacerlo el shell por defecto
Ejecuta este comando para instalar Zsh:
```
sudo apt install zsh
```
Una vez terminada la ejecución, ejecuta este otro comando para hacer a Zsh el *shell* por defecto (recuerda ingresar tu contraseña de super usuario):
```
chsh -s $(which zsh)
```
Una vez terminado el proceso, cierra Windows Terminal y vuélvelo a abrir. Cuando se abra, te pedirá que hagas la configuración inicial de Zsh. Escribe 2 y presiona Enter.

![Initial-configuration-zsh.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604262108798/5mQ1CJ9U1.png)

*Notarás que los colores de la terminal cambiaron, esto es porque Zsh configuró un tema por defecto. Aprenderás a cambiar este tema en los siguientes pasos.*

Con estos simples pasos ya tienes Zsh como *shell* por defecto en tu terminal. Para verificarlo, ejecuta este comando:
```
echo $SHELL
```

El que debería imprimir lo siguiente: `/usr/bin/zsh`.



# Instalación de Oh My Zsh
Para instalar Oh My Zsh solo tienes que ejecutar el siguiente comando:
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
*Una vez terminado el proceso, notarás, una vez más, que el tema de la terminal cambió. Esto es porque Oh My Zsh configuró el tema por defecto llamado `robbyrussell`.*

![Oh-my-zsh.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604262426102/f8Rb5uh3c.png)

### Instalar extensión de Visual Studio Code
Para poder seguir con los siguientes pasos, debes tener instalada la extensión llamada [Remote - WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) para poder usar **WSL con Visual Studio Code**. Si la tienes instalada, continua con el [siguiente paso](#acceder-al-archivo-de-configuracion) y si no, ve a las extensiones e instálala.

![Remote-wsl.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604262546208/pBVNIwXai.png)

### Acceder al archivo de configuración
Este archivo es el que contiene toda la configuración de Zsh y es el que debes editar para poder habilitar los diferentes temas o *plugins* que quieras instalar.

Para editar este archivo con Visual Studio Code debes ejecutar el siguiente comando:
```
code ~/.zshrc
```

### Editar tema
Para poder usar los más de 150 temas que vienen por defecto en Oh My Zsh, debes buscar, en el archivo de configuración `(.zshrc)`, la configuración llamada `ZSH_THEME`. Debes editar esta con el nombre del tema que prefieras.

*En [este link](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes) te dejo todos los temas que tiene Oh My Zsh por defecto.*

Si no estas seguro que tema usar,  te recomiendo escribir `random` y guardar el archivo. Con esta configuración cada vez que abras la terminal, se usará un tema diferente y se mostrará el nombre de cada uno. Así, si encuentras uno que te gusta, puedes copiar ese nombre y reemplazar `random`.

```
ZSH_THEME = "random"
```

![Random-theme.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604262967300/q-WUgFWxA.png)

### Añadir plugins
Los *plugins* entregan mayor funcionalidad a la terminal. Entre los *plugins* más famosos están los de `autosuggestions` y `syntax highlighting`, los cuales instalarás a continuación.

El primero sugiere comandos para autocompletarlos en base a los que vayas escribiendo. Y el segundo colorea los comandos dependiendo de su función.

Para instalar el *plugin* de `autosuggestions` ejecuta el siguiente comando:
```
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
```
Y para instalar el de `syntax highlighting` ejecuta este:
```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```
Con esto ya los tienes instalados, pero falta habilitarlos. Para habilitarlos, ve al archivo `.zshrc`, busca la configuración **"plugins"** y añade los *plugins* que acabas de instalar:
```
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```
*Si quieres instalar más plugins, te dejo una lista de [todos los plugins disponibles](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins).*



# Instalación de Powerlevel10k
Si bien Oh My Zsh ya viene con muchos temas por defecto, el tema más popular y, en mi opinión, el mejor es **Powerlevel10k**, el cual instalarás a continuación.

### Instalar NerdFonts
Para que el tema Powerlevel10k funcione correctamente necesitamos instalar alguna fuente de NerdFonts. Existen muchas fuentes diferentes, si quieres verlas todas te dejo [todas las fuentes disponibles](https://www.nerdfonts.com/font-downloads). Sin embargo, la fuente que yo te recomiendo es **FuraMono**, la cual puedes descargar en [este link](https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/FiraMono/Regular/complete/Fura%20Mono%20Regular%20Nerd%20Font%20Complete.otf?raw=true).

Una vez descargado el archivo, debes ejecutarlo e instalarlo.

### Clonar repositorio de GitHub
Para clonar el [repositorio](https://github.com/romkatv/powerlevel10k) ejecuta este comando:
```
git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```

### Establecer Powelevel10k como tema por defecto
Llegó el momento de establecer Powerlevel10k como tu tema por defecto en el archivo `.zshrc`. En la configuración `ZSH_THEME` escribe lo siguiente:
```
ZSH_THEME="powerlevel10k/powerlevel10k"
```
También, en la línea siguiente añade esta configuración para habilitar la fuente que acabas de instalar:
```
POWERLEVEL9K_MODE="nerdfont-complete"
```

![Zsh-theme.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604264273723/pXPUuAOTV.png)

Guarda el archivo y ya puedes cerrarlo.

Ahora, cuando vuelves a la terminal, debería aparecerte la configuración inicial de Powerlevel10k:

>Para realizar esta configuración solo debes de leer las indicaciones y elegir las opciones que más te gusten.


![P10k-initial-configuration.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604264359419/8r6pP6gud.png)

¡Pero todavía no presiones nada! Te falta un paso muy importante.

Se puede notar que  se muestran dos rectángulos sin relleno en lo que debería ser un diamante. 🔷 Esto es porque aún no configuraste la fuente instalada previamente **(FuraMono)** en Windows Terminal.

![No-diamond.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604264423557/18t_g5JWf.png)



# Configuración de Windows Terminal

### Cambiar fuente
En Windows Terminal, haz click en el menú desplegable y selecciona configuración o *settings* (si lo tienes en inglés) para abrir el archivo de configuración de Windows Terminal en Visual Studio Code.

> No confundir el archivo de configuración de Windows Terminal `(settings.json)` con el de Zsh `(.zshrc)`. Los dos son muy diferentes.

Ahora, para establecer FuraMono como fuente en Windows Terminal, tienes que dirigirte a la configuración de la terminal de Ubuntu y añadir la siguiente línea:
```json
"fontFace": "FuraMono Nerd Font"
```

![WT-font-face.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604264681663/uTL7d7wg2.png)

Una vez hecho esto, si vuelves a la terminal, ya debería aparecer el diamante y ya puedes iniciar la configuración inicial de Powerlevel10k. 😉😉

![Yes-diamond.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604264788632/qJztzvEEf.png)

### Cambiar tema (opcional)
Una vez terminas la configuración, tu terminal se debería ver algo parecido a esto (cambiará dependiendo de las opciones elegidas en la configuración):

![P10k-no-theme.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604264923844/quEM_wbJQ.png)

Así como se pueden seleccionar temas para Zsh, también puedes cambiar el tema de Windows Terminal, y así personalizar sus colores.

> Si quieres que haga un post dedicado a como **personalizar Windows Terminal** házmelo saber en los comentarios. 😁

Existen muchos temas disponibles, acá te dejo un enlace a [Terminal Splash](https://terminalsplash.com/) para que veas todos los que tienen.  En lo personal, mi tema favorito se llama `"Aurelia"` y para establecer este tema en tu terminal, en el mismo archivo de configuración de Windows Terminal, busca la palabra ***schemes*** y, dentro del arreglo, pega lo siguiente:
```json
{
  //Color Scheme: Aurelia
  "name": "Aurelia",
  "background": "#1a1a1a",
  "black": "#000000",
  "blue": "#579BD5",
  "brightBlack": "#797979",
  "brightBlue": "#9CDCFE",
  "brightCyan": "#2BC4E2",
  "brightGreen": "#1AD69C",
  "brightPurple": "#975EAB",
  "brightRed": "#EB2A88",
  "brightWhite": "#EAEAEA",
  "brightYellow": "#e9ad95",
  "cyan": "#00B6D6",
  "foreground": "#EA549F",
  "green": "#4EC9B0",
  "purple": "#714896",
  "red": "#E92888",
  "white": "#EAEAEA",
  "yellow": "#CE9178"
}
```

Y en la configuración de la terminal de Ubuntu debes agregar esta línea:

```json
"colorScheme": "Aurelia"
```

Dentro de este arreglo de `scheme` puedes agregar todos los temas que desees. Y para cambiarlo simplemente debes de cambiar la configuración previa con el nombre del tema que desees.

![WT-color-scheme.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604265090192/tXcqHOP9q.png)

# Configuración de fuente de Visual Studio Code

Este es el último y el paso más corto de este post. Solo tenemos que cambiar la fuente que Visual Studio Code utilizará para su terminal integrada.

Abre la configuración, busca "terminal font" y en esa configuración pega esto: `FuraMono Nerd Font`.

![VSCode-font.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604265182101/xkLfyVhRU.png)

¡Y listo! Eso es todo lo que teníamos por hacer. 🥳 🥳 🥳



# Conclusiones
¡Enhorabuena! Pasaste de tener una terminal que se veía así:

![Cmd.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604265249595/PDN3-_RJA.png)

A una que se ve totalmente diferente:

![P10k.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1604265265607/V75vrcDd6.png)

¿Puedes notar esa grandísima diferencia no? 😅 Gracias a WSL, Zsh, Oh My Zsh y Windows Terminal ahora tienes una terminal muy hermosa y también muy poderosa. 😎

En el siguiente post planeo hablar de algunas instalaciones necesarias, tips o problemas con los que me he topado al empezar a usar WSL para mis proyectos, así que te veo ahí, no te lo pierdas. 😉

Si te gusto el post o te ayudó en algo dale like y si tienes algún aporte, comentario o recomendación, escríbela en los comentarios. Me es de gran ayuda para mejorar mi contenido. 😃 Nos vemos en el siguiente post. 👋



---
# Recursos
* [https://ohmyz.sh/](https://ohmyz.sh/)
* [https://github.com/romkatv/powerlevel10k](https://github.com/romkatv/powerlevel10k)
* [https://github.com/ohmyzsh/ohmyzsh/wiki/Themes](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)
---