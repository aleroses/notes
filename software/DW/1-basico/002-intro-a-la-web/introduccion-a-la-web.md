# Curso de Introducción a la Web: Historia y Funcionamiento de Internet

~~Diego De Granda~~

## 1. Bienvenida al desarrollo web


## 2. ¿Cómo empezó todo?

Los problemas que se intentaban resolver con las máquinas y computadoras eran de **cálculo**.

### Primeras herramientas de cálculo

- El **ábaco** es considerado la primera computadora. Su uso consiste en conteos decimales.
- Después aparecieron las **máquinas mecánicas no eléctricas**, que ayudaban a hacer cálculos de mayor complejidad.
- Luego aparecieron las **computadoras humanas**: personas encargadas de realizar los cálculos manualmente.

### Máquinas programables

- En los años 40 aparecieron las **máquinas que se podían programar**. Estuvieron muy presentes durante la guerra, pero existía el problema de la falta de almacenamiento de datos.
- Para resolverlo aparecieron las **tarjetas perforadas**, cuya función principal era guardar información.

### Machine Code y lenguajes de programación

- Posteriormente, nació el **Machine Code** (lenguaje de máquina), que realiza los cálculos utilizando el sistema binario.
- Esto presentaba un gran nivel de dificultad, así que nacieron los **lenguajes de programación**.
- Entre los primeros lenguajes se encontraban Fortran, Cobol, Basic, C, Pascal y C++.
- El Machine Code es considerado un **lenguaje de bajo nivel**.

### Enlaces

- [Historia de los lenguajes de programación](https://es.wikipedia.org/wiki/Historia_de_los_lenguajes_de_programaci%C3%B3n)
- [Historia programación](https://platzi.com/cursos/historia-programacion/)

## 3. Inputs y outputs

La interacción que tenemos con las computadoras se da a través de **entradas y salidas**.

**Entrada (input) → Proceso → Salida (output)**

- **Entrada o input:** es la información que ingresamos a la computadora. Se puede ingresar a través de dispositivos de entrada como escáner, micrófono, webcam, mouse, teclado, etc.
- **Proceso:** son los cálculos que realiza la computadora tomando como base la información ingresada.
- **Salida u output:** es la información que devuelve la computadora. Se puede visualizar a través de dispositivos de salida como impresora, proyector, parlante, monitor, etc.

Todo lo que la computadora hace son cálculos de alto nivel.

## 4. Binario

**Machine Code** es un lenguaje binario. El sistema binario es básicamente un sistema de conteo, y la computadora solo entiende ceros y unos.

### Método 1: De decimal a binario con las potencias de 2

Para convertir un número decimal a binario, utilizamos como referencia las potencias de 2:

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|-----|----|----|----|---|---|---|---|

Primero escribimos los valores desde `128` hasta `1`. Luego comenzamos desde el número más grande y vamos comprobando si podemos restarlo al número que tenemos: si cabe, colocamos `1` y seguimos con el resto; si no, colocamos `0`.

#### Ejemplo 1: número 70 a binario

Comenzamos desde el número más grande y vamos comprobando si podemos restarlo al número que tenemos:
⠀
- **128 → 0**  
	128 > 70, el dígito es `0`. 
- **64 → 1**  
	64 < 70, el dígito es `1` y utilizamos el resto: `70 - 64 = 6` 
- **32 → 0**  
	32 > 6, el dígito es `0`. 
- **16 → 0**  
	16 > 6, el dígito es `0`. 
- **8 → 0**  
	8 > 6, el dígito es `0`. 
- **4 → 1**  
	4 < 6, el dígito es `1` y utilizamos el resto: `6 - 4 = 2` 
- **2 → 1**  
	2 = 2, el dígito es `1`. Como el resto llegó a `0`, el resto de dígitos será `0`. 
- **1 → 0**  
	1 > 0, el dígito es `0`. 

Los valores son:

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|-----|----|----|----|---|---|---|---|
|  0  |  1 |  0 |  0 | 0 | 1 | 1 | 0 |

Por lo tanto: 

```
70 (decimal) → 01000110 (binario) 
```

**Comprobación:** sumamos solamente los valores que tienen un `1`:

```
64 + 4 + 2 = 70
```

#### Ejemplo 2: número 151 a binario

Nuevamente, utilizamos las potencias de 2 como referencia:

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|-----|----|----|----|---|---|---|---|

Comenzamos desde el número más grande: 

- **128 → 1**  
	128 < 151, el dígito es `1` y utilizamos el resto: `151 - 128 = 23` 
- **64 → 0**  
	64 > 23, el dígito es `0`. 
- **32 → 0**  
	32 > 23, el dígito es `0`. 
- **16 → 1**  
	16 < 23, el dígito es `1` y utilizamos el resto: `23 - 16 = 7` 
- **8 → 0**  
	8 > 7, el dígito es `0`. 
- **4 → 1**  
	4 < 7, el dígito es `1` y utilizamos el resto: `7 - 4 = 3` 
- **2 → 1**  
	2 < 3, el dígito es `1` y utilizamos el resto: `3 - 2 = 1` 
- **1 → 1**  
	1 = 1, el dígito es `1`. 

Por lo tanto: 

```
151 (decimal) → 10010111 (binario)
```

### 🔥 Potencias de 2

Desde `1`, las cifras se van duplicando:

```
1 → 2 → 4 → 8 → 16 → 32 → 64 → 128 → 256 → 512 → ...
```

Puedes colocar tantos valores como sean necesarios según la conversión que quieras realizar.

### Método 2: De decimal a binario mediante divisiones entre 2

Otra forma de convertir **70 decimal a binario** es dividir sucesivamente entre `2` hasta llegar a un cociente de `1`. Después, escribimos el último cociente y los restos, leyendo **de abajo hacia arriba**.

```
70 ÷ 2 = 35 → resto 0
35 ÷ 2 = 17 → resto 1
17 ÷ 2 = 8  → resto 1
 8 ÷ 2 = 4  → resto 0
 4 ÷ 2 = 2  → resto 0
 2 ÷ 2 = 1  → resto 0
```

El último cociente es `1`. Ahora leemos desde el último cociente hacia arriba:

```
1 0 0 0 1 1 0
```

Por lo tanto:

```
70 (decimal) → 1000110 (binario)
```

Si queremos representarlo utilizando **8 bits**, agregamos un `0` al inicio:

```text
70 (decimal) → 01000110 (binario)
```

## 5. Bits y bytes

La computadora entiende todo en base a un sistema binario compuesto por **bits** y **bytes**.

- **Bit:** cada dígito del sistema binario.
- **Byte:** la combinación de 8 bits.

### Transistores

- Son la forma en que la computadora entiende los unos y ceros.
- Funcionan con dos estados:
  - ON - OFF
  - True - False
  - 0 - 1

## 6. ASCII

Referencia: [ASCII Code](https://www.ascii-code.com/)

**ASCII** (*American Standard Code for Information Interchange*) es un sistema en el que se asigna un **valor numérico** a una letra, número o carácter especial. 

Se le asigna un valor numérico para que posteriormente la computadora pueda representarlo en **binario** y así interpretar de qué letra, número o carácter se trata.

### Tabla ASCII: Letras mayúsculas

| Carácter | Decimal | Carácter | Decimal | Carácter | Decimal | Carácter | Decimal |
|-----------|--------|----------|---------|----------|---------|----------|---------|
| A        | 65      | B        | 66      | C        | 67      | D        | 68      |
| E        | 69      | F        | 70      | G        | 71      | H        | 72      |
| I        | 73      | J        | 74      | K        | 75      | L        | 76      |
| M        | 77      | N        | 78      | O        | 79      | P        | 80      |
| Q        | 81      | R        | 82      | S        | 83      | T        | 84      |
| U        | 85      | V        | 86      | W        | 87      | X        | 88      |
| Y        | 89      | Z        | 90      |          |         |          |         |

Por ejemplo:

```text
A → 65
B → 66
C → 67
...
Z → 90
```

### Traducir código ASCII

Supongamos que recibimos los siguientes valores decimales:

```
161 72 111 108 97 33
```

Podemos buscar cada valor en la tabla ASCII para obtener el carácter correspondiente:

|Decimal |Binario    |Carácter|
|--------|-----------|--------|
|161     |`10100001`|¡      |
|72      |`01001000`|H      |
|111     |`01101111`|o      |
|108     |`01101100`|l      |
|97      |`01100001`|a      |
|33      |`00100001`|!      |

Por lo tanto:

```
161 72 111 108 97 33
 ↓   ↓  ↓   ↓   ↓  ↓
 ¡   H  o   l   a  !

¡Hola!
```

### Convertir un número decimal a binario

También podemos convertir directamente un valor ASCII decimal a binario mediante divisiones sucesivas entre `2`.

Por ejemplo, para convertir el valor ASCII de `!`, que es `33`:

```
33 ÷ 2 = 16 → resto 1
16 ÷ 2 = 8  → resto 0
 8 ÷ 2 = 4  → resto 0
 4 ÷ 2 = 2  → resto 0
 2 ÷ 2 = 1  → resto 0
```

El último cociente es `1`.

Ahora leemos desde el último cociente hacia arriba:

```
1 0 0 0 0 1
```

Por lo tanto:

```
33 (decimal) = 100001 (binario)
```

Si utilizamos 8 bits:

```
33 (decimal) = 00100001 (binario)
```

Y según ASCII:

```text
! → 33 → 00100001
```

### ¿Qué sucede cuando escribimos un texto?

Cuando escribimos `¡Hola!`, podemos entender el proceso de la siguiente manera:

```
Texto
  ↓
Código ASCII
  ↓
Código binario
  ↓
Computadora
```

Por ejemplo:

```text
¡Hola!
  ↓
161 72 111 108 97 33
  ↓
10100001 01001000 01101111 01101100 01100001 00100001
```

Cada carácter tiene asociado un valor numérico y ese valor puede representarse mediante bits.

### Bytes y bits

En ASCII tradicional, cada carácter ocupa **1 byte**, es decir:

```text
1 byte = 8 bits
```

Por lo tanto, el texto `¡Hola!` tiene **6 caracteres**.

Si cada carácter ocupa 1 byte:

```text
6 caracteres × 1 byte = 6 bytes
```

Y como cada byte tiene 8 bits:

```text
6 bytes × 8 bits = 48 bits
```

Por lo tanto:

```text
¡Hola! = 6 bytes = 48 bits
```

> **Nota:** ASCII estándar utiliza 7 bits para representar 128 caracteres (valores 0–127), aunque normalmente los caracteres ASCII se almacenan en unidades de 1 byte (8 bits).  
> El valor `161` de `¡` no pertenece al ASCII estándar; corresponde a una extensión de ASCII, como **ISO-8859-1 / Windows-1252**, dependiendo de la codificación utilizada.

## 7. Unicode

Referencia: [Unicode Table](https://unicode-table.com/en/#basic-latin)

Aunque ASCII fue muy innovador, solo se enfocaba en el alfabeto común y dejaba de lado otros alfabetos y caracteres especiales.

Ahí es donde surge **Unicode**: incluye todos los caracteres especiales, los emojis y distintos alfabetos. Su lista cuenta con más de 1 millón de caracteres.

## 8. RGB

**RGB** es un formato de colores. Cada píxel dentro de una imagen está compuesto por 3 subpíxeles: rojo (**R**ed), verde (**G**reen) y azul (**B**lue), con un tono de 0 a 255.

### Ejemplos de colores básicos

- Negro: (0, 0, 0)
- Blanco: (255, 255, 255)
- Rojo: (255, 0, 0)

### Combinando tonalidades

Combinando tonalidades se pueden formar colores específicos.

Ejemplo: **Plum Purple (178, 80, 228)**

- R: 178 = `10110010`
- G: 80 = `01010000`
- B: 228 = `11100100`

Cada píxel representa un cálculo de la computadora.

### Resumen: todo es binario

La computadora solo interpreta números binarios. Siempre realiza la siguiente transformación:

- Números → binario
- Letras → números (según ASCII) → binario
- Caracteres especiales → número (según Unicode) → binario
- Imagen → números (RGB) → binario
- Música → números (según las ondas) → binario

Es decir, todo lo que realizamos en la computadora consiste en números binarios.

## 9. ¿De dónde viene el internet?

El internet viene directamente de los cables que tenemos en la casa y en la ciudad, y que hacen posible que tengamos conexión.

La mayoría de estos cables se encuentran en el mar, porque van directamente de una parte del mundo a otra.

Referencia: [Submarine Cable Map](https://www.submarinecablemap.com/)

### Origen del nombre

- **Internet** es una abreviación de **Internetworking**. Se creó en los años 70 para referirse a los cables físicos y a las computadoras que se conectan entre sí.

### ARPANET

- El internet nace de un proyecto llamado **ARPANET** (*Advanced Research Projects Agency NETwork*) en los años 70. Es la forma en que se conectaron ciertas universidades entre sí para intercambiar información.
- Fue un experimento del gobierno estadounidense con el fin de **descentralizar sus comunicaciones** en medio de la guerra fría.
- Comenzó conectando 4 computadoras de universidades vía fibra óptica. Después el experimento evolucionó hasta conectar computadoras vía satélite.
- Con la evolución del experimento se establecieron reglas y protocolos, y de ahí nacieron el arroba (@) y **HTTP**.

## 10. Protocolos

### TCP/IP

**TCP/IP** (*Transmission Control Protocol / Internet Protocol*) es un protocolo de transmisión que se divide en 5 etapas.

Es la forma en que se genera la información y en que, al enviarla a través de internet, llega a su destino mediante encabezados. Divide la información en paquetes y, con internet, cada uno de ellos toma el camino más rápido para llegar a una dirección.

### Capas

| Capa            | Protocolos / elementos |
|-----------------|------------------------|
| Aplicación      | HTTP, FTP              |
| Transporte      | TCP, UDP               |
| Red             | IP, routers            |
| Enlace de datos | Ethernet, switches     |
| Físico          | Cables                 |

## 11. ISP

**ISP** (*Internet Service Provider*) son los proveedores de internet. Son intermediarios con toda la infraestructura que nos da acceso a internet, y nos otorgan una **dirección IP** (IP Address).

En resumen, el ISP es esa empresa a la que llamas bien enojado cuando el internet va lento, jaja. Es el que se encarga de conectarte y de mantener la infraestructura de la red.

La IP es como ese "número telefónico" que tienes. Y los DNS… bueno, en la siguiente clase :D

## 12. DNS

**DNS** (*Domain Name System*) se creó para poder identificar a quién tenemos que contactar sin escribir la dirección IP.

Ejemplo: `172.217.7.23` es la IP de Google. En vez de escribir la dirección IP, podemos ingresar a la dirección a través del dominio de Google.

El DNS hace que sea más fácil interactuar con otro equipo.

## 13. El primer desarrollador web

Utilizamos la Web para crear y compartir información.

Hubo un primer desarrollador web: **Tim Berners-Lee**.

- Hizo la propuesta de **W3**, una forma de globalizar la información y poder enlazarla (*linkearla*).
- Todo lo generó a través de una computadora **NeXT**.
- Escribió las 3 tecnologías fundamentales para el desarrollo web:
  - **HTML:** lenguaje de marcado para la Web.
  - **URL:** dirección a la que nos conectamos.
  - **HTTP:** forma de comunicarnos a través de peticiones.
- Construyó el primer servidor web.
- Construyó el primer navegador.

Referencia: [The WorldWideWeb project](http://info.cern.ch/hypertext/WWW/TheProject.html)

## 14. W3C

**W3C** (*World Wide Web Consortium*) trabaja los estándares, que son las tecnologías que se utilizan en la Web. Se encarga de realizar mejoras y modificaciones en la Web, generar propuestas, etc.

Existen muchas empresas que trabajan junto con el W3C para mejorar la Web.

Referencia: [Lista de miembros del W3C](https://www.w3.org/Consortium/Member/List)

## 15. Web browser

Han existido muchos navegadores, por ejemplo:

- **Mosaic:** implementó los primeros gráficos en los navegadores. Este navegador ya no existe.
- **Netscape:** gracias a este navegador tenemos ahora JavaScript.
- **Google Chrome:** mejoró las interacciones con las páginas e inició el desarrollo de las aplicaciones web.

## 16. Evolución del protocolo HTTP

**HTTP** (*Hypertext Transfer Protocol*) son reglas de comunicación.

Para este protocolo existen **HTTP Request** y **HTTP Response**, que se encargan del procesamiento de las solicitudes.

### Métodos de HTTP

- **GET:** solicita datos (por ejemplo, platzi.com).
- **POST:** envía datos (por ejemplo, un login).
- **PUT:** crea o reemplaza datos (modificar).
- **DELETE:** borra datos específicos.

### HTTPS

**HTTPS** (*Hypertext Transfer Protocol Secure*) es la parte de seguridad en la conexión: las peticiones van encriptadas.

## 17. Estándares web

Los **estándares web** nacen a causa de la "Guerra de los Navegadores": no existía una regla sobre hacia dónde iba la Web, y los navegadores implementaban sus propios estándares.

### Estándares

- **HTML:** arquitectura de la información y del texto. Actualmente se usa HTML5.
- **CSS:** manejo de estilos, colores y diseño.
- **JavaScript:** interactividad y aplicaciones web.
- **WebAssembly:** es un estándar que nació en diciembre de 2019 y funciona como un compilador.

## 18. ¿Dónde estamos ahora?

Hay 4000 millones de dispositivos conectados a la Web. Estos dispositivos no son solo computadoras: ahora cualquier equipo puede llegar a conectarse a la Web.

Actualmente existen patrones de diseño web para diversos dispositivos. Como buena práctica, se debería empezar por el diseño **mobile first**.

### Tecnologías actuales

- **Internet of Things (Internet de las cosas):** son objetos inteligentes conectados a internet, por ejemplo, un refrigerador o un automóvil.
- **Machine Learning y Artificial Intelligence (aprendizaje automático e inteligencia artificial):** son tecnologías que están creciendo actualmente, y ambas se están aplicando en muchos proyectos.
- **5G:** gracias a esta tecnología aumentará el número de dispositivos conectados.

## 19. DOM

**DOM** (*Document Object Model*) es un árbol que se genera con la información de las etiquetas HTML.

Proporciona una representación estructural del documento y permite modificar su contenido o su presentación visual. Con JavaScript podemos generar interactividad a través del DOM.

### Ejemplo de árbol DOM

```text
Document
└── html
    ├── head
    │   └── style
    │       └── attribute: type
    └── body
        └── div
            └── attribute: id
```

## 20. CSSOM

**CSSOM** (*CSS Object Model*) es una estructura similar al DOM, pero en lugar de representar el contenido del HTML, representa los **estilos**: genera un árbol con la información de CSS.

Permite leer y modificar los estilos de CSS de forma dinámica, es decir, mientras la página ya está cargada, normalmente usando JavaScript.

### DOM vs. CSSOM (complemento)

|                       | DOM                | CSSOM          |
|-----------------------|--------------------|----------------|
| Se genera a partir de | Las etiquetas HTML | Las reglas CSS |
| Representa            | La estructura y el contenido | Los estilos (colores, tamaños, diseño) |

### Ejemplo (complemento)

Con este CSS:

```css
body { font-size: 16px; }
p    { color: red; }
span { display: none; }
```

el navegador genera un árbol de estilos como este:

```text
CSSOM
└── body (font-size: 16px)
    ├── p (color: red)
    └── span (display: none)
```

### Modificar estilos con JavaScript (complemento)

```js
document.querySelector("p").style.color = "blue";
```

Con esta línea se cambia el color del párrafo mientras la página está abierta.

### Dónde encaja en el proceso de renderizado

El navegador construye el **DOM** y el **CSSOM** por separado. Luego los une para formar el **Render tree**.

## 21. Render tree

El **Render tree** (árbol de renderizado) es un árbol que se genera al juntar los objetos del **DOM** y del **CSSOM**.

Se construye directamente en el navegador, que interpreta toda la información para saber qué elementos mostrar y con qué estilos.

### Cómo se forma

```text
DOM (estructura y contenido)  ─┐
                               ├──► Render tree
CSSOM (estilos)               ─┘
```

### Qué incluye y qué no

- Incluye solo los elementos **visibles**, cada uno con sus estilos calculados.
- No incluye elementos que no se muestran, como `<head>`, `<script>` o los que tienen `display: none`.

Ejemplo con el HTML y CSS del punto anterior:

```text
DOM:    body → p, span
CSSOM:  p { color: red }   span { display: none }

Render tree:
body
└── p (color: red)
```

El `span` queda fuera porque tiene `display: none`.

### Dónde encaja en el proceso de renderizado

```text
DOM + CSSOM → Render tree → Layout → Paint
```

El Render tree es el paso previo al **Layout** (siguiente punto), donde se calcula la posición y el tamaño de cada elemento.

## 22. Layout

El **Layout** (maquetación) es el paso en el que el navegador identifica en qué parte de la pantalla irá cada elemento del proyecto.

El navegador forma la maquetación del proyecto: a partir del Render tree, se generan los contenedores de información (cajas) que ocupará cada elemento.

### Qué calcula

- La **posición** de cada elemento (dónde empieza en la pantalla).
- El **tamaño** de cada elemento (ancho y alto).
- Estos valores dependen del tamaño de la ventana o del dispositivo, por eso el layout se vuelve a calcular si cambiamos el tamaño de la pantalla.

### Ejemplo (complemento)

Con el Render tree del punto anterior:

```text
Render tree:
body
└── p (color: red)

Layout:
body → x: 0, y: 0, ancho: 1000 px, alto: 600 px
└── p → x: 0, y: 0, ancho: 1000 px, alto: 20 px
```

Los valores son ilustrativos: cambian según el contenido y la pantalla.

### Dónde encaja en el proceso de renderizado

```text
DOM + CSSOM → Render tree → Layout → Paint
```

El Layout define **dónde** va cada caja y **de qué tamaño**. El siguiente paso, **Paint**, se encarga de pintarlas.

## 23. Paint

El **Paint** (pintado) es el paso en el que se ponen los detalles finales para que el proyecto se vea como queríamos al principio. Cada contenedor es como una caja a la que solo le queda ponerle color o diseño dinámico.

Es la parte final del proceso: después de esto ya podemos interactuar con la página.

### Qué se pinta

- Colores de texto y de fondo.
- Bordes y sombras.
- Imágenes.
- El texto mismo, con su tipo de letra.

### Ejemplo

Con el Layout del punto anterior:

```text
Layout:
body → x: 0, y: 0, ancho: 1000 px, alto: 600 px
└── p → x: 0, y: 0, ancho: 1000 px, alto: 20 px

Paint:
body → se pinta el fondo de la página
└── p → se pinta el texto en rojo (color: red)
```

La caja del `p` ya sabía **dónde** estaba y **de qué tamaño** era (Layout); ahora se decide **cómo se ve** (Paint).

### Dónde encaja en el proceso de renderizado

```text
DOM + CSSOM → Render tree → Layout → Paint
```

Con el Paint termina el recorrido del **Critical Rendering Path**: el navegador ya muestra la página en pantalla.

## 24. JavaScript engine

El **JavaScript engine** (motor de JavaScript) es un motor que entiende el lenguaje JavaScript y puede convertirlo a **Machine Code**, para que el navegador sepa qué función debe realizar.

### Qué hace

- **Lee** el código JavaScript de la página.
- **Lo convierte** a Machine Code, el lenguaje binario que entiende la computadora (punto 2 y punto 4).
- **Lo ejecuta**, para que las funciones se lleven a cabo en el navegador.

### Ejemplo

```text
JavaScript:    document.querySelector("p").style.color = "blue";
                         ↓
JS Engine:     lo lee y lo convierte a Machine Code
                         ↓
Navegador:     cambia el color del párrafo a azul
```

### Ejemplos de motores

| Navegador     | Motor          |
|---------------|----------------|
| Google Chrome | V8             |
| Firefox       | SpiderMonkey   |
| Safari        | JavaScriptCore |

### Dónde encaja en el proceso de renderizado (complemento)

```text
DOM + CSSOM → Render tree → Layout → Paint
                  ▲
              JS Engine (ejecuta el JavaScript y puede modificar el DOM y el CSSOM)
```

El JS Engine no es un paso más de la cadena: trabaja en paralelo y puede modificar el DOM y el CSSOM, lo que obliga al navegador a repetir el Render tree, el Layout y el Paint.

## 25. Cierre del curso


## Examen

Puedes revisar y cambiar las respuestas. Al terminar, presiona **"Calificar respuestas"** para enviar las preguntas y conocer tu puntuación.

1. **¿Para qué servían las tarjetas perforadas?**
   Para almacenar información e ingresar instrucciones a una computadora.

2. **¿Cómo convierte una computadora texto en unos y ceros?**
   Las computadoras convierten texto y otros datos en binario utilizando un valor asignado de códigos como ASCII y Unicode.

3. **¿Cuáles son periféricos de salida?**
   Monitor, bocinas, audífonos e impresora.

4. **¿Cuáles son periféricos de entrada?**
   Teclado, micrófono, cámara, mouse, escáner.

5. **En binario, ¿cómo se representaría el número 38?**
   `00100110`

6. **En binario, ¿cómo se representaría el string "hola"?**
   `01101000 01101111 01101100 01100001`

7. **¿Cuántos bits tiene un byte?**
   Un byte tiene 8 bits.

8. **¿Cómo se forma un píxel?**
   Un píxel se forma por la combinación de tonos de 3 subpíxeles: rojo, verde y azul (RGB).

9. **¿Cómo representamos el color rojo en RGB?**
   `(255, 0, 0)`

10. **¿Qué es ISP?**
    Proveedor de servicios de internet (*Internet Service Provider*).

11. **¿Cuáles fueron las tres tecnologías que dieron nacimiento a la web como la conocemos hoy en día?**
    HTML, URL y HTTP.

12. **¿Quién creó el primer navegador?**
    Tim Berners-Lee.

13. **¿Qué significa WWW?**
    *World Wide Web*.

14. **¿Cuál es el protocolo que utilizamos para poder enviar y recibir peticiones en la web?**
    HTTP.

15. **¿Cuáles son todas las partes de un Critical Rendering Path?**
    1. DOM
    2. CSSOM
    3. Render tree
    4. JS Engine (opcional)
    5. Layout
    6. Paint

    Referencia: [CRP: Critical Render Path o ruta de acceso de representación crítica](https://vanessamarely.medium.com/crp-critical-render-path-o-ruta-de-acceso-de-representaci%C3%B3n-cr%C3%ADtica-1f2ca78d2645)

16. **¿En qué paso del Critical Rendering Path se combinan el DOM y el CSSOM?**
    Render tree.

17. **¿En qué paso del Critical Rendering Path comenzamos a crear la estructura del proyecto sin diseño?**
    Layout.

18. **HTML y CSS son dos de los principales estándares web.**
    Verdadero.