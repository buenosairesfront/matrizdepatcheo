# Formato de patch

[← Volver al README](../README.md)

Los patches se guardan como JSON. La app exporta dos tipos de archivo: un **patch** suelto y una **biblioteca** con varios patches. Los dos se pueden abrir desde *Patches → Abrir archivo* o pegando el texto en *Código del patch*.

## Patch

```json
{
 "app": "U-MA matriz de patcheo",
 "type": "patch",
 "version": 2,
 "name": "Básico",
 "data": {
  "pins": {
   "kbd>o1p": "r",
   "osc1>f1in": "w",
   "flt1>vcain": "r",
   "env1>vcal": "r",
   "vca>outLR": "r"
  },
  "P": { "o1w": "sawtooth", "f1f": 500, "f1q": 8 },
  "arp": { "on": false, "latch": true }
 }
}
```

| Campo | Obligatorio | Descripción |
| --- | --- | --- |
| `app`, `type`, `version` | no | Identifican el archivo. `type` es `"patch"`. |
| `name` | no | Nombre del patch (hasta 40 caracteres). Si falta, se usa "Importado". |
| `data.pins` | **sí** | Objeto `"fuente>destino": "clavija"`. |
| `data.P` | no | Valores de perillas. Los que falten conservan su valor por defecto. |
| `data.arp` | no | `on`: arpegio activo. `latch`: sostener (por defecto `true`). |

También se acepta el objeto `data` solo (sin envoltorio), siempre que tenga `pins`.

### Clavijas

| Código | Clavija | Valor |
| --- | --- | --- |
| `g` | Cian | +0,10 |
| `w` | Blanca | +0,35 |
| `r` | Magenta | +1,00 |
| `b` | Amarilla | −0,35 |

### Fuentes (`fuente` en la clave)

`osc1` `osc2` `osc3` `osc4` `noise` `ring` `flt1` `flt2` `fold` `vca` `dly` `rev` `lfo1` `lfo2` `lfo3` `sh` `env1` `env2` `kbd` `gate` `padx` `pady` `wheel` `dc`

### Destinos (`destino` en la clave)

| Id | Destino | Id | Destino |
| --- | --- | --- | --- |
| `outLR` | Salida L+R | `o2fm` | OSC 2 FM lin. |
| `outL` | Salida L | `f1c` | Filtro 1 corte |
| `outR` | Salida R | `f1q` | Filtro 1 reson. |
| `f1in` | Filtro 1 in | `f2c` | Filtro 2 corte |
| `f2in` | Filtro 2 in | `f2q` | Filtro 2 reson. |
| `ringA` | Ring A | `fdr` | Plegador drive |
| `ringB` | Ring B | `vcal` | VCA nivel |
| `foldin` | Plegador in | `dlt` | Delay tiempo |
| `vcain` | VCA in | `dlf` | Delay realim. |
| `dlyin` | Delay in | `l1r` | LFO 1 veloc. |
| `revin` | Reverb in | `l2r` | LFO 2 veloc. |
| `o1p` … `o4p` | OSC 1–4 afin. | `l3r` | LFO 3 veloc. |
| `o1fm` | OSC 1 FM lin. | `shin` | S&H entrada |

Las claves con fuentes o destinos que no existen, o con clavijas desconocidas, se ignoran al cargar.

### Perillas (`data.P`)

Los valores numéricos fuera de rango se recortan al mínimo o máximo. Las opciones de lista deben coincidir exactamente.

| Id | Perilla | Rango / opciones | Por defecto |
| --- | --- | --- | --- |
| `o1f` `o2f` `o3f` | Frecuencia OSC 1–3 | 20–2000 Hz | 261,6 · 262,9 · 349,2 |
| `o1w` `o2w` `o3w` | Onda OSC 1–3 | `sawtooth` `square` `triangle` `sine` | sierra · cuadrada · triángulo |
| `o4f` | Frecuencia OSC 4 | 10–1000 Hz | 65,4 |
| `f1f` | Filtro 1 corte | 40–12000 Hz | 1200 |
| `f1q` | Filtro 1 resonancia | 0–25 | 4 |
| `f2t` | Filtro 2 tipo | `bandpass` `highpass` `lowpass` `notch` | `bandpass` |
| `f2f` | Filtro 2 corte | 40–12000 Hz | 800 |
| `f2q` | Filtro 2 resonancia | 0,1–30 | 5 |
| `fd` | Plegador drive | 0,5–8 | 1,5 |
| `vb` | VCA nivel base | 0–1 | 0 |
| `dt` | Delay tiempo | 0,01–1,5 s | 0,33 |
| `df` | Delay realimentación | 0–0,95 | 0,4 |
| `rs` | Reverb tamaño | 0,3–6 s | 2,5 |
| `l1r` `l2r` `l3r` | LFO 1–3 velocidad | 0,02–40 Hz | 0,3 · 2 · 5 |
| `l1w` `l2w` `l3w` | LFO 1–3 onda | `sawtooth` `square` `triangle` `sine` | seno · cuadrada · sierra |
| `shr` | S&H velocidad | 0,5–30 Hz | 6 |
| `e1a` `e1d` `e1s` `e1r` | Envolvente 1 A D S R | 0,001–3 · 0,01–3 · 0–1 · 0,01–5 | 0,005 · 0,3 · 0,6 · 0,4 |
| `e2a` `e2d` `e2s` `e2r` | Envolvente 2 A D S R | ídem | 0,01 · 0,5 · 0,2 · 0,6 |
| `gl` | Glide | 0–0,5 s | 0 |
| `wh` | Rueda | 0–1 | 0 |
| `mv` | Volumen de salida | 0–1 | 0,6 |
| `aSc` | Arpegio escala | `pmay` `pmin` `may` `men` `dor` `lid` `hira` `insen` | `pmay` |
| `aTo` | Arpegio tónica | `"0"` (C) a `"11"` (B), como texto | `"0"` |
| `aPa` | Arpegio patrón | `chord` `scale` | `chord` |
| `aMo` | Arpegio recorrido | `up` `down` `updown` `rand` | `updown` |
| `aDi` | Arpegio división | `"4"` `"8"` `"8t"` `"16"` | `"16"` |
| `aBpm` | Arpegio tempo | 40–240 | 110 |
| `aOc` | Arpegio octavas | 1–3 | 2 |
| `aGa` | Arpegio duración | 0,1–1 | 0,5 |

## Biblioteca

```json
{
 "app": "U-MA matriz de patcheo",
 "type": "library",
 "version": 2,
 "patches": [
  { "name": "Mi patch", "date": 1792694110000, "data": { "pins": { }, "P": { }, "arp": { } } }
 ]
}
```

Al importar una biblioteca, cada patch se agrega a *Mis patcheos*; si ya existe uno con el mismo nombre (sin distinguir mayúsculas), se reemplaza.

## Almacenamiento en el navegador

| Clave de `localStorage` | Contenido |
| --- | --- |
| `umamp-lib-v1` | Lista de patches guardados (mismo formato que `patches` de la biblioteca). |
| `umamp-cur-v2` | Patch en uso, para recuperarlo al volver a abrir la app. |
