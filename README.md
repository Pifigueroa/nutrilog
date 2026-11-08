# NutriLog (PWA)

App de registro de comidas y nutrientes. Se instala en el celu como una app, funciona sin internet y se carga con la mano, con el teclado o **por voz**. Tu lista de comidas se maneja desde Excel (hoja "Lista").

## Qué hay en esta carpeta

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La app completa (pantallas, lógica y estilos). |
| `manifest.webmanifest` | Le dice al celu el nombre, los colores y el ícono de la app. |
| `sw.js` | "Service worker": guarda la app en el celu para que abra sin internet. |
| `icons/` | Íconos de la app (pantalla de inicio, pestaña del navegador). |
| `xlsx.full.min.js` | Librería (SheetJS) que lee y escribe archivos Excel. Licencia en `xlsx.LICENSE.txt`. |

## 1. Publicarla (hace falta una sola vez)

Una PWA tiene que estar en una dirección web con **HTTPS**. Dos opciones gratuitas:

### Opción A: Netlify Drop (la más rápida)
1. Entrá a https://app.netlify.com/drop
2. Arrastrá esta carpeta (o el .zip) a la zona de carga.
3. Te da una dirección que termina en `netlify.app`.
4. Para quedarte con el sitio, creá una cuenta gratis y "reclamalo" (claim). Según la documentación de Netlify, un sitio subido sin cuenta queda protegido con una contraseña temporal hasta que lo reclamás. Según tu plan, el sitio puede quedar privado por defecto: si es así, hay que hacerlo público desde la configuración del sitio para abrirlo desde el celu sin iniciar sesión.

### Opción B: GitHub Pages
1. Creá una cuenta en https://github.com y un repositorio público nuevo (por ejemplo `nutrilog`).
2. Subí todos los archivos de esta carpeta (botón "Add file → Upload files"). `index.html` tiene que quedar en la raíz.
3. En el repositorio: **Settings → Pages → Build and deployment**: Source "Deploy from a branch", rama `main`, carpeta `/ (root)`. Guardá.
4. Después de uno o dos minutos la app queda en `https://TU-USUARIO.github.io/nutrilog/`.

## 2. Instalarla en el celu

- **Android (Chrome):** abrí la dirección → menú ⋮ → **Instalar app** (o "Agregar a pantalla de inicio").
- **iPhone (Safari):** abrí la dirección → botón Compartir → **Agregar a inicio**.

Se abre a pantalla completa, con su ícono, como cualquier otra app.

## 3. Cargar por voz

En la pestaña **Registro**, tocá el 🎤 y hablá. Dos formas:

- **Por código:** "desayuno uno, media mañana dos, almuerzo cuatro". Entiende también "DES1", "MM2" o el nombre del tipo de comida que uses en tu Excel (por ejemplo "snack uno").
- **Por descripción:** "palta con queso", "salmón", "empanadas de atún".

Siempre te muestra lo que entendió con casillas tildadas. Revisás, tocás **Agregar** y se guarda con la fecha y hora de ese momento (podés cambiarlas antes).

Limitaciones:
- El dictado usa el reconocimiento de voz del navegador: necesita **internet** y que le des permiso al micrófono. Anda mejor en Chrome para Android.
- En iPhone puede no estar disponible dentro de la app instalada. En ese caso, tocá el campo de búsqueda y usá el micrófono del teclado.

## 4. Tus datos

- Se guardan **en el propio dispositivo** (en el navegador). El celu y la compu no se sincronizan solos.
- Para pasar datos de un lado a otro, o para tener una copia de respaldo: pestaña **Comidas → Exportar Excel**. Con **Importar Excel** cargás o actualizás la lista de comidas desde la hoja "Lista".
- Si borrás los datos del navegador o desinstalás la app, se pierden los datos locales. Conviene exportar a Excel cada tanto.

## 5. Actualizar la app

Si cambiás algún archivo, volvé a subirlo y subí el número de versión en la primera línea de `sw.js` (`nutrilog-v1` → `nutrilog-v2`). Así el celu descarga la versión nueva. Se actualiza la próxima vez que abras la app (a veces hay que abrirla dos veces).

## 6. Probarla en tu compu antes de publicarla

Con Python instalado, desde esta carpeta:

```
python3 -m http.server 8000
```

y abrí http://localhost:8000 en Chrome. (Abrir `index.html` con doble clic no alcanza: el service worker y el micrófono necesitan `http://localhost` o `https://`.)
