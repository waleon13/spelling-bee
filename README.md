# Mi Spelling Bee

Aplicación web de una sola página para practicar el concurso de deletreo
(*spelling bee*) de 1.º y 2.º grado. Son 50 palabras en inglés con su
significado en español. Funciona en el teléfono y en la computadora, sin
instalar nada.

Publicada en GitHub Pages: <https://waleon13.github.io/spelling-bee/>

## Modos

La app tiene cuatro formas de practicar:

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

Un sistema de estrellas y confeti premia los aciertos. Las estrellas y las
estadísticas se guardan en el navegador (por dispositivo, no en la nube), así
que se conservan al cerrar y volver a abrir.

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
- `spelling_bee_words_1st-_and_2nd-___1.jfif` — imagen original con la lista de
  las 50 palabras.

## Tecnología

HTML, CSS y JavaScript puro, sin dependencias ni paso de compilación. Las únicas
cargas externas son las tipografías de Google Fonts (*Baloo 2* y *Nunito*).
