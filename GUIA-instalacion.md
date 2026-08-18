# Guía: subir tu Backlog a GitHub Pages e instalarlo en tu Samsung

Todo esto se hace **desde el navegador**. No necesitas Git, ni terminal, ni instalar nada.

---

## Archivos que vas a subir

Son cinco, todos van **en la raíz** del repositorio (sin carpetas):

| Archivo | Qué es |
|---|---|
| `index.html` | La app |
| `manifest.json` | Nombre, ícono y colores |
| `sw.js` | El caché offline |
| `icon-192.png` | Ícono chico |
| `icon-512.png` | Ícono grande |

> El nombre `index.html` es obligatorio. GitHub Pages busca ese archivo para saber qué mostrar.

---

## Parte 1 — Crear el repositorio

1. Entra a **github.com** y da clic en el **+** de arriba a la derecha → **New repository**.
2. **Repository name**: `backlog` (o el nombre que quieras, en minúsculas y sin espacios).
3. **Visibility**: elige **Public**. Es obligatorio: con cuenta gratuita, publicar desde una rama solo funciona en repos públicos.
4. Marca la casilla **Add a README file**. Esto crea la rama `main` de una vez.
5. Clic en **Create repository**.

---

## Parte 2 — Subir los archivos

1. Ya dentro del repo, clic en **Add file** → **Upload files**.
2. Arrastra (o selecciona) los **cinco archivos** juntos.
3. Espera a que terminen de cargar y clic en **Commit changes**.

Deberías ver los cinco archivos listados en la página principal del repo.

---

## Parte 3 — Encender GitHub Pages

1. En tu repo, clic en la pestaña **Settings** (arriba a la derecha).
2. En el menú de la izquierda, sección **Code and automation**, clic en **Pages**.
3. En **Build and deployment** → **Source**, elige **Deploy from a branch**.
4. En **Branch**, cambia de `None` a **main**, deja la carpeta en **/(root)** y clic en **Save**.
5. Espera 1-2 minutos y refresca la página. Aparecerá tu dirección arriba.

Tu URL queda así:

```
https://TU-USUARIO.github.io/backlog/
```

**La diagonal final importa.** Si la omites, el manifest y el service worker pueden no cargar.

---

## Parte 4 — Instalarla en tu Samsung

1. Abre esa URL en **Chrome** en tu celular.
2. Espera unos segundos a que cargue completa (la primera vez descarga las fuentes).
3. Va a aparecer el botón morado **"Instalar en el celular"** dentro de la app. Dale clic.
   - Si no aparece: menú **⋮** de Chrome → **Añadir a pantalla de inicio** o **Instalar aplicación**.
4. Confirma. El ícono morado queda en tu pantalla de inicio.

Ábrela desde el ícono: debe verse a pantalla completa, sin barra de direcciones. Ponla en modo avión para comprobar que funciona sin internet.

---

## Cómo actualizarla después

Cuando quieras cambiar algo (agregar juegos, cambiar colores, lo que sea):

1. Entra al repo → clic en el archivo → ícono del **lápiz** para editar.
2. Guarda con **Commit changes**.
3. **Importante**: si tocas `index.html`, abre también `sw.js` y sube el número de versión:
   `const CACHE = 'backlog-v1'` → `'backlog-v2'`.
   Sin ese cambio, tu celular puede seguir sirviendo la versión vieja desde el caché.
4. Abre la app en el celular, ciérrala y vuelve a abrirla. Ya está actualizada.

---

## Si algo falla

| Síntoma | Causa probable | Solución |
|---|---|---|
| Error 404 al abrir la URL | Pages aún no termina, o el archivo no se llama `index.html` | Espera 2 min y refresca; verifica el nombre exacto |
| No aparece la opción de instalar | Falta el manifest o el service worker | Confirma que `manifest.json` y `sw.js` están en la raíz junto al `index.html` |
| Se abre con barra del navegador | No se registró como app instalada | Desinstala el acceso directo y vuelve a instalarla desde Chrome |
| No guarda los cambios | Modo incógnito o almacenamiento bloqueado | Ábrela en una pestaña normal de Chrome |
| El botón "Deploy from a branch" está gris | El repo es privado | Settings → General → Danger Zone → cambiar a **Public** |

---

## Si después quieres el APK

Con la PWA ya publicada, entra a **pwabuilder.com**, pega tu URL y te genera el paquete de Android. Usa Trusted Web Activity y Bubblewrap de Google, y te entrega un `.apk` para instalar directo y un `.aab` para la Play Store.

Ten en cuenta dos cosas: si generas el APK sin firmar tienes que firmarlo antes de instalarlo, y necesitas subir un archivo `assetlinks.json` a tu sitio o Android te va a mostrar la barra de direcciones dentro de la app.

Mi consejo: prueba primero la PWA. Para uso personal hace lo mismo y se actualiza sola.
