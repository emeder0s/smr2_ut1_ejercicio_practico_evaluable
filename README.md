# Prueba práctica: la web de Nivel Extra

La tienda de videojuegos **Nivel Extra** les encarga su web: una página de inicio y una página de contacto con un formulario que funcione en su servidor.

> [!IMPORTANT]
> **Reglas (léanlas antes de empezar)**
>
> 1. La prueba es **individual**. Pueden consultar sus apuntes, sus prácticas y sus repositorios. **No pueden usar inteligencia artificial** (ChatGPT, Copilot, Gemini…), ni chats, ni pedir ayuda a sus compañeros. Si se detecta, la prueba queda suspensa.
> 2. Usen **exactamente** los nombres de archivos, carpetas, clases, `id` y `name` que pide el enunciado, en minúscula. La prueba se corrige con un programa: si un nombre no coincide, ese punto no cuenta.
> 3. Se les preguntará sobre el código entregado. **Sus respuestas forman parte de la nota.**
> 4. Cuando terminen, deberán **enseñar el diseño de su web antes de la entrega**.
> 5. Para entregar, ejecuten `recoge.sh` y envíen por correo el archivo que genera (lo explica el último apartado). **Sin ese archivo no hay entrega.**

## Calificación

| Parte | Qué se valora | Puntos |
|---|---|:-:|
| Servidor | Apache en marcha, la web en `localhost/examen/` y `enviar.php` funcionando | 1 |
| Página de inicio | Estructura y etiquetas HTML de `index.html` (parte 1) | 2 |
| Formulario | El formulario de `contacto.html` (parte 2) | 2 |
| CSS | Hoja de estilos enlazada y reglas pedidas (parte 3) | 2 |
| HTTP y registros | Las pruebas del servidor (parte 4) | 1 |
| Diseño | Que la web se vea bien y sea fácil de leer (se revisa en su pantalla antes de la entrega) | 1 |
| Defensa oral | Saber explicar su propio código | 1 |

## Material

Descarguen el archivo **`material-examen.zip`** de este repositorio (ábranlo y pulsen el botón de descarga), guárdenlo en su carpeta de Descargas y descomprímanlo (botón derecho → «Extraer aquí»). Dentro tienen:

- `textos.txt`: todos los textos de la web, **en el orden en que van y con la etiqueta en la que va cada uno**. Cópienlos tal cual: lo que se evalúa es el código que ponen ustedes.
- `logo.png`: el logo de la tienda.
- `enviar.php`: el programa que recibe el formulario. **No lo modifiquen.**
- `recoge.sh`: el programa para entregar.

## Parte 0. Preparen la carpeta

Creen la carpeta del examen y háganse dueños de ella, para poder editar sin `sudo`:

```bash
sudo mkdir /var/www/html/examen
sudo chown -R $USER /var/www/html/examen
```

Copien a la carpeta el logo y `enviar.php` (si su carpeta se llama *Downloads*, cambien el nombre):

```bash
cd ~/Descargas/material-examen
cp logo.png enviar.php /var/www/html/examen/
```

Comprueben que `http://localhost/examen/logo.png` enseña el logo. A partir de aquí, todos los archivos van en `/var/www/html/examen/`.

## Parte 1. La página de inicio: `index.html`

> [!TIP]
> Sigan `textos.txt` de arriba abajo: delante de cada texto pone en qué etiqueta va. Esta lista sirve para comprobar que no les falta nada.

- [ ] Estructura completa: `<!DOCTYPE html>`, `<html lang="es">` y un `<head>` con `<meta charset="UTF-8">`, el `<title>` de `textos.txt` y el enlace a `estilos.css`.
- [ ] Un `<header>` con: el logo (`<img>` de `logo.png` con su `alt`), el título en `<h1>`, el lema en un párrafo con `id="destacado"` y un `<nav>` con enlaces a `index.html` y `contacto.html`.
- [ ] Un `<main>` con tres secciones. Cada una va en un `<section>` con su título en `<h2>`:
    - **Novedades:** cada juego en su propio `<article>`, con el nombre del juego en `<h2>`, el texto y el precio. El `<article>` de *Kart Tropical* lleva `class="oferta"`.
    - **Nuestros servicios:** una lista `<ul>` con los cuatro servicios.
    - **Horario.**
- [ ] Un `<footer>` con el texto del pie y **su nombre**.
- [ ] Todas las rutas (imagen, enlaces, hoja de estilos) son **relativas**.

## Parte 2. La página de contacto: `contacto.html`

Los textos, las etiquetas de cada campo y sus `name` están en la segunda parte de `textos.txt`.

- [ ] La misma estructura que la página de inicio: `<head>` con su `<title>` y la hoja de estilos, `<header>` con `<h1>` y menú, el texto de introducción y el `<footer>`.
- [ ] Un formulario que envía los datos a `enviar.php` por el método **POST**.
- [ ] Campo **Nombre**: de texto, con `name="nombre"` y **obligatorio**.
- [ ] Campo **Correo**: de tipo correo electrónico, con `name="email"` y obligatorio.
- [ ] **Plataforma**: un desplegable con `name="plataforma"` y las cuatro opciones.
- [ ] **Mensaje**: un cuadro de texto de varias líneas con `name="mensaje"`.
- [ ] Cada campo con su `<label>` asociado (`for` e `id`).
- [ ] Un botón para enviar, con el texto «Enviar mensaje».

## Parte 3. Los estilos: `estilos.css`

Una sola hoja de estilos, enlazada desde las dos páginas. Tiene que tener, como mínimo, estas reglas:

- [ ] `body`: el tipo de letra (`font-family`) y el color de fondo de la página.
- [ ] `#destacado`: que el lema llame la atención.
- [ ] `.oferta`: que el juego en oferta se distinga de los demás.
- [ ] `nav a`: el estilo de los enlaces del menú.
- [ ] `nav a:hover`: que los enlaces del menú cambien al pasar el ratón.
- [ ] Todo lo que quieran añadir para que la web quede bien: el diseño también puntúa.

## Parte 4. Pongan a prueba su servidor

Todo lo que hagan aquí queda apuntado en el `access.log` de Apache, y eso es lo que se corrige.

- [ ] Abran `http://localhost/examen/contacto.html`, rellenen el formulario y envíenlo. Tiene que salir la página «¡Mensaje recibido!» con sus datos y el método **POST**.
- [ ] Provoquen un error **404** dentro de `/examen/`.
- [ ] Creen un archivo `privado.html` con cualquier contenido y hagan que Apache **no pueda leerlo**: al pedir `http://localhost/examen/privado.html` tiene que dar un **403**.

## Entrega

1. Enseñen el diseño de su web.
2. Ejecuten el programa de entrega:

    ```bash
    cd ~/Descargas/material-examen
    sudo bash recoge.sh
    ```

3. Al terminar, dice dónde ha dejado el archivo: `examen-SUUSUARIO.tar.gz`, en su carpeta personal. **Envíen ese archivo adjunto por correo electrónico.**

> [!NOTE]
> Si cambian algo después de entregar, vuelvan a ejecutar `recoge.sh` y envíen el archivo nuevo: se corrige el último que llegue.
