# Mi Spelling Bee

Aplicación web de una sola página para practicar el concurso de deletreo
(*spelling bee*) de 1.º y 2.º grado. Son 101 palabras en inglés con su
significado en español, repartidas en dos niveles. Funciona en el teléfono y en
la computadora, sin instalar nada.

Publicada en GitHub Pages: <https://waleon13.github.io/spelling-bee/>

## Niveles

En la portada se elige con qué lista practicar:

- **Nivel 1** — las 50 palabras de la primera lámina.
- **Nivel 2** — las 51 palabras de la segunda lámina.

Los tres modos de palabras (Escuchar y aprender, Deletrear y Quiz) trabajan
sobre el nivel elegido, así que una ronda solo saca palabras de esa lista. El
abecedario no cambia, y Mi progreso suma lo de los dos niveles juntos: las
estrellas y las estadísticas no se llevan por separado. El nivel queda guardado,
así que al volver a abrir la app sigue el último que se usó.

## Modos

La app tiene cinco formas de practicar:

- **Escuchar y aprender** — muestra cada palabra, la dice en voz alta, da su
  significado y su pronunciación letra por letra.
- **Deletrear** — dice una palabra y hay que escribirla sin verla. Da pistas y
  revela la respuesta si no sale a la segunda.
- **Quiz de significados** — muestra la palabra y hay que elegir qué significa
  en español entre cuatro opciones.
- **El abecedario** — las 26 letras A–Z con su nombre en inglés, para oír cada
  una y aprender a decirlas.
- **Mi progreso** — estrellas ganadas, palabras escuchadas, aciertos en
  Deletrear y en Quiz. Incluye un botón para reiniciar las estrellas.

Un sistema de estrellas y confeti premia los aciertos. Las estrellas, las
estadísticas y el nivel elegido se guardan en el navegador (por dispositivo, no
en la nube), así que se conservan al cerrar y volver a abrir.

## Pronunciación

Cada palabra muestra cómo se dice, deletreada con el nombre de cada letra en
inglés pero escrito para leerlo en español. Por ejemplo:

- `just` → jei-iu-es-ti
- `cake` → si-ei-kei-i

La correspondencia letra→sonido está en el objeto `LETTER_SOUND` dentro de
`index.html`. Si alguna letra suena rara, se cambia ahí.

## Cómo usarlo

- **En línea:** abrir la URL de GitHub Pages de arriba.
- **Local:** abrir `index.html` en cualquier navegador moderno. No necesita
  servidor ni conexión (salvo la primera vez, para cargar las tipografías).

La voz usa la síntesis de voz del navegador. En iPhone/Safari el audio solo
arranca después de tocar la pantalla una vez; la app ya lo maneja.

## Archivos

- `index.html` — toda la aplicación (HTML, CSS y JavaScript en un solo archivo).
- `spelling_bee_words_1st-_and_2nd-___1.jfif` — lámina original con las 50
  palabras del Nivel 1.
- `Vocabulario 2.jpeg` — lámina con las palabras del Nivel 2. Trae 52 casillas,
  pero `family` viene repetida en el original, así que son 51 palabras.

## Tecnología

HTML, CSS y JavaScript puro, sin dependencias ni paso de compilación. Las únicas
cargas externas son las tipografías de Google Fonts (*Baloo 2* y *Nunito*).
