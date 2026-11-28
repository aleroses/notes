# Curso de Prework: Configuración de Entorno de Desarrollo en Windows

> Ricardo Celis

## 1. ¿Qué es el navegador?

El **navegador** es el programa que nos permite acceder a las páginas web y visualizarlas. Funciona gracias al protocolo **HTTP/HTTPS** y se basa en tres tecnologías:

- **HTML**
- **CSS**
- **JS** (JavaScript)

### ¿Qué hace cada tecnología? (complemento)

- **HTML:** define la estructura y el contenido de la página.
- **CSS:** define los estilos (colores, tamaños, diseño).
- **JS:** agrega interactividad.

### Versiones de Google Chrome

- **Canary**
- **Dev** (la que se instala en el siguiente punto)
- **Stable**

### Otros navegadores para desarrollo

- **Edge** y sus DevTools.
- **Firefox Developer Edition**.

### Extensiones

- Ver extensiones para Google Chrome: [[vsc-chrome]]

## 2. Descarga e instala un navegador web: Chrome Dev

Descarga e instala la versión **Chrome Dev** de Google Chrome.

- [Enlace de descarga](https://www.google.com/intl/es_us/chrome/dev/)

### Pasos básicos

1. Entra al enlace de descarga.
2. Descarga el instalador y ejecútalo.
3. Al terminar, abre Chrome Dev y verifica que funcione.

## 3. Manejo básico de las DevTools

### Cambiar el idioma de Chrome

Podemos entrar a la configuración (*settings*) de Chrome y cambiar el idioma. No olvides darle a **Relaunch** para que se apliquen los cambios.

- [Chrome settings](chrome://settings/languages)

### Extensiones útiles

Podemos instalar extensiones desde la tienda de Chrome:

- **Toggle JavaScript:** conecta y desconecta rápidamente el JavaScript de la página.
- **Dev tools**
- **Lighthouse:** comprueba automáticamente la calidad de las páginas web.

[Chrome Web Store](https://chromewebstore.google.com/?hl=es)

### Abrir las herramientas de desarrollador

- `Ctrl + Shift + I`

### Otras formas de abrirlas

- Tecla `F12`.
- Clic derecho sobre la página → **Inspeccionar**.

## Quiz

### ¿Qué provee la herramienta Windows Subsystem for Linux?

- La transición entre plataformas Windows y Linux

### ¿Cómo se denomina la extensión que permite conectar y desconectar rápidamente el JavaScript en tu página web?

- Toggle JavaScript

### ¿Qué hace la herramienta Google Lighthouse?

- Automáticamente comprueba la calidad de las páginas web

### ¿Qué plataformas se unifican con Windows Subsystem for Linux?

- Windows y Linux

## 4. Instalando VSCode

Descarga e instala **Visual Studio Code** (VSCode), el editor de código que usaremos en el curso.

- [Visual Studio Code](https://code.visualstudio.com/)

### Atajos

- Ver mis notas: [[atajos]]

### Pasos básicos

1. Entra al sitio oficial y descarga la versión para Windows.
2. Ejecuta el instalador y sigue los pasos.
3. Al terminar, abre VSCode y verifica que funcione.

## 5. Extensiones de Visual Studio Code

Para abrir el panel de extensiones también puedes usar `Ctrl + Shift + X`.

### Extensiones recomendadas

- **Prettier - Code formatter**
- **Color Highlight**
- **Highlight Matching Tag**
- **ESLint**
- **CSS Peek**
- **Live Server**
- **Path Intellisense**
- **Auto Rename Tag**
- **Material Icon Theme**
- **Code Spell Checker**
- **WSL** 👈👀 Instalar **después** de haber instalado WSL (puntos 6 y 7).
- **Node Require**
- **Remote Development**

### ¿Para qué sirve cada una?

- **Prettier:** formatea el código automáticamente.
- **Color Highlight:** muestra el color real junto a los códigos de color (por ejemplo, `#ff0000`).
- **Highlight Matching Tag:** resalta la etiqueta de cierre que corresponde a la de apertura.
- **ESLint:** detecta errores y malas prácticas en JavaScript.
- **CSS Peek:** permite ver la definición de una clase CSS desde el HTML.
- **Live Server:** abre un servidor local que recarga la página al guardar.
- **Path Intellisense:** autocompleta rutas de archivos.
- **Auto Rename Tag:** al cambiar una etiqueta de apertura, cambia también la de cierre.
- **Material Icon Theme:** pone íconos distintos a cada tipo de archivo.
- **Code Spell Checker:** revisa la ortografía en el código.
- **WSL:** conecta VSCode con el subsistema de Linux.
- **Node Require:** ayuda a trabajar con los `require` de Node.js.
- **Remote Development:** permite trabajar en entornos remotos, contenedores o WSL.

### Cómo usar Live Server en proyectos reales de HTML y CSS

- En VSCode: clic derecho sobre el archivo HTML → **Run Live Server**.

## 6. ¿Qué es Windows Subsystem for Linux?

El **Subsistema de Windows para Linux** (*Windows Subsystem for Linux*, WSL) permite a los desarrolladores ejecutar un entorno de GNU/Linux, incluida la mayoría de herramientas de línea de comandos, utilidades y aplicaciones, directamente en Windows. Lo hace sin modificar el sistema y sin la sobrecarga de una máquina virtual tradicional o de una configuración de arranque dual.

- Fuente: [Microsoft Learn](https://learn.microsoft.com/es-es/windows/wsl/about)

### Verificar la versión de Windows 10

- Abre el **CMD** y ejecuta:

  ```bash
  winver
  ```

- Versión mínima requerida: **2004** (compilación del sistema operativo **19041.450**).

### ¿Por qué usar WSL?

- Permite usar herramientas de Linux (terminal, `apt`, `git`, `node`, etc.) sin salir de Windows.
- Evita instalar una máquina virtual o dejar Windows para usar Linux.
- Consume menos recursos que una máquina virtual (ver punto 9, VirtualBox).

## 7. Configurar Windows 11 para soportar la instalación de WSL

Entramos a la tienda de Windows (Microsoft Store) y descargamos:

- **Windows Terminal**

### Instalación de Windows Subsystem for Linux

Seguir los pasos de la documentación oficial:

- [Documentación](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

1. Abre **PowerShell** con clic derecho → **Ejecutar como administrador** 👈👀
2. Ejecuta:

   ```powershell
   wsl --install
   ```

![Powershell](https://i.postimg.cc/g2dYkFxJ/1-wsl-install.png)

> Si ejecutas PowerShell sin ser administrador, te dará el siguiente error:
> **La operación solicitada requiere elevación**

### En caso de conflictos o errores

Abre PowerShell como administrador y ejecuta:

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Después, busca **Windows Terminal** y elige **Ubuntu**. En caso de errores, busca el mensaje de error en internet.

### Reiniciar el equipo

Tras instalar WSL o habilitar la característica, conviene reiniciar el equipo antes de abrir Ubuntu.

## 8. Ubuntu en WSL

### Instalar Ubuntu desde la tienda de Microsoft

![Ubuntu](https://i.postimg.cc/jSbsdW8P/7-canonical-ubuntu.png)

Después de instalarlo, **reinicia la PC**.

![Config Ubuntu](https://i.postimg.cc/Y2ncK9V2/7-config.png)

Al abrir Ubuntu por primera vez, se crea el usuario:

- **UNIX username:** `Ubuntu`
- **Contraseña:** `Ubuntu`

### 🔥 Configuración de Ubuntu 22.04.1 LTS

Usa las flechas del teclado y luego `Enter`.

![Idioma](https://i.postimg.cc/JtwZdFyB/7-config-ubuntu-22lts.png)

Done

![Password](https://i.postimg.cc/MTFy1Hq5/7-config-ubuntu-22lts-password.png)

Done

![Montaje](https://i.postimg.cc/Y0LQR7SH/7-montaje.png)

Done

![Completed](https://i.postimg.cc/xCCvkMDq/7-completed.png)

Done

### 📌 Errores

- **Paso 01:** [Cómo habilitar el Subsistema de Windows para Linux](https://answers.microsoft.com/en-us/insider/forum/all/how-to-enable-the-windows-subsystem-for-linux/16e8f2e8-4a6a-4325-a89a-fd28c7841775)
  - **Habilitar el modo de desarrollador en Windows 10**.
  - Activar las **Características de Windows** necesarias.
  - Reiniciar.
- **Paso 02:** [Video en YouTube](https://www.youtube.com/watch?v=7P039GotVyY)
  - Error `0x80370102`: *The virtual machine could not be started because a required feature is not installed.*
  - [Solución del error 0x80370102](https://made4geek.com/error-0x80370102-the-virtual-machine-could-not-be-started-because-a-required-feature-is-not-installed-wsl-2-code-example/)

### Configuración de Ubuntu en WSL

#### Moverse por las carpetas

- `pwd`: muestra la posición actual (la ruta completa desde la raíz).
- `cd`: *change directory*. Sin argumentos, vuelve al Home.
  - `cd ..`: retrocede una posición.
  - `cd /`: va a la raíz.
  - `cd ~`: va al Home.
  - `cd /home/Ubuntu`: lleva a esa ruta.
  - `cd ../..`: retrocede dos posiciones.
  - `cd mnt`: permite cambiar de disco o partición. Desde aquí se puede entrar al disco C o D.
  - `cd d`: entra al disco D (estando dentro de `mnt`).
- `ls`: muestra el contenido de la posición actual.

#### Acceder al disco C

```bash
cd /
pwd
ls
cd mnt
ls
cd c
ls
cd Users
ls
cd usuario/Desktop
ls
```

📌 `Alt + 126` = `~`

#### Crear la carpeta de trabajo

Todos los proyectos deben estar dentro de Ubuntu.

```bash
cd ~
sudo mkdir personalProjects          # sudo otorga permisos de administrador
ls
mkdir proyectoDemoCursoPrework       # crea una carpeta
ls
touch index.html                     # crea un archivo
ls
mv index.html proyectoDemoCursoPrework   # primero el archivo a mover y luego la carpeta destino
ls
mv proyectoDemoCursoPrework personalProjects
ls
cd personalProjects
ls
cd proyectoDemoCursoPrework
code .
```

### ¿Qué hace `code .`?

Abre VSCode en la carpeta actual (el punto `.` significa "esta carpeta"). Para que funcione desde Ubuntu, VSCode y la extensión **WSL** deben estar instalados (puntos 4 y 5).

## 9. Instalación de VirtualBox

**VirtualBox** es un software de virtualización que permite instalar otros sistemas operativos dentro de Windows, como si fueran programas.

### Descargas

- [Descargar VirtualBox](https://www.virtualbox.org/wiki/Downloads): elige **Windows hosts** 👈👀
- [Descargar Ubuntu](https://releases.ubuntu.com/)

### Pasos básicos

1. Descarga e instala VirtualBox (versión **Windows hosts**).
2. Descarga la imagen ISO de Ubuntu.
3. En el siguiente punto se usa esa ISO para crear la máquina virtual.

### ¿WSL o VirtualBox?

- **WSL:** más ligero y rápido, integrado en Windows. Es la opción principal de este curso.
- **VirtualBox:** instala un sistema completo en una máquina virtual. Consume más recursos, pero es una alternativa si WSL no funciona.

## 10. Instalando Ubuntu en una máquina virtual

> Pendiente: buscar un tutorial actualizado. :3

- Ver mi nota de Obsidian: [[1-virtual-box#Instalación]]

### Pasos generales (complemento)

1. Abre **VirtualBox** y crea una nueva máquina virtual.
2. Selecciona la imagen ISO de Ubuntu descargada en el punto anterior.
3. Asigna memoria RAM y espacio en disco a la máquina virtual.
4. Inicia la máquina e instala Ubuntu siguiendo el asistente.

## 11. Comandos básicos de la terminal

### Abrir el proyecto desde Ubuntu

Abre la terminal de Ubuntu y ejecuta:

```bash
cd ~
ls
cd personalProjects
ls
cd proyectoDemoCursoPrework
ls
code .
```

Haz algunos cambios en el HTML y activa el servidor con clic derecho → **Run Live Server**.

### Ver el contenido de un archivo

```bash
cat index.html    # muestra el contenido del archivo
man cat           # abre el manual de uso de cat
```

- Presiona `q` para salir del manual.

### Volver al Home

```bash
cd ~
```

### Resumen de comandos (complemento)

| Comando  | Para qué sirve |
|----------|---|
| `cd`    | Cambia de carpeta |
| `ls`    | Lista el contenido de la carpeta actual |
| `code .`| Abre VSCode en la carpeta actual |
| `cat`   | Muestra el contenido de un archivo |
| `man`   | Muestra el manual de un comando |
| `q`     | Sale del manual |

## 12. Instalación de Node

### Actualizar los paquetes de Ubuntu

```bash
sudo apt-get update      # actualiza la lista de paquetes (pide la contraseña y carga)
sudo apt-get update      # se repite para asegurar que cargue completo
sudo apt-get upgrade     # aplica las actualizaciones
```

- `apt-get` es el gestor de paquetes que usamos para instalar programas.
- Cuando pregunte si deseas continuar, escribe `y`.

### Instalar Node.js y npm

```bash
sudo apt install nodejs   # escribe y cuando lo pida
node -v                   # verifica la versión instalada
sudo apt install npm      # escribe y cuando lo pida
```

### Actualizar Node.js

```bash
sudo npm install -g n
sudo n latest
reset
```

### Cómo configurar tu primer proyecto en React.js

```bash
clear                             # limpia la terminal
cd personalProjects
ls
npx create-react-app test         # instala los archivos y elimina el instalador
cd test
npm start
```

1. Abre **otra terminal**. Para detener el servidor en ejecución, usa `Ctrl + C`.
2. Ejecuta `code .` para abrir VSCode en la carpeta.
3. Entra a `src` → `App.js`, edita el archivo y guarda con `Ctrl + S`.
4. Vuelve a encender el servidor. Dentro de VSCode: **Terminal** → **New Terminal** y ejecuta:

   ```bash
   npm start
   ```

### Si hay un error de permisos en la terminal de Linux

```bash
sudo chown -R ubuntu ~/personalProjects
```

### ¿Qué es `chown`?

Cambia el propietario de una carpeta. Aquí devuelve al usuario `ubuntu` el control de `personalProjects`, que se creó con `sudo` (punto 8) y por eso pertenecía a root.

## 13. Instalación de Python

### Instalar Python

```bash
sudo apt install software-properties-common     # herramientas para gestionar repositorios
sudo add-apt-repository ppa:deadsnakes/ppa      # agrega el repositorio con versiones de Python
sudo apt update                                 # actualiza la lista de paquetes
sudo apt install python3.8                      # instala Python 3.8
python3 --version                               # verifica la versión instalada
clear                                           # limpia la terminal
```

### Probar Python en la terminal

Abre el intérprete de Python:

```bash
python3
```

Dentro del intérprete escribe:

```python
num1 = 1.99
num2 = 2.01
suma = num1 + num2
print('El resultado: {0} y {1}: {2} '.format(num1, num2, suma))
```

Resultado esperado:

```text
El resultado: 1.99 y 2.01: 4.0
```

### Salir del intérprete (complemento)

Para volver a la terminal de Ubuntu, escribe `exit()` o presiona `Ctrl + D`.

### ¿Qué hace `.format()`? (complemento)

Reemplaza los marcadores `{0}`, `{1}` y `{2}` por los valores que se le pasan, en orden: `num1`, `num2` y `suma`.

## Quiz

### ¿Qué se usa para instalar Ubuntu sin problemas?

- Windows Subsystem for Linux

### ¿Qué hace el comando `dism.exe /online /enable-feature -- featurename: virtual machine platform con la opción all no-restart`?

- Habilita la plataforma de Windows para máquinas virtuales

## 14. Instalando Git

> Para borrar necesitas estar en la ubicación exacta del archivo o carpeta.

### Borrar archivos y carpetas

Borrar un archivo:

```bash
rm nombreArchivo.extension
```

Borrar una carpeta vacía:

```bash
rm -d nombreCarpetaVacia
```

Borrar un directorio con contenido:

```bash
cd ..
rm -rf test
ls
```

Si revisamos VSCode, la carpeta ya no estará. El siguiente paso es cerrarla:

- **File** → **Close Folder**

### 🔥 Instalar Git

Verifica si ya está instalado:

```bash
cd ..
clear
git --version
```

En caso de no tenerlo instalado:

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt install git
```

También se puede instalar el paquete completo:

```bash
sudo apt-get install git-all
```

- Ver mis notas de Obsidian sobre la instalación: [[git-github#5. Instalando Git en Linux]]

### Crear una cuenta en GitHub

- [GitHub](https://github.com/)

### ¿Qué hace `rm -rf`? (complemento)

- `-r`: borra de forma recursiva (la carpeta y todo su contenido).
- `-f`: fuerza el borrado sin pedir confirmación.
- **Úsalo con cuidado:** lo borrado no va a la papelera y no se puede recuperar.

## 15. Vinculando nuestra llave SSH en GitHub

Una llave SSH permite conectarte a GitHub sin escribir tu usuario y contraseña cada vez.

- Ver mis notas: [[git-github#22. Conexión a GitHub con SSH]]

### Forma actual (recomendada): ed25519

El correo que uses al crear la llave debe ser el mismo con el que creaste tu cuenta en GitHub.

```bash
# 1. Generar la llave
ssh-keygen -t ed25519 -C "tu_correo@ejemplo.com"
# Enter para aceptar la ubicación por defecto
# passphrase: opcional, puedes dar Enter si no quieres usar una

# 2. Iniciar el agente SSH
eval "$(ssh-agent -s)"

# 3. Agregar la llave al agente
ssh-add ~/.ssh/id_ed25519
# Enter passphrase: si no creaste una, solo dale Enter

# 4. Mostrar la llave pública para copiarla
cat ~/.ssh/id_ed25519.pub
```

La llave pública se ve así (es solo un ejemplo):

```text
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIExampleKeyExampleKeyExampleKeyExample tu_correo@ejemplo.com
```

### Agregar la llave en GitHub

1. Entra a tu avatar o foto de cuenta → **Settings**.
2. **SSH and GPG keys** → **New SSH key**.
3. **Title:** un nombre para identificarla (por ejemplo, `Llave WSL`).
4. **Key:** pega la llave pública completa (el resultado de `cat`).
5. Haz clic en **Add SSH key**.

### Probar la conexión

```bash
ssh -T git@github.com
```

La primera vez pregunta si confías en el servidor: escribe `yes`. Si todo salió bien, GitHub responde con un mensaje de bienvenida con tu usuario.

### Forma anterior del curso: RSA

```bash
ssh-keygen -t rsa -b 4096 -C "tu_correo@ejemplo.com"
# Enter
# Contraseña (passphrase)
eval "$(ssh-agent -s)"     # muestra que el agente está corriendo
clear
cd ~/.ssh
ls
cat id_rsa.pub             # copia la llave pública
```

- Se agrega en GitHub igual que arriba (**Settings** → **SSH and GPG keys** → **New SSH key**), con el título `Llave curso Prework`.
- En mi caso no me pidió contraseña :v
- Usa RSA solo si tu sistema no soporta ed25519.

### Qué es cada archivo

- `id_ed25519`: llave **privada**. Nunca se comparte.
- `id_ed25519.pub`: llave **pública**. Es la que se pega en GitHub.

## 16. Subir tu primer repositorio

### Ubicar el proyecto

En la terminal, busca el proyecto:

```bash
ls
cd personalProjects
ls
```

### Configurar Git 👈👀

```bash
git config --global user.email "tu_correo@ejemplo.com"
git config --global user.name "Tu Nombre"
git config --edit --global     # abre el archivo de configuración para revisarlo
```

- El correo debe ser el mismo de tu cuenta de GitHub.

### Crear el repositorio local

```bash
git init
git add .
git commit -m "first commit"
clear
```

### Crear el repositorio en GitHub

1. **Repositories** → **New**.
2. **Repository name:** `MyWeb`.
3. **Description:** Repositorio para pruebas de configuración SSH.
4. Elige **Public**.
5. Haz clic en **Create repository**.

### Conectar y subir

```bash
# Crear la conexión remota (usa la URL SSH que te da GitHub)
git remote add origin git@github.com:tu-usuario/MyWeb.git
git remote -v

# Revisar si tu rama se llama main o master
git branch

# Subir los cambios
git push origin master     # o main, según el nombre de tu rama
```

### Enviar nuevos cambios

Haz pequeños cambios en el HTML y envíalos a GitHub:

```bash
git status
git add .
git commit -m "Nuevo cambio"
git push origin master     # o main
```

Actualiza GitHub y revisa los cambios:

- Entra en `index.html`.
- Verás dos commits.

- Ver mi resumen de Git y GitHub: [[git-github#19. Uso de GitHub]]

### Rama main vs. master

- Git y GitHub usan hoy **`main`** como nombre de la rama principal por defecto; antes era `master`.
- Para renombrar tu rama local a `main`:

  ```bash
  git branch -M main
  ```

- Con `-u` en el primer push, Git recuerda la rama y después basta escribir `git push`:

  ```bash
  git push -u origin main
  ```

### Qué hace cada comando (complemento)

| Comando | Para qué sirve |
|---|---|
| `git init` | Crea un repositorio de Git en la carpeta |
| `git add .` | Prepara todos los archivos para el commit |
| `git commit -m "..."` | Guarda los cambios con un mensaje |
| `git remote add origin ...` | Conecta tu repositorio local con GitHub |
| `git remote -v` | Muestra las conexiones remotas |
| `git push` | Envía los commits a GitHub |
| `git status` | Muestra los archivos modificados |

## Quiz

### ¿Cómo se agregarán todos los archivos al repositorio?

- `git add .`

### ¿Cuál es el primer comando para iniciar un repositorio de GitHub?

- `git init`

### ¿Qué comando agrega todos los archivos al repositorio?

- `git add`

### ¿Cómo inicializamos nuestro primer repositorio de GitHub?

- Hacemos `git init`

## 17. PowerToys

**PowerToys** es un conjunto de utilidades gratuitas de Microsoft para Windows que mejoran la experiencia de uso y aumentan la productividad.

- [PowerToys (documentación de Microsoft)](https://learn.microsoft.com/en-us/windows/powertoys/)

### Instalación

También se puede descargar desde la tienda de Windows (Microsoft Store).

### Otras formas de instalarlo (actualizado)

- **GitHub:** descargando el instalador desde la página de *releases* del proyecto.
- **WinGet** (desde PowerShell o la terminal):

  ```powershell
  winget install --id Microsoft.PowerToys --source winget
  ```

### FancyZones

Una de las utilidades más usadas. Permite dividir la pantalla en **zonas** (*layouts*) y acomodar las ventanas en ellas.

- Abrir el editor de layouts: `Win + Shift + `` ` `` (tecla de acento grave o *backtick*). Este atajo se puede cambiar en la configuración de PowerToys.
- Tipos de layout: **Grid** (cuadrícula, que se divide y se une) y **Canvas** (zonas que pueden superponerse).
- También puedes abrir el editor desde PowerToys → **FancyZones** → **Open layout editor**.

### Otras utilidades útiles (complemento)

| Utilidad       | Atajo              | Para qué sirve |
|----------------|--------------------|----------------|
| Color Picker   | `Win + Shift + C` | Elegir un color de cualquier parte de la pantalla y copiarlo |
| Text Extractor | `Win + Shift + T` | Copiar texto de cualquier parte de la pantalla |
| Always On Top  | `Win + Ctrl + T`  | Fijar una ventana por encima de las demás |
| Shortcut Guide | `Win + Shift + /` | Mostrar los atajos disponibles |

## Quiz

### ¿Cuál de las siguientes opciones no es una forma de layout?

- Esquema

### ¿Qué características podemos añadir en Fancy Zones?

- Prioridad y cuadrícula

### ¿Qué combinación de teclas nos permite abrir el Editor de Fancy Zones?

- Win + Shift + Ñ

### ¿Cuál es uno de los parámetros para ajustar las zonas de apresamiento de Fancy Zones?

- Margen

### ¿Cómo se llama el conjunto de utilidades que podemos instalar en Windows para mejorar nuestra experiencia y aumentar nuestra productividad?

- PowerToys

## Examen 📌

<details>
	<summary>Haz clic para ver los resultados 👀</summary>
	<br/>

1. ¿Qué es Ubuntu?

	- 📌 Una distribución Linux, es de las más usadas, tiene una terminal potente y fácil de comenzar a utilizar

2. ¿Por qué la virtualización puede ser más lenta que soluciones integradas como WSL2?

	- 📌 Debido a que al virtualizar estamos reservando recursos para que sean ejecutados por la máquina virtual y además estamos corriendo el software encargado de la virtualización misma, esto puede ser intensivo de RAM, disco duro, y procesador

3. ¿Cuáles son algunos de los principales usos de Python?

	- 📌 Desarrollo backend, Data Science, IA, entre otros

4. ¿Qué es GitHub?

	- 📌 Un sitio web creado para que diferentes desarrolladoras y equipos de trabajo puedan subir sus repositorios de Git y manejar de forma eficiente y colaborativa, en la nube su proceso de desarrollo

5. ¿Qué es VSCode?

	- 📌 Visual Studio Code (VS Code) es un editor de código fuente desarrollado por Microsoft, es código abierto, y es multiplataforma, además es el que usarás en el resto de cursos de desarrollo web

6. ¿Por qué es importante saber utilizar Git?

	- 📌 Porque es el sistema de control de versiones usado por de facto en la industria tech, nos permite al usarlo con un sitio como Github o similares colaborar y trabajar en equipo

7. ¿Quíén fue el creador de Git?

	- 📌 Linus Torvalds, el mismo creador de Linux

8. ¿Qué es una terminal?

	- 📌 Un software que nos permite interactuar directamente con nuestra computadora a través de comandos y texto, tal como lo hacemos tradicionalmente a través de ventanas, íconos, menús y botones en Windows

9. ¿Para qué nos sirve utilizar WSL2?

	- 📌 WSL2 nos permite tomar todas las grandes ventajas y facilidades que siempre han existido de desarrollar en Linux, como sus terminales, sin tener que acostumbrarnos a un Sistema Operativo distinto a que usamos día a día, quizás tienes videollamadas, y en Ubuntu por ejemplo puede ser difícil compartir audio, video, etc. Así que esta fue la forma de Microsoft de ser un sistema útil para desarrollar software que tradicionalmente se hacía en Linux dando la practicidad de Windows

9. Node.js es:

	- 📌 Un intérprete de JavaScript, que nos permitirá ejecutar JavaScript en nuestra terminal y no solo en el navegador, se utiliza principalmente para servidores

11. ¿Qué es Virtual Box?

	- 📌 Un software de virtualización que nos permitirá instalar distintos sistemas operativos virtualizando el entorno en el que estamos, compartiendo recursos con la máquina host

12. ¿Por qué razón utilizamos Google Chrome?

	- 📌 Por ser el navegador más utilizado, es importante visualizar nuestros proyectos web como los verán la gran mayoría de usuarios

13. ¿Qué es WSL2?

	- 📌 Windows Subsystem for Linux2, un subsistema en Windows que ejecuta el kernel completo de Linux, permitiéndonos ejecutar cualquier distribución de Linux que necesitamos directamente en Windows

14. ¿Para qué nos sirven las DevTools?

	- 📌 Para facilitar el desarrollo de nuestros proyectos web, buscar y corregir errores, entender el rendimiento de nuestro sitio

15. ¿Qué es Git?

	- 📌 Git es un sistema de control de versiones y manejo de repositorios, nos permite manejar el progreso en el desarrollo de nuestro software, probar cosas nuevas, regresar a versiones anteriores, y demás
</details>
