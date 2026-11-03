# Momento 2: Misión de Apropiación

Catálogo semántico con jerarquía CSS aplicada.

## Archivos

- `index.html` → maquetado semántico
- `estilos.css` → hoja de estilos
- `README.md` → documentación

## Estructura HTML

- `header > nav > ul > li > a` (menú principal)
- `main > section > article` (productos)
- `aside > h2 + ul > li > a` (categorías y marcas)
- `footer > p + ul > li > a` (derechos y redes)

## Cálculo de especificidad

- Etiqueta = 1 punto
- Clase = 10 puntos
- ID = 100 puntos

## Conflicto ID vs Clase

Aunque `.btn-comprar` esté escrito después de `#btn-destacado` en el CSS,
el ID gana siempre porque pesa 100 puntos frente a 10 de la clase.

```css
.btn-comprar   { color: green; } /* 10 pts */
#btn-destacado { color: red; }   /* 100 pts → gana */