# Sitio web de las guías (para GitHub Pages)

**PUBLICADO el 16/09/2026 10:4x en https://gurmanyach.github.io/guias-webinar-coit/**
Repositorio `gurmanyach/guias-webinar-coit`, rama `main`. Comprobado al publicar: la dirección
responde, la portada enlaza las 15 páginas y la Guía 13 se sirve completa. El QR de las
transparencias y del folleto apunta ahí (decodificado para comprobarlo, no supuesto).
Republicar tras cambios: copiar de `01_ENTREGABLES/GUIAS/` y `git add . && git commit && git push`.

Carpeta lista para publicar tal cual. **Origen: `01_ENTREGABLES/GUIAS/`** — aquí solo hay copias; si algo
cambia, se edita allí y se vuelve a copiar (`Copy-Item ..\01_ENTREGABLES\GUIAS\*.html .`).

## Por qué existe

El código QR llevaba a la página publicada en claude.ai. **Medido por Kim en su móvil el 16/09:** ese
enlace lo intercepta la app de Claude y no muestra las guías. Google Drive tampoco sirve: no muestra un
HTML como página web, solo lo descarga. Decisión de Kim (16/09 01:3x): **publicar el HTML en GitHub Pages**
y apuntar ahí el QR.

## Contenido

| Fichero | Qué es |
|---|---|
| `index.html` | Portada con las 14 guías y el glosario |
| `Guia_1…Guia_14`, `Glosario.html` | Las 15 páginas navegables, cada una con el botón «Índice de guías» |
| `Guias_y_glosario_Webinar_IA.pdf` | Las 14 guías + glosario en PDF (203 págs., 3,2 MB), por si alguien prefiere descargarlo |
| `Catalogo_de_marcos_Webinar_IA.pdf` | La Guía 11 completa: los 47 marcos con ficha, anatomía, taller y evidencia (412 págs., 6,1 MB) |
| `Guias_y_glosario_COMPLETO.html` | Todo en un solo HTML, con las pestañas desplegadas y sin recursos externos. **No lleva botón de índice** (es autocontenido, para guardarlo suelto) y **la portada no lo enlaza** |
| `.nojekyll` | Evita que GitHub reprocese las páginas |

**Por qué el catálogo va en un PDF aparte** (decisión de Kim, 16/09, tras medirlo): la Guía 11 son 47 marcos
en bloques desplegables y al imprimirlos abiertos ocupaba 424 de las 619 páginas que llegó a tener el PDF
único. Medido: 619 págs/9,0 MB todo desplegado · 204/3,2 MB con el catálogo plegado · 184/3,0 MB con todo
plegado. Así que el catálogo tiene su propio PDF y en el de las guías queda **enunciado** (los 47 títulos con
autor y resumen, más un aviso de dónde está la ficha completa). Nadie pierde contenido: los 47 marcos
íntegros están en el HTML, en el ZIP y en este sitio.

Ninguna página carga nada de fuera (ni tipografías, ni CDN, ni imágenes externas), así que funcionan
también abiertas desde disco o sin internet.

## Publicar (cuando haya sesión de GitHub)

```powershell
cd E:\BMetal\09_PROYECTOS\webinar_COIT_IA_libre_ejercicio\03_SITIO_WEB
gh auth status                 # debe decir "Logged in to github.com"
git init -b main
git add .
git commit -m "Guías del webinar COIT"
gh repo create guias-webinar-coit --public --source=. --push
gh api -X POST repos/:owner/guias-webinar-coit/pages -f "source[branch]=main" -f "source[path]=/"
gh api repos/:owner/guias-webinar-coit/pages --jq .html_url   # la dirección pública
```

Después: rehacer el QR con esa dirección (`02_FUENTES/qr_guias.png`, con `segno`), regenerar deck y
folleto (`node deck.js && python siglas_pie.py && node handout.js`) y volver a exportar el PDF del
folleto. **Comprobación final: escanear el QR con el móvil** — es la única prueba que vale, porque el
fallo anterior solo se vio así.

## Aviso

Lo que se suba aquí queda **público en internet**. Las guías pasaron revisión adversarial de saneado,
pero conviene ser exacto sobre **qué** se saneó, porque la frase anterior («sin nombres internos») era
más ancha de lo que el contenido cumple (lo detectó la revisión del 16/09):

- **Fuera, verificado:** direcciones IP, rutas de disco, nombres de clientes y proyectos de cliente,
  correos, teléfonos, credenciales y códigos del sistema de calidad. Comprobado con búsquedas por
  patrón y control positivo: 0 apariciones.
- **Dentro, a propósito:** los **alias de los agentes** del ecosistema y su reparto de papeles (Guía 7,
  «El ecosistema de vecinos»), el **tipo de máquina** sin identificarla («servidor Linux con GPU de
  16 GB», «Mac Studio de 128 GB»), el nombre de algún conector interno (Guía 10) y el **nombre de pila
  del ponente**. Es el contenido que Kim pidió compartir; no es un descuido, pero **es una decisión
  suya**, no del saneado automático. Si se quiere fuera, hay que editar las guías 7 y 10.

Cualquier cambio futuro debe pasar la misma revisión antes de publicarse.

**El PDF ya no se sirve desde Google Drive.** La Guía 14 enlazaba allí el PDF, y eso tenía dos
problemas medidos el 16/09: el fichero servido estaba caducado (132 págs., sin las guías 12-14, entre
ellas la que lo anunciaba) y la página pública de Drive **muestra el correo del propietario** a
cualquiera que abra el enlace. Ahora la Guía 14 describe los dos PDF, que se descargan desde este
mismo sitio.
