# Arrejuntao

Junta varias capturas en una sola imagen con un título en cada una, lista para pegar en Word.

Pensado para los trabajos de clase: cuando tienes que poner varias capturas seguidas en un documento y quieres que queden alineadas, del mismo tamaño y cada una con su texto.

Todo se procesa en tu navegador: las imágenes no se suben a ningún sitio.

![Interfaz de Arrejuntao](docs/interfaz.png)

## Qué hace

- **Añadir imágenes** arrastrándolas, eligiéndolas o pegándolas con `Ctrl + V` (ideal con `Win + Shift + S`).
- **Un título por imagen**, encima o debajo, con tamaño, color, tipo de letra y negrita a elegir. Opción de numerarlas automáticamente (`1 · Título`).
- **Recortar** cada imagen arrastrando sobre la zona que quieres conservar. Con *Aplicar a todas* el mismo recorte se aplica al resto (si tienen otro tamaño, en proporción).
- **Ordenar** las imágenes y elegir cuántas van por fila.
- **Igualar el alto** de todas para que queden alineadas sin deformarse, o fijar un alto concreto.
- **Separación, margen, borde fino y fondo transparente** opcionales.
- **Exportar**: copiar la imagen al portapapeles para pegarla en Word, o descargarla en PNG.

Los ajustes se recuerdan en el navegador para la próxima vez. Las imágenes no se guardan.

## Cómo se usa

1. Añade tus capturas.
2. Escribe el título de cada una y ordénalas con ◀ ▶.
3. Recorta si hace falta.
4. Ajusta el aspecto en el panel de la izquierda.
5. Pulsa **Copiar imagen** y pégala en Word con `Ctrl + V`, o **Descargar PNG**.

Resultado con cuatro capturas, dos por fila y con los títulos numerados:

![Ejemplo de resultado](docs/ejemplo.png)

## Por carpetas

Para montar muchas imágenes de una vez, cambia a **Por carpetas** y elige (o arrastra) una carpeta. Cada subcarpeta se convierte en una imagen, con sus capturas juntas y el nombre de cada archivo, sin la extensión, como título.

```
Práctica/
├── imagen1/
│   ├── (1) A.png
│   ├── (2) B con poca luz.png
│   └── (3) C.png
└── imagen2/
    ├── Fallo con la mano lejos.png
    └── Fallo con poca luz.png
```

- **Orden**: pon `(1)`, `(2)`… al principio o al final del nombre. No sale en el título. Las capturas sin número van después, por orden alfabético.
- **Guardar**: en Chrome y Edge, *Guardar en las carpetas* deja cada resultado como `arrejuntao.png` dentro de su subcarpeta (el navegador pide permiso la primera vez). En cualquier navegador, *Descargar ZIP* baja todas, cada una con el nombre de su carpeta.
- **Ajustes**: se aplican los mismos del panel izquierdo a todas. *Editar* abre una carpeta en el modo normal para recortar o retocar esa imagen.

Los `arrejuntao.png` que ya estén en las carpetas se ignoran al volver a cargarlas.

## Cómo funciona

Es un único archivo `index.html` con HTML, CSS y JavaScript, sin dependencias ni proceso de compilación.

La imagen final se dibuja en un `<canvas>`: para cada captura se calcula su tamaño escalado al alto común, se pinta el recorte con `drawImage` y se escribe el título con `fillText`, partiéndolo en líneas con `measureText` si no cabe. El resultado se convierte a PNG con `canvas.toBlob()`.

En el modo por carpetas, la carpeta se lee con la File System Access API (`showDirectoryPicker`), que también permite escribir los resultados en ella, o con un `<input webkitdirectory>` en los navegadores que no la tienen. El ZIP se genera en el propio navegador, sin librerías.

## Licencia

[MIT](LICENSE)
