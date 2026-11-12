# Momento 2: Misión de Apropiación

Catálogo semántico con jerarquía CSS, especificidad y modelo de caja aplicado.

## Estructura del proyecto

- `index.html` → Estructura semántica y contenido del catálogo.
- `estilos.css` → Hoja de estilos con herencia, especificidad y modelo de caja.
- `README.md` → Documentación de los hallazgos y cálculos.

## Cálculo de especificidad

- Etiqueta = 1 punto
- Clase = 10 puntos
- ID = 100 puntos

### Conflicto ID vs Clase

Aunque `.btn-comprar` esté escrito después de `#btn-destacado` en el CSS, el ID gana siempre porque pesa 100 puntos frente a 10 de la clase. Finalmente, se refactorizó usando `.btn-destacado` para evitar malas prácticas.

# Hallazgos: El Modelo de Caja

Aquí documenté mis conclusiones sobre cómo funciona el espacio en CSS:

### 1. ¿Cuál es la diferencia práctica entre Margin y Padding?

- **Padding (Relleno):** Es el espacio que hay _por dentro_ de la caja. Es como el relleno de un cojín; evita que el texto quede pegado a los bordes de la tarjeta. Empuja el contenido hacia adentro.
- **Margin (Margen):** Es el espacio que hay _por fuera_ de la caja. Es como cuando separas dos muebles para que no choquen; empuja la tarjeta para alejarla de las demás.

### 2. ¿Por qué es obligatorio usar `box-sizing: border-box`?

Porque si no lo usamos, cuando le metemos relleno (padding) o bordes a una caja, el navegador hace que la caja se vuelva más grande de lo normal. Eso daña el diseño y hace que todo se descuadre. Al usar `border-box`, le decimos al navegador que el tamaño de la caja ya incluye el relleno y los bordes, así todo queda ordenado y no se sale de su lugar.

### 3. ¿Cómo se ven afectados los elementos hermanos cuando le aplicas un margen grande a uno de ellos?

Si le pongo un margen muy grande a una tarjeta, esta va a empujar a las demás tarjetas que están a su alrededor, creando un hueco gigante entre ellas. Si el margen es exagerado, la tarjeta se puede salir del espacio donde debería estar y hasta puede hacer que aparezca una barra para moverse de lado a lado en la pantalla.

# Hallazgos: Centralización de Identidad Visual y Espaciado

### 1. Lista completa de variables declaradas

En la pseudoclase `:root` se declararon las siguientes variables para estandarizar el diseño:

- **Colores:** `--color-primario`, `--color-secundario`, `--color-fondo`, `--color-texto`.
- **Tipografía:** `--fuente-principal` (vinculada desde Google Fonts).
- **Espaciados (Box Model):** `--espaciado-pequeno` (8px), `--espaciado-medio` (16px), `--espaciado-grande` (24px).

### 2. Ventaja de reutilizar medidas de margen y relleno

Usar variables de espaciado evita que el diseño se vea desordenado o desigual. Al usar `var(--espaciado-medio)` en lugar de inventar valores como 15px, 17px o 20px en cada selector, garantizamos que todas las tarjetas y secciones tengan **exactamente la misma proporción de aire**. Esto hace que el catálogo se vea armónico, profesional y fácil de ajustar (si cambio el valor de la variable, cambia en todos lados de golpe).

### 3. Cómo previene colisiones visuales la centralización en `:root`

Al centralizar los colores y medidas en `:root`, la hoja de estilos se vuelve mucho más limpia y predecible. Si el proyecto crece y hay cientos de líneas de código, no tendremos que pelear con colores repetidos que chocan entre sí. Si necesitamos cambiar el color del botón o el fondo, lo hacemos una sola vez en la variable maestra, evitando que un color quede huérfano y garantizando que toda la identidad visual se mantenga unificada.

# Hallazgos: Pseudoclases y Pseudoelementos

## 1. Diferencia funcional entre una pseudoclase y un pseudoelemento\*\*

- **Pseudoclase (ej. `:hover`, `:focus`):** Se usa para **reaccionar a eventos**. No crea nada nuevo, solo le dice al navegador: _"Cuando el usuario pase el mouse (hover) o haga clic en la tecla Tab (focus), cambia el estilo de este elemento"_. Depende de la interacción del usuario.
- **Pseudoelemento (ej. `::before`, `::after`):** Se usa para **inyectar contenido visual**. No depende de lo que haga el usuario, sino que el navegador dibuja un elemento nuevo (como un punto, un ícono o una etiqueta) que no está escrito en el HTML.

## 2. Importancia técnica del `:focus` para la accesibilidad web\*\*

El `:focus` es vital porque mucha gente (o personas con discapacidad visual) navega por internet usando el teclado (tecla Tab) en lugar del mouse. Si no aplicamos un estilo claro de `:focus`, el usuario no sabrá en qué enlace está parado y se perderá. Al ponerle un contorno de color llamativo, garantizamos que la página sea incluyente y fácil de usar para todos, cumpliendo con las normas de accesibilidad.

## 3. ¿Por qué inyectar decoraciones con `::before`/`::after` en lugar de ensuciar el HTML?\*\*

Porque mantener el HTML limpio es una regla de oro. Si queremos poner un punto (`•`) en un menú o una etiqueta de "¡Oferta!", y lo escribimos directo en el HTML, estaríamos llenando el código de etiquetas vacías (como `<span>`) que no aportan nada a la estructura. Al hacerlo desde CSS con `::before` o `::after`, separamos el contenido (HTML) del diseño (CSS). Si el día de mañana queremos quitar las viñetas o la etiqueta de oferta, solo borramos una línea en el CSS y el HTML queda intacto y limpio.

# Hallazgos: Arquitectura BEM y Modularidad

**(1) ¿Qué significa la sigla BEM y cómo se escribe visualmente?**
BEM significa **Bloque, Elemento y Modificador**. Es una forma de nombrar las clases para que cualquiera entienda qué hace cada parte del código:
- **Bloque:** Es el componente principal e independiente. Se escribe con una sola palabra (ej. `.card`).
- **Elemento:** Es una parte que vive dentro del bloque y depende de él. Se escribe con doble guion bajo (ej. `.card__title` o `.card__image`).
- **Modificador:** Es una variación o cambio de estado del bloque o elemento. Se escribe con doble guion medio (ej. `.card--destacada`).

**(2) ¿Por qué dividir el CSS en varios archivos facilita el trabajo colaborativo?**
Porque evita que todo el equipo esté escribiendo en el mismo archivo gigante al mismo tiempo. Si un compañero se encarga de los botones y otro de las tarjetas, cada uno trabaja en su propio archivo (`botones.css` y `tarjeta.css`) sin riesgo de borrar el trabajo del otro. Al final, el archivo principal los une con `@import`. Esto hace que encontrar errores sea mucho más rápido y el proyecto se vuelva ordenado y modular.

**(3) ¿Cómo esta metodología evita la guerra de especificidad (Cascada) al mantener un peso plano?**
Antes usábamos selectores anidados como `aside ul li a`, que hacen que el CSS sea un caos difícil de controlar. Con BEM, usamos una sola clase (como `.sidebar__link`). En CSS, una clase siempre pesa **10 puntos**. Al usar solo clases, todas tus reglas tienen exactamente el mismo peso. Esto significa que ninguna regla va a "pisar" a otra por accidente. Si quieres cambiar algo, simplemente usas el modificador y listo, sin necesidad de usar IDs (que pesan 100) ni el `!important`.