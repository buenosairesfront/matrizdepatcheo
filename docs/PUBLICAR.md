# Publicación

[← Volver al README](../README.md)

## Dónde está publicada

La app se sirve con **GitHub Pages** desde la rama `main`, carpeta raíz (`/`):

**https://buenosairesfront.github.io/matrizdepatcheo/**

El archivo `.nojekyll` hace que Pages sirva los archivos tal cual, sin procesarlos.

Si alguna vez Pages queda desactivado: en el repo, **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / `(root)` → Save**. La primera publicación tarda uno o dos minutos.

## Actualizar la app

Toda la app está en `index.html`. Para cambiarla:

1. Editá `index.html` (o reemplazalo por una versión nueva).
2. Probala local (abajo).
3. Hacé commit y push a `main`. Pages se actualiza solo en un par de minutos.

Si cambiás los patches de fábrica, regenerá los archivos de `ejemplos/` y, si cambia el aspecto, `docs/captura.png`.

## Probar local

Doble clic en `index.html` alcanza. Para probar como en la web:

```sh
python3 -m http.server 8000
# abrí http://localhost:8000
```

## Dependencias

Ninguna para correr. Solo carga tipografías de Google Fonts (Barlow Condensed, IBM Plex Mono y Noto Sans JP para el logo); sin conexión usa tipografías del sistema y funciona igual.
