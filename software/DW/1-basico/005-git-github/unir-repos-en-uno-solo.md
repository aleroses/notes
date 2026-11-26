# Guía: unir dos repositorios Git en uno solo conservando el historial

Registro personal, 25 de noviembre de 2026. Caso real: `English` + `software-notes` → `notes`.

## 1. Objetivo y contexto

Partía de **dos repositorios independientes**, cada uno con su propia carpeta local y su propio repo en GitHub:

| Carpeta local           | Repo remoto                                   |
| ----------------------- | --------------------------------------------- |
| `~/Documents/English`  | `git@github.com:aleroses/English.git`        |
| `~/Documents/software` | `git@github.com:aleroses/software-notes.git` |

Quería terminar con **un solo repositorio** llamado `notes`, tanto en local como en GitHub, con esta forma:

```bash
notes/
├── english/
└── software/
```

Requisito adicional: **conservar el historial de commits de ambos repos** (no solo copiar archivos).

Datos del entorno: Linux, shell zsh, autenticación a GitHub por SSH, rama principal `master` en ambos repos (no `main`).

## 2. Conceptos previos

### ¿Qué es `git subtree`?

`git subtree` es un comando incluido en Git que permite **traer otro repositorio dentro de una subcarpeta del repo actual**, con todos sus commits. Después de hacerlo, el resultado es **un solo repo normal**: no queda ninguna relación con el repo de origen, no hay archivos extra de configuración ni nada que mantener.

### Por qué no simplemente copiar y pegar la carpeta

Si copias `English/` dentro de `software/` con `cp -r`, aparecería la carpeta `English/.git` (un repo dentro de otro). Git lo trata como un repo anidado y **no versiona sus archivos**: en GitHub aparecería como una carpeta vacía. Hay que borrar ese `.git` y entonces pierdes todo el historial.

### Alternativas que existen (y por qué no las usé)

- **Copiar sin historial**: borrar `English/.git`, copiar la carpeta y hacer un commit. Es lo más simple, pero se pierden los 396 commits.
- **Submódulos (`git submodule`)**: mantienen los repos separados y enlazados. No era lo que quería (yo quería uno solo) y añaden complejidad.
- **`git merge --allow-unrelated-histories`**: también conserva historial, pero mezcla los archivos de ambos repos en la raíz. Si los dos tienen un `README.md` o un `.gitignore` en la raíz, hay conflictos. Por eso hay que mover antes todo a una subcarpeta.
- **`git filter-repo`**: herramienta externa más potente (reescribe el historial). Es excesiva para este caso.

Elegí `git subtree add` porque es simple, viene con Git y conserva el historial.

## 3. Estado inicial

```bash
Documents
├── English
│   ├── Anki/ InUse/ Listening/ Others/ 
│   ├── LICENSE
│   ├── README.md
│   └── PachoOchoa
└── software
    ├── DMP
    ├── DW
    ├── others
    ├── projects
    └── README.md
```

Comprobación de los remotos de cada repo (se ejecuta dentro de cada carpeta):

```bash
git remote -v
```

## 4. Paso 0: respaldo y comprobaciones previas

Nunca hagas esto sin respaldo. Una operación mal hecha en Git suele poder deshacerse, pero la copia es gratis y evita sustos.

```bash
cd ~/Documents
cp -r English English.bak
cp -r software software.bak
```

En **cada repo**, comprueba el estado y apunta el nombre de la rama:

```bash
cd ~/Documents/English
git status        # debe decir "nothing to commit, working tree clean"
git branch        # anota si es main o master

cd ~/Documents/software
git status
git branch
```

Si hay cambios pendientes, haz `git add -A`, `git commit` y `git push` **antes** de seguir. Si hay archivos sin trackear que quieres conservar (por ejemplo `.obsidian/`), anótalos: hay que moverlos a mano en el paso 2.

Comprueba también que `git subtree` está disponible:

```bash
git subtree --help
```

Si no existe, instálalo desde el paquete de Git de tu distribución (en la mayoría de instalaciones ya viene incluido).

## 5. Paso 1: renombrar el repo en GitHub

El repo que usé como base fue `software-notes`, y lo renombré a `notes`.

1. En GitHub abre el repo → **Settings** → **General** → campo **Repository name** → escribe `notes` → **Rename**.
2. GitHub crea una redirección automática desde la URL antigua, pero conviene actualizar el remoto local para no depender de ella:

```bash
cd ~/Documents/software
git remote set-url origin git@github.com:aleroses/notes.git
git remote -v     # verifica que fetch y push apuntan a notes.git
```

Nota: el renombrado en GitHub no cambia nada del contenido ni del historial.

## 6. Paso 2: mover el contenido del repo base a una subcarpeta

Si importara `English` directamente a la raíz, sus archivos (`README.md`, `.gitignore`, `LICENSE`) chocarían con los del otro repo. La solución es que **cada repo viva en su propia subcarpeta**. El repo base (`software`) debe quitarse de la raíz y moverse a `software/software/`:

```bash
cd ~/Documents/software
mkdir software
git ls-tree --name-only HEAD | grep -vx software | xargs -d '\n' -I{} git mv {} software/
git commit -m "Move software notes into software/ subfolder"
```

Qué hace cada parte:

- `mkdir software`: crea la subcarpeta destino.
- `git ls-tree --name-only HEAD`: lista todo lo que está **versionado** en la raíz (incluye archivos ocultos versionados como `.gitignore`).
- `grep -vx software`: excluye la carpeta `software` recién creada para no intentar moverla dentro de sí misma.
- `xargs -d '\n' -I{} git mv {} software/`: ejecuta `git mv` por cada elemento, respetando nombres con espacios.
- `git mv` mueve y registra el cambio en un solo paso.

La salida del commit mostró muchas líneas como `rename {DW => software/DW}/... (100%)`. Eso es lo esperado: Git detecta que son movimientos, no borrados y creaciones, y el `(100%)` indica que el contenido no cambió, así que el historial de cada archivo se conserva.

Puntos de atención:

- **`xargs -d` es de GNU/Linux.** En macOS el `xargs` de BSD no tiene la opción `-d`; ahí usa otra forma, por ejemplo un bucle `for`.
- **Lo que no está versionado no se mueve.** `git ls-tree` solo ve lo trackeado. Carpetas sin trackear (como `.obsidian/` o archivos ignorados por `.gitignore`) se quedan en la raíz. Muévelas con `mv` normal y revisa con `git status`.
- La carpeta local también se llamaba `software`, así que durante un rato existía `software/software/`. No es un error, solo confunde. Se arregla en el paso 5.

## 7. Paso 3: importar el segundo repo con `git subtree add`

```bash
git subtree add --prefix=English ../English master
```

Significado:

- `--prefix=English`: carpeta de destino dentro del repo. Se crea sola y no debe existir antes.
- `../English`: ruta del repo de origen (relativa a donde estás). También puede ser una URL, por ejemplo `git@github.com:aleroses/English.git`.
- `master`: rama del repo de origen que quieres traer.

### Error que me salió: rama incorrecta

Primero ejecuté el comando con `main` y falló:

```bash
fatal: couldn't find remote ref main
```

Causa: el repo `English` usa la rama `master`, no `main`. Solución: verificar con `git branch` en el repo de origen y usar el nombre correcto.

### Resultado correcto

```
From ../English
 * branch   master -> FETCH_HEAD
Added dir 'English'
```

`git subtree add` hace dos cosas: descarga todos los commits del otro repo y crea un **commit de merge** que coloca su contenido en `English/`. Mi historial quedó así (los números se ven en `git status` como "ahead by 397 commits"):

```
b40e3605 Add 'English/' from commit '3333cb35...'
9661a513 Move software notes into software/ subfolder
320a6036 add gh-cli
...
```

Opción `--squash`: si prefieres no traer todos los commits y quedarte con uno solo, añade `--squash`. Yo no la usé porque quería conservar el historial completo.

## 8. El problema que me pasó: renombrar una carpeta de `English` a `english`

Después del `subtree add`, renombré la carpeta con el comando normal del sistema:

```bash
mv English english
```

Sin hacer nada más en Git, `git status` mostró algo alarmante:

```
Changes not staged for commit:
        deleted:    English/.gitignore
        deleted:    English/Anki/Scraping/mined.js
        ... (cientos de líneas)

Untracked files:
        english/
```

### Por qué pasa

Git guarda en su índice las rutas **exactas** de cada archivo, incluidas las mayúsculas. Para Git, `English/Anki/...` y `english/Anki/...` son **rutas distintas**. Al renombrar la carpeta fuera de Git:

- Las rutas `English/...` dejan de existir en disco → Git las ve como **borradas**.
- La carpeta `english/` es nueva → Git la ve como **sin trackear**.

No se perdió nada: los archivos siguen ahí, solo cambió el nombre. Git simplemente aún no lo sabe.

### Dos formas de resolverlo

**Opción A: deshacer el cambio de nombre**

```bash
mv english English
git status      # queda limpio
```

**Opción B (la que elegí): confirmar el cambio de nombre en Git**

```bash
git add -A
git status      # debe mostrar "renamed: English/... -> english/..."
git commit -m "Rename English to english"
```

Antes de hacer el commit revisa que `git status` muestre `renamed:` y no un montón de `deleted:` y `new file:`. Git detecta los renames comparando contenido, así que con archivos sin modificar aparecen como renames sin problema.

### La forma correcta de hacerlo desde el principio

Cuando renombras algo versionado, hazlo con Git:

```bash
git mv English english
git commit -m "Rename English to english"
```

### Si el sistema de archivos no distingue mayúsculas (Windows, macOS por defecto)

En esos sistemas `English` y `english` son la misma carpeta, y un `git mv English english` directo puede fallar o no registrar el cambio. Se hace en dos pasos con un nombre intermedio:

```bash
git mv English english-tmp
git mv english-tmp english
git commit -m "Rename English to english"
```

En Linux (mi caso) el sistema sí distingue mayúsculas y funciona directo.

## 9. Paso 4: verificar y subir a GitHub

Antes de subir, comprobé que todo estuviera donde debía:

```bash
git status               # nothing to commit, working tree clean
git remote -v            # origin apunta a git@github.com:aleroses/notes.git
ls -a english            # confirma que existen .gitignore, LICENSE, README.md y las carpetas
tree -L 3                # revisa la estructura completa
git log --oneline | head # revisa los últimos commits
```

Luego el push (la rama era `master`):

```bash
git push origin master
```

Salida: `Writing objects: 100% (2506/2506), 119.84 MiB` y `320a6036..f1eec325 master -> master`. Se subieron los commits de ambos repos (unos 119 MB). Después de eso `git status` dijo `Your branch is up to date with 'origin/master'`.

No hizo falta `--force`. Si alguna vez Git te rechaza el push, **no uses force a ciegas**: revisa primero con `git fetch` y `git log origin/master`.

## 10. Paso 5: renombrar la carpeta local y limpiar

La carpeta raíz del repo seguía llamándose `software`. Renombrarla no afecta a Git porque Git no guarda el nombre de la carpeta contenedora:

```bash
cd ~/Documents
mv software notes
cd notes
git status      # sigue limpio
```

Cuando confirmes en GitHub que `notes` muestra ambas carpetas y el historial completo, limpia:

```bash
cd ~/Documents
rm -rf English English.bak software.bak
```

Y en GitHub, en el repo viejo `English`: **Settings** → **Danger Zone** → **Archive this repository** (queda de solo lectura y se puede recuperar) o **Delete** (irreversible). Mi recomendación: archivar primero y borrar más adelante.

## 11. Cómo se trabaja ahora con Git

No cambia nada. Es **un único repositorio normal**:

- Un solo `.git` en la raíz (`notes/.git`).
- Un solo `git add`, `git commit` y `git push` para todo.
- `english/` y `software/` son simples carpetas, no repos independientes.
- No existe ningún vínculo con los repos originales; no hay que actualizar nada con `git subtree pull`.

Para ver el historial de una carpeta concreta:

```bash
git log -- english/
git log -- software/
```

Para seguir el historial de un archivo a través de renames:

```bash
git log --follow -- english/README.md
```

Limitación a conocer: el historial anterior a la migración de los archivos de `software/` aparece bajo las rutas antiguas (en la raíz). `git log --follow` por archivo lo resuelve; el `git log -- software/` de carpeta solo mostrará lo posterior al movimiento y el commit de movimiento.

## 12. Cosas que pueden romperse (y cómo evitarlas)

### Errores al ejecutar los comandos

- **`fatal: couldn't find remote ref main`**: la rama se llama `master` (o al revés). Verifica con `git branch` en el repo de origen.
- **`Working tree has modifications. Cannot add.`**: `git subtree add` exige un árbol de trabajo limpio. Haz commit o `git stash` antes.
- **`prefix 'English' already exists.`**: la carpeta destino ya existe en el repo. Elige otro nombre de prefijo o elimina/mueve esa carpeta antes.
- **`git: 'subtree' is not a git command`**: tu instalación de Git no incluye subtree. Instálalo desde el paquete de tu distribución.
- **`xargs: invalid option -- 'd'`**: estás en macOS (xargs BSD). Usa un bucle `for` en su lugar.
- **Push rechazado (`non-fast-forward`)**: el remoto tiene commits que no tienes. Haz `git fetch` y revisa; no fuerces el push sin entender por qué.
- **Push rechazado por archivos grandes**: GitHub bloquea archivos de más de 100 MB. Mi push de unos 119 MB pasó porque eran muchos archivos pequeños, pero un solo archivo grande lo bloquearía. Si pasa, hay que sacarlo del historial (con `git filter-repo`) o usar Git LFS.

### Problemas de nombres y rutas

- **Renombrar con `mv` en vez de `git mv`**: Git ve borrados + archivos nuevos hasta que haces `git add -A`. Es lo que me pasó. No pierdes datos, pero asusta.
- **Cambiar solo mayúsculas/minúsculas**: en Windows y macOS puede no detectarse el cambio; usa el truco de dos pasos con nombre temporal.
- **Nombres con espacios o tildes** (`Curso de Introducción a Java SE`): funcionan, pero rompen scripts mal escritos y producen URLs con `%20`. Ya los tengo, conviene normalizarlos más adelante.
- **Dos archivos con el mismo nombre en la raíz** (`README.md`, `.gitignore`, `LICENSE`) al unir repos sin subcarpetas: conflicto de merge. Por eso se mueve todo a subcarpetas primero.
- **Archivos sin trackear o ignorados** (`.obsidian/`, `node_modules/`, `.env`): no se mueven con `git mv`. Revísalos con `git status --ignored` y muévelos a mano.
- **`.gitignore` anidado**: el `.gitignore` de English ahora vive en `english/.gitignore` y solo afecta a esa carpeta. Si querías reglas globales, crea un `.gitignore` en la raíz.

### Problemas de contenido

- **Enlaces internos entre notas** (Obsidian, enlaces relativos en Markdown, imágenes `![](ruta)`): si mueves o renombras carpetas, pueden romperse. Obsidian los actualiza solo si renombras desde la app, no desde la terminal. Tras un cambio grande, haz una búsqueda de rutas antiguas, por ejemplo `grep -r "DW/" .`.
- **Repos dentro de repos**: si alguna subcarpeta tenía su propio `.git` (por ejemplo un proyecto clonado), Git la trata como repo anidado y no sube sus archivos. Comprueba con `find . -name .git -maxdepth 4`.
- **Scripts con rutas absolutas o relativas** (por ejemplo los `.py` de `english/Listening`): si usan rutas calculadas desde la raíz del repo, hay que actualizarlas.
- **LICENSE y README**: tras la unión hay dos README y una LICENSE que solo cubre una parte. Decide si quieres una licencia global en la raíz.

### Problemas relacionados con GitHub y otros equipos

- **Clones antiguos en otras máquinas**: siguen apuntando al nombre viejo. La redirección de GitHub los hace funcionar un tiempo, pero lo correcto es `git remote set-url origin <nueva-url>`.
- **La redirección de un repo renombrado se pierde** si más tarde creas un repo nuevo con el nombre antiguo (`software-notes`). No lo hagas.
- **Stars, issues, forks y wiki** del repo viejo no se transfieren al importar con subtree. En mi caso el repo base fue el renombrado, así que conservó los suyos; los de `English` quedan en ese repo archivado.
- **GitHub Actions, GitHub Pages, webhooks, integraciones**: dependen del nombre del repo. Revisa la configuración tras renombrar.
- **Tags y ramas** del repo importado no se traen con `subtree add` (solo la rama indicada). Si el repo de origen tenía tags o ramas importantes, no se migran.
- **Borrar el repo `English` antes de verificar**: si lo borras y luego detectas que faltaba algo, solo te queda el respaldo local. Archiva primero.

## 13. Cómo deshacer si algo sale mal

Antes de hacer push (todo es local y reversible):

```bash
git log --oneline | head      # localiza el commit anterior a la operación
git reset --hard origin/master  # vuelve al estado del remoto, descarta commits locales
```

Advertencia: `git reset --hard` descarta cambios sin commitear y commits locales no subidos. Usa antes `git status` y asegúrate de tener el respaldo.

Si te equivocaste de commit al hacer reset, `git reflog` muestra el historial de movimientos de HEAD y permite volver a cualquier estado reciente (`git reset --hard <hash>`).

Si todo salió mal, borra la carpeta y restaura el respaldo: `rm -rf software && cp -r software.bak software`.

Después del push, no reescribas historia publicada salvo que sepas exactamente lo que haces; lo seguro es corregir con un commit nuevo.

## 14. Resumen: todos los comandos en orden

```bash
# 0. Respaldo y comprobaciones
cd ~/Documents
cp -r English English.bak
cp -r software software.bak
cd English  && git status && git branch
cd ../software && git status && git branch
git subtree --help

# 1. Renombrar el repo en GitHub (desde la web) y actualizar el remoto
cd ~/Documents/software
git remote set-url origin git@github.com:aleroses/notes.git
git remote -v

# 2. Mover el contenido del repo base a una subcarpeta
mkdir software
git ls-tree --name-only HEAD | grep -vx software | xargs -d '\n' -I{} git mv {} software/
git commit -m "Move software notes into software/ subfolder"

# 3. Importar el segundo repo (rama correcta: master o main)
git subtree add --prefix=English ../English master

# 4. (Opcional) renombrar carpeta usando Git
git mv English english
git commit -m "Rename English to english"

# 5. Verificar y subir
git status
git remote -v
tree -L 3
git log --oneline | head
git push origin master

# 6. Renombrar la carpeta local y limpiar
cd ~/Documents
mv software notes
rm -rf English English.bak software.bak   # solo tras verificar en GitHub
```

Finalmente, en GitHub: archivar (o borrar) el repo viejo `English`.

## 15. Checklist final

- [ ] Respaldos creados antes de empezar.
- [ ] Ambos repos sin cambios pendientes y con push hecho.
- [ ] Nombre de la rama de cada repo comprobado (main o master).
- [ ] Repo base renombrado en GitHub y `git remote set-url` ejecutado.
- [ ] Contenido del repo base movido a subcarpeta y commit hecho.
- [ ] `git subtree add` ejecutado con la rama correcta.
- [ ] Renames hechos con `git mv` (o confirmados con `git add -A`).
- [ ] `git status` limpio y estructura revisada con `tree`.
- [ ] Push realizado y verificado en la web de GitHub (carpetas e historial).
- [ ] Carpeta local renombrada a `notes`.
- [ ] Repo viejo archivado en GitHub; respaldos locales borrados solo después de verificar.
- [ ] Pendiente: README raíz, licencia global y normalizar nombres de carpetas.
