# Instrucciones del proyecto — Mi Spelling Bee

App web de una sola página para que una niña de 8 años practique el spelling bee
de 1.º y 2.º grado (50 palabras en inglés con significado en español). Todo vive
en `index.html`. Publicada en GitHub Pages.

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

- `WORDS` — arreglo de pares `["palabra", "significado"]`. Las 50 palabras.
- `LETTER_SOUND` — nombre de cada letra del inglés escrito para leerlo en
  español (A→ei, J→jei, W→dobol-iu, Z→zi…). La función `pronounce(word)` arma
  el texto tipo `jei-iu-es-ti`. Si hay que ajustar cómo suena una letra, se
  cambia aquí y afecta a toda la app.
- Cinco pantallas, cada una en su `<section class="screen">`: los cuatro modos
  (`startLearn`/`renderLearn`, `startSpell`/`renderSpell`, `startQuiz`/`renderQuiz`,
  `startAlphabet`/`renderAlphabet`) más `startProgress`/`renderProgress`.
- **Estado guardado** (`localStorage`, clave `spellingBee.v1`): objeto con
  `stars` y `stats` (`learnHeard`, `spellCorrect`, `spellFirstTry`,
  `quizCorrect`). `loadState()` al arrancar, `saveState()` en cada cambio.
  Es por dispositivo/navegador, no en la nube.
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

## Probar

Abrir `index.html` en el navegador, o servir la carpeta
(`python -m http.server`) si se quiere probar con `localhost` en el navegador
del entorno. Verificar los cuatro modos y que la consola quede sin errores.

## Desplegar

Repositorio: <https://github.com/waleon13/spelling-bee> · Pages:
<https://waleon13.github.io/spelling-bee/>. El despliegue es subir `index.html`
al repo (Pages se actualiza solo). Confirmar con Walter antes de hacer `push`.
