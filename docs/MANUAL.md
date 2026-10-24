# Manual · Matriz de patcheo / U-MA

[← Volver al README](../README.md) · [Abrir la app](https://buenosairesfront.github.io/matrizdepatcheo/)

## Índice

1. [Idea general](#1-idea-general)
2. [Encender y primer sonido](#2-encender-y-primer-sonido)
3. [La matriz](#3-la-matriz)
4. [Clavijas](#4-clavijas)
5. [Fuentes (filas)](#5-fuentes-filas)
6. [Destinos (columnas)](#6-destinos-columnas)
7. [Módulos y perillas](#7-módulos-y-perillas)
8. [Teclado, gate y joystick](#8-teclado-gate-y-joystick)
9. [Arpegiador](#9-arpegiador)
10. [Osciloscopio](#10-osciloscopio)
11. [Patches: guardar, copiar, exportar](#11-patches-guardar-copiar-exportar)
12. [Patches de fábrica](#12-patches-de-fábrica)
13. [Recetas para empezar](#13-recetas-para-empezar)
14. [Problemas comunes](#14-problemas-comunes)

---

## 1. Idea general

En un sintetizador modular los módulos no están conectados entre sí: el sonido aparece cuando los unís. Acá, en lugar de cables, hay una **matriz de clavijas** como la del EMS Synthi AKS / VCS3:

- **Eje Y (filas): fuentes.** Todo lo que *sale* de algo: osciladores, salidas de filtros, LFO, envolventes, el teclado.
- **Eje X (columnas): destinos.** Todo lo que *recibe*: las salidas de audio, las entradas de los procesadores y los parámetros que se pueden modular.

Cada punto conecta una fila con una columna. Una fila puede ir a muchos destinos, y un destino puede recibir muchas fuentes (se suman).

## 2. Encender y primer sonido

Los navegadores no dejan sonar nada hasta que tocás algo. Tocá el **botón magenta ⏻** arriba a la derecha: el LED se pone cian y el botón deja de estar magenta. Cualquier clic en la matriz, el teclado o el joystick también enciende el audio.

La primera vez se carga el patch **Básico**: tocá el teclado y suena. Después, la app recuerda el último patch que estabas usando.

## 3. La matriz

- **Pasar el mouse** por un punto ilumina en ámbar su fila y su columna.
- **Tocar un punto vacío** pone la clavija elegida.
- **Tocar un punto con la misma clavija** la saca.
- **Tocar un punto con otra clavija** la cambia (cambia la intensidad).
- Debajo de la matriz, el **lector** explica qué hace la conexión que acabás de tocar.
- Arriba se ve cuántos pins hay. **Azar** arma un patch aleatorio y **Limpiar** vacía la matriz.

Los colores de los bordes agrupan las filas y columnas:

| Color | Filas (fuentes) | Columnas (destinos) |
| --- | --- | --- |
| Amarillo | Fuentes de audio | Afinación y FM de osciladores |
| Cian | Procesos (filtros, VCA, efectos) | Entradas de audio de los procesos |
| Magenta | Controles (LFO, envolventes, teclado…) | Parámetros modulables |
| Blanco | — | Salidas |

En celular, la matriz se desplaza con el dedo; los nombres de filas y columnas quedan fijos.

## 4. Clavijas

| Clavija | Valor | Uso típico |
| --- | --- | --- |
| **Cian** | +10 % | Modulaciones sutiles: vibrato, envío leve a la reverb. |
| **Blanca** | +35 % | Uso general: mezclar osciladores, modular el filtro. |
| **Magenta** | +100 % | Conexión plena: teclado a afinación, VCA a la salida, envolvente al VCA. |
| **Amarilla** | −35 % | Igual que la blanca, pero invierte la señal (el efecto va al revés). |

El valor de la clavija se multiplica por la **escala del destino** (ver la tabla de destinos). Por ejemplo, en afinación la escala es 1200 cents, así que la magenta da **una octava por unidad**: el teclado necesita magenta para quedar afinado.

## 5. Fuentes (filas)

### Audio (amarillo)

| Fuente | Qué es |
| --- | --- |
| OSC 1, OSC 2, OSC 3 | Osciladores con onda elegible (sierra, cuadrada, triángulo, seno). |
| OSC 4 sub | Oscilador seno de rango bajo (10 Hz a 1 kHz): sub-bajo, bombo o modulador de FM. |
| Ruido blanco | Ruido continuo. |

### Procesos (cian)

| Fuente | Qué es |
| --- | --- |
| Ring mod | Salida del modulador en anillo (Ring A × Ring B). |
| Filtro 1 | Salida del filtro pasa-bajos resonante. |
| Filtro 2 | Salida del filtro multimodo (pasa-banda de fábrica). |
| Plegador | Salida del plegador de onda (wavefolder). |
| VCA | Salida del amplificador controlado por tensión. |
| Delay | Salida del delay con realimentación. |
| Reverb | Salida de la reverb por convolución. |

### Control (magenta)

| Fuente | Qué es |
| --- | --- |
| LFO 1, LFO 2, LFO 3 | Osciladores lentos (0,02 a 40 Hz), salida de −1 a +1. |
| Sample & hold | Toma una muestra a la velocidad elegida. Si **S&H entrada** está conectada, congela esa señal; si no, da valores al azar. |
| Envolvente 1, Envolvente 2 | ADSR de 0 a 1, disparadas por el teclado o el arpegio. |
| Teclado afin. | Tensión de afinación: 0 en C4, +1 por octava. |
| Gate | 1 mientras hay una nota apretada, 0 si no. |
| Joystick X, Joystick Y | Posición del pad, de −1 a +1. |
| Rueda | Valor de la perilla "Rueda" (0 a 1). |
| Continua +1 | Una tensión fija de 1: sirve para desplazar un parámetro. |

## 6. Destinos (columnas)

| Destino | Tipo | Escala (× clavija) | Qué hace |
| --- | --- | --- | --- |
| Salida L+R | salida | — | Sale por los dos canales. |
| Salida L / Salida R | salida | — | Sale por un solo canal (estéreo). |
| Filtro 1 in | audio | — | Entra al filtro pasa-bajos 1. |
| Filtro 2 in | audio | — | Entra al filtro 2. |
| Ring A | audio | — | Portadora del modulador en anillo. |
| Ring B | parámetro | 1 | Multiplica la entrada A: anillo con audio, trémolo con LFO. |
| Plegador in | audio | — | Entra al plegador de onda. |
| VCA in | audio | — | Entra al VCA. |
| Delay in | audio | — | Entra al delay. |
| Reverb in | audio | — | Entra a la reverb. |
| OSC 1–4 afin. | afinación | 1200 cents | Afinación exponencial (magenta = 1 octava por unidad). |
| OSC 1 / OSC 2 FM lin. | FM lineal | 600 Hz | Suma Hz a la frecuencia: campanas y metales. |
| Filtro 1 / 2 corte | parámetro | 4800 cents | Abre y cierra el filtro (magenta = 4 octavas por unidad). |
| Filtro 1 / 2 reson. | parámetro | 12 | Sube y baja la resonancia. |
| Plegador drive | parámetro | 0,5 | Cuántas veces se pliega la onda. |
| VCA nivel | parámetro | 1 | Volumen del VCA. Ideal para una envolvente. |
| Delay tiempo | parámetro | 0,25 s | Estira el tiempo: vibrato de cinta y glitches. |
| Delay realim. | parámetro | 0,5 | Cantidad de repeticiones. |
| LFO 1–3 veloc. | parámetro | 8 Hz | Acelera o frena el LFO. |
| S&H entrada | sample & hold | — | La señal que congela el sample & hold. |

**Señal de audio en un parámetro.** Si mandás un oscilador (audio) a un parámetro, la modulación es tan rápida que aparecen bandas laterales: FM, AM, filtros ásperos. Es intencional y es donde están muchos de los sonidos más raros.

**Señal de control en una entrada de audio.** Un LFO lento en una entrada de audio casi no se oye (solo clicks); uno a más de 20 Hz sí.

## 7. Módulos y perillas

Debajo del teclado hay una tarjeta por módulo. Las perillas fijan el **valor base**; lo que conectás en la matriz se suma a ese valor.

- **Faders:** cada valor continuo se mueve con un fader; la barra se llena con el valor.
- **Botones con silueta:** la onda (sierra, cuadrada, triángulo, seno) y el tipo de filtro se eligen con botones que muestran su forma. En el arpegiador, la escala muestra sus notas en 12 puntos, la tónica es un mini teclado y patrón, recorrido y división tienen su ícono.
- **Pantalla del módulo:** cada tarjeta dibuja en vivo su forma: la onda de osciladores y LFO, la curva del filtro, la ADSR de las envolventes, el plegado, las repeticiones del delay, la cola de la reverb y los escalones del sample & hold.
- **Pastilla en la matriz:** tocá el nombre de una fuente (las filas con ▸) y se abre su tarjeta ahí mismo, al lado de la fila. Los cambios se reflejan en la tarjeta de abajo, que sigue en su lugar. Se cierra con ×, con Esc o tocando afuera.

| Módulo | Perillas | Rango |
| --- | --- | --- |
| OSC 1 | Frecuencia, Onda | 20–2000 Hz (261,6) · sierra |
| OSC 2 | Frecuencia, Onda | 20–2000 Hz (262,9) · cuadrada |
| OSC 3 | Frecuencia, Onda | 20–2000 Hz (349,2) · triángulo |
| OSC 4 sub | Frecuencia | 10–1000 Hz (65,4) |
| Filtro 1 | Corte, Resonancia | 40–12 000 Hz · 0–25 dB |
| Filtro 2 | Tipo, Corte, Resonancia | pasa-banda / pasa-altos / pasa-bajos / rechaza-banda · 40–12 000 Hz · 0,1–30 |
| Plegador | Drive | 0,5–8 |
| VCA | Nivel base | 0–1 (0: cerrado hasta que lo abra una envolvente) |
| Delay | Tiempo, Realimentación | 0,01–1,5 s · 0–0,95 |
| Reverb | Tamaño | 0,3–6 s |
| LFO 1 / 2 / 3 | Velocidad, Onda | 0,02–40 Hz |
| Sample & hold | Velocidad | 0,5–30 Hz |
| Envolvente 1 / 2 | Ataque, Caída, Sostén, Relajación | 0,001–3 s · 0,01–3 s · 0–1 · 0,01–5 s |
| Teclado y rueda | Glide, Rueda | 0–0,5 s · 0–1 |
| Salida | Volumen | 0–1 |

La salida pasa por un filtro pasa-altos a 18 Hz, saturación suave y un limitador antes de llegar a los parlantes.

## 8. Teclado, gate y joystick

- **Teclado en pantalla:** dos octavas, polifónico al tocar pero monofónico al sonar (suena la última nota). Con **Oct − / Oct +** se mueve entre C1 y C7.
- **Teclado de la compu:** `A W S E D F T G Y H U J K` (una octava) y siguen `O L P Ñ`. Se ignora mientras escribís en un campo de texto.
- **Gate fijo:** deja el gate abierto, como si mantuvieras una tecla. Útil para drones o para escuchar un patch sin tocar.
- **Glide** (en la tarjeta *Teclado y rueda*): portamento entre notas.
- **Joystick X/Y:** arrastrá el punto. X e Y van de −1 a +1 y aparecen como fuentes en la matriz.

## 9. Arpegiador

Activá **Arpegio**. Con **Sostener** encendido sigue sonando solo; la nota que tocás define desde dónde arranca, siempre ajustada a la escala y la tónica elegidas.

| Control | Opciones |
| --- | --- |
| Escala | Pentatónica mayor, Pentatónica menor, Mayor, Menor natural, Dórica, Lidia, Hirajoshi, In sen |
| Tónica | C a B |
| Patrón | Acorde (salta de a terceras de la escala) o Escala (grado por grado) |
| Recorrido | Sube, Baja, Sube y baja, Azar |
| División | 1/4, 1/8, 1/8 tresillo, 1/16 |
| Tempo | 40–240 bpm |
| Octavas | 1–3 |
| Duración | 10–100 % del paso (largo del gate) |

El arpegio maneja el gate y las envolventes; mientras está activo, *Gate fijo* no se puede usar. Las teclas que toca se iluminan en cian.

## 10. Osciloscopio

Muestra la onda de salida (línea ámbar, sincronizada en el cruce por cero) y el espectro (barras cian). Sirve para ver qué hace el plegador, el ring mod o el filtro.

## 11. Patches: guardar, copiar, exportar

Abrí **Patches** (botón de carpeta arriba o *Patches* en la matriz).

- **Guardar el actual:** escribí un nombre y tocá *Guardar*. Si el nombre ya existe, se reemplaza.
- **Mis patcheos:** lista de lo guardado, con *Cargar* y *Borrar* (pide confirmación).
- **Clásicos:** los 12 patches de fábrica.
- **Código del patch:** el patch actual como texto JSON. *Copiar código* lo copia; pegando otro código y tocando *Cargar este código* lo abre.
- **Archivo:** *Descargar patch actual*, *Descargar biblioteca* (todos tus patches en un archivo) y *Abrir archivo* (acepta un patch o una biblioteca).

Todo se guarda **en este navegador** (`localStorage`). Si borrás los datos del sitio o cambiás de navegador o de equipo, no aparecen: exportá la biblioteca para tener copia. El patch en uso se guarda solo cada vez que cambiás algo.

El formato de los archivos está en [`FORMATO-PATCH.md`](FORMATO-PATCH.md). En [`../ejemplos/`](../ejemplos/) están los patches de fábrica como archivos.

## 12. Patches de fábrica

| Patch | Qué hace | Cómo tocarlo |
| --- | --- | --- |
| Básico | Dos osciladores, filtro con envolvente y VCA. | Tocá el teclado. |
| Campanas | OSC 1 y OSC 3 multiplicados en el ring mod. | Mové la frecuencia del OSC 3. |
| S&H clásico | El sample & hold salta el filtro resonante. | Mantené una nota o usá el arpegio. |
| FM metálico | OSC 4 modula a OSC 1. | Cambiá la frecuencia del OSC 4. |
| Caos realimentado | Lazo plegador → filtro 2 → delay. | Suena solo. |
| Drone Synthi | Tres osciladores en un filtro, con joystick. | Suena solo; X = resonancia, Y = corte. |
| Percusión de ruido | Ruido filtrado afinado por el teclado. | Notas cortas. |
| Bajo ácido | Línea resonante tipo 303 con arpegio. | Corre solo; tocá otra nota para moverlo. |
| Pad analógico | Tres osciladores desafinados, ataque lento. | Acordes largos. |
| Viento | Ruido filtrado con tres LFO lentos. | Suena solo; joystick Y cambia el tono. |
| Bombo analógico | Seno con caída rápida de afinación. | El arpegio lo dispara en negras. |
| Escuela de Berlín | Secuencia en semicorcheas con delay. | Corre sola. |

## 13. Recetas para empezar

**Un oscilador directo.** Limpiar → OSC 1 → Salida L+R (blanca). Suena continuo; cambiá la onda en la tarjeta OSC 1.

**Voz de sintetizador.** Teclado afin. → OSC 1 afin. (magenta) · OSC 1 → Filtro 1 in (blanca) · Filtro 1 → VCA in (magenta) · Envolvente 1 → VCA nivel (magenta) · VCA → Salida L+R (magenta).

**Vibrato.** Sobre la voz anterior: LFO 1 → OSC 1 afin. (cian), con el LFO a unos 5 Hz.

**Filtro que se abre.** Envolvente 2 → Filtro 1 corte (blanca). Con amarilla se cierra en vez de abrirse.

**Trémolo.** OSC 1 → Ring A (magenta) · LFO 2 → Ring B (magenta) · Ring mod → Salida L+R (blanca).

**Ecos que se desafinan.** VCA → Delay in (blanca) · Delay → Salida L+R (blanca) · LFO 3 → Delay tiempo (cian).

## 14. Problemas comunes

| Problema | Qué revisar |
| --- | --- |
| No suena nada | ¿Tocaste ⏻? ¿El LED está cian? ¿Hay alguna fuente de audio llegando a una **Salida**? ¿El VCA está en 0 sin envolvente? Probá *Gate fijo*. |
| En iPhone no suena | Apagá el modo silencio con el interruptor lateral. |
| Suena desafinado con el teclado | Usá clavija **magenta** de *Teclado afin.* a la afinación del oscilador. |
| Ruido fuerte o saturado | Un lazo de realimentación: bajá *Realimentación* del delay o sacá clavijas del lazo. Bajá el *Volumen* de salida. |
| Perdí mis patches | Están en el navegador donde los guardaste. Exportá la biblioteca para tener copia. |
| "El código no es un patch válido" | El texto pegado no es JSON o no tiene `pins`. Ver [`FORMATO-PATCH.md`](FORMATO-PATCH.md). |
