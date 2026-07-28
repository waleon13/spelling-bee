# Instrucciones del proyecto — Mi Spelling Bee

App web de una sola página para que una niña de 8 años practique el spelling bee
de 1.º y 2.º grado (101 palabras en inglés con significado en español, en dos
niveles). Todo vive en `index.html`. Publicada en GitHub Pages.

## Reglas de este proyecto

- **Un solo archivo.** HTML, CSS y JavaScript van juntos en `index.html`. No
  agregar build, frameworks, bundlers ni archivos JS/CSS aparte sin preguntar.
- **Sin dependencias.** La única carga externa son las tipografías de Google
  Fonts. No agregar librerías.
- **No romper el diseño.** Reutilizar las variables CSS (`--honey`, `--green`,
  `--ink`, `--line`, etc.) y las clases existentes (`.card`, `.btn`, `.meaning`,
  `.pron`, `.reveal`…). Estilo editorial y sobrio, sin AI-slop.
- **Es para una niña.** Textos en español, cortos y amables. La interfaz se usa
  en teléfono; cuidar que todo quede tocable y legible.

## Cómo está armado

- `WORDS_N1` (50 palabras) y `WORDS_N2` (51) — arreglos de pares
  `["palabra", "significado"]`, uno por nivel. `WORDS` es la lista activa y
  apunta a uno de los dos; `setLevel(n)` la cambia y `renderLevel()` marca el
  botón elegido en la portada. **Todo lo demás lee `WORDS`**, así que agregar o
  quitar palabras no toca ningún modo.
- Ningún significado se repite dentro de un nivel ni entre niveles. Es a
  propósito: el Quiz identifica la respuesta correcta comparando el texto de la
  opción, así que dos palabras con el mismo significado lo romperían.
- `LETTER_SOUND` — nombre de cada letra del inglés escrito para leerlo en
  español (A→ei, J→jei, W→dobol-iu, Z→zi…). La función `pronounce(word)` arma
  el texto tipo `jei-iu-es-ti`. Si hay que ajustar cómo suena una letra, se
  cambia aquí y afecta a toda la app.
- Cinco pantallas, cada una en su `<section class="screen">`: los cuatro modos
  (`startLearn`/`renderLearn`, `startSpell`/`renderSpell`, `startQuiz`/`renderQuiz`,
  `startAlphabet`/`renderAlphabet`) más `startProgress`/`renderProgress`.
- **Estado guardado** (`localStorage`, clave `spellingBee.v1`): objeto con
  `stars`, `stats` (`learnHeard`, `spellCorrect`, `spellFirstTry`,
  `quizCorrect`) y `level` (1 o 2). `loadState()` al arrancar, `saveState()` en
  cada cambio. Es por dispositivo/navegador, no en la nube.
- Voz: `speak()` (promesa, una frase) y `say()` (cancela y habla). Tienen
  arreglos para iOS Safari (`primeSpeech`, `liveUtterances`). **No tocar esa
  lógica de voz sin preguntar**, es frágil en iPhone.

## Decisiones tomadas

- La pronunciación se escribe con el **nombre en inglés de cada letra**, en
  grafía española. La **W** quedó como `dobol-iu` (aprobado por Walter).
- Las estrellas y estadísticas **se guardan** en `localStorage`. El botón
  "Reiniciar estrellas" (pantalla Mi progreso) pone `stars` en 0 pero **no**
  borra las estadísticas.
- Audio: en Escuchar y aprender el audio **nunca se dispara solo** (ni al entrar
  ni al pasar entre palabras con Anterior/Siguiente); la niña lo controla con
  "Escuchar" / "Despacio". Evita que dos audios choquen y se corte la primera
  letra. El margen entre `cancel()` y `speak()` en `say()` es de 250 ms. Nota:
  en Deletrear y Quiz sí se pronuncia la palabra al cargar (ahí es necesario).
- Feedback táctil: un listener delegado en `document` agrega la clase `.tapped`
  (animación `tapPulse`) a botones, modos, letras y opciones al tocarlos, para
  que se note que el toque registró.
- Audio (deletreo): al pasar de un audio a otro (ej. oír la palabra y luego
  "Deletrear") se cortaba la primera letra. `spellOut` usa `settleSpeech()`, que
  espera a que el motor quede realmente libre (sondeando, con tope de seguridad)
  antes de decir la primera letra, en vez de una pausa fija corta.
- En Aprender, "Anterior" se deshabilita en la primera palabra.
- Las palabras van en **dos niveles separados**, no en una sola lista de 101
  (aprobado por Walter). Así "Escuchar y aprender" sigue siendo una sesión de 50
  o 51 palabras y no mezcla lo que ya domina con lo nuevo. Las estrellas y las
  estadísticas sí son globales, no se llevan por nivel.
- Los dos botones de nivel de la portada reutilizan `.btn-honey` (activo) y
  `.btn-ghost` (inactivo) dentro de un `.nav-row`; no se agregó CSS nuevo.

## Probar

Abrir `index.html` en el navegador, o servir la carpeta
(`python -m http.server`) si se quiere probar con `localhost` en el navegador
del entorno. Verificar los cuatro modos **en los dos niveles** y que la consola
quede sin errores.

## Desplegar

Repositorio: <https://github.com/waleon13/spelling-bee> · Pages:
<https://waleon13.github.io/spelling-bee/>. El despliegue es subir `index.html`
al repo (Pages se actualiza solo). Confirmar con Walter antes de hacer `push`.
