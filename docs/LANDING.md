# Enlace desde la landing de Buenos Aires Front

[← Volver al README](../README.md)

La matriz de patcheo va a ser una de las opciones de la landing de **Buenos Aires Front** (todavía no está hecha). Esta página junta lo necesario para sumarla cuando se arme.

## Datos de la tarjeta

Están en [`landing.json`](../landing.json), en la raíz del repo, para que la landing los pueda leer directo o copiarlos a mano:

| Campo | Valor |
| --- | --- |
| Título | Matriz de patcheo |
| Serie | U-MA / Tool 03 |
| Descripción | Sintetizador modular en el navegador: matriz de clavijas al estilo EMS Synthi, arpegiador en escala y biblioteca de patches. |
| Enlace | https://buenosairesfront.github.io/matrizdepatcheo/ |
| Imagen | https://buenosairesfront.github.io/matrizdepatcheo/docs/captura.png (1280 × 900) |
| Ícono | https://buenosairesfront.github.io/matrizdepatcheo/favicon.svg |

La app ya tiene metadatos Open Graph, así que al compartir el enlace en redes o mensajería aparece con título, descripción y captura.

## Ejemplo de tarjeta

```html
<a class="tool" href="https://buenosairesfront.github.io/matrizdepatcheo/">
  <img src="https://buenosairesfront.github.io/matrizdepatcheo/docs/captura.png"
       alt="Matriz de patcheo U-MA" loading="lazy" width="1280" height="900">
  <small>U-MA / Tool 03</small>
  <h3>Matriz de patcheo</h3>
  <p>Sintetizador modular en el navegador: matriz de clavijas al estilo EMS Synthi,
     arpegiador en escala y biblioteca de patches.</p>
</a>
```

Si la landing se arma leyendo un archivo con la lista de herramientas, alcanza con traer `landing.json`:

```js
const tool = await fetch('https://buenosairesfront.github.io/matrizdepatcheo/landing.json').then(r => r.json());
```

## Si la landing usa un dominio propio

Si Buenos Aires Front publica con un dominio propio (por ejemplo, con un repo `buenosairesfront.github.io` o un `CNAME`), las herramientas quedan bajo ese dominio en `/matrizdepatcheo/` y el enlace pasa a ser relativo: `href="/matrizdepatcheo/"`. En ese caso hay que actualizar las URL de `landing.json` y las etiquetas `og:url` y `og:image` de `index.html`.

## Volver a la landing desde la app

La app todavía no tiene un enlace de vuelta a la landing, porque la landing no existe. Cuando esté publicada, se puede sumar un botón en el encabezado de `index.html` (junto al de encendido) que apunte a su dirección.
