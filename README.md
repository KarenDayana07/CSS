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
- **Padding (Relleno):** Es el espacio que hay *por dentro* de la caja. Es como el relleno de un cojín; evita que el texto quede pegado a los bordes de la tarjeta. Empuja el contenido hacia adentro.
- **Margin (Margen):** Es el espacio que hay *por fuera* de la caja. Es como cuando separas dos muebles para que no choquen; empuja la tarjeta para alejarla de las demás.

### 2. ¿Por qué es obligatorio usar `box-sizing: border-box`?
Porque si no lo usamos, cuando le metemos relleno (padding) o bordes a una caja, el navegador hace que la caja se vuelva más grande de lo normal. Eso daña el diseño y hace que todo se descuadre. Al usar `border-box`, le decimos al navegador que el tamaño de la caja ya incluye el relleno y los bordes, así todo queda ordenado y no se sale de su lugar.

### 3. ¿Cómo se ven afectados los elementos hermanos cuando le aplicas un margen grande a uno de ellos?
Si le pongo un margen muy grande a una tarjeta, esta va a empujar a las demás tarjetas que están a su alrededor, creando un hueco gigante entre ellas. Si el margen es exagerado, la tarjeta se puede salir del espacio donde debería estar y hasta puede hacer que aparezca una barra para moverse de lado a lado en la pantalla.
