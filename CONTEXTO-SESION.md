# Contexto del proyecto — JOFEMESA × LeadadGo

Este repo es la continuación portátil de una sesión de Claude Code que se quedó local a un
ordenador (las sesiones del CLI no se sincronizan entre máquinas). Este archivo resume todo lo
hecho hasta ahora para que, al abrir el repo en otro PC con Claude Code, se pueda retomar el
trabajo sin perder contexto.

## El proyecto

Gaston trabaja en **LeadadGo**, agencia española de leads/Ads. El cliente es **JOFEMESA**,
empresa de alquiler de maquinaria de obra e industria (plataformas elevadoras, carretillas, etc.),
39 años en el mercado, 12 sedes en 8 provincias. El encargo: auditar su web actual y proponer un
rediseño centrado en conversión (formularios, velocidad, medición), con presupuesto tope de
4.000 € y en regla con RGPD.

## Identidad visual usada

Extraída de un PDF de referencia de LeadadGo (`PRESENTACIÓN LEADADGO.pdf.pdf`) — **solo los
colores y tipografías**, no su estructura narrativa:

- `--navy:#1A1449` `--navy2:#1D1A55` `--navy3:#241D66` `--deep:#100D2E`
- `--mag:#B73C8E` `--magl:#C9529F` `--magd:#A43E90`
- `--teal:#3BB8B2` (fondos/bordes) · `--teal-ink:#12726D` (texto sobre fondo claro, 5,75:1 WCAG)
- `--mist:#F0F3FA` `--border:#DEE3F0` `--t2:#545E7B` `--t3:#6B7492` (subido desde `#8A93AC` para cumplir WCAG AA, 4,62:1)
- Tipografías: **Barlow Condensed** (titulares) + **Outfit** (cuerpo), vía Google Fonts

## Estructura de carpetas

```
/                                          ← raíz del repo
├── 01-04-*.pdf                            ← exportaciones PDF de los 4 documentos
├── PRESENTACIÓN LEADADGO.pdf.pdf          ← PDF de referencia de identidad LeadadGo
├── JOFEMESA/
│   ├── 01-Auditoria-Web-Actual.md         ← fuente markdown de cada documento
│   ├── 02-Manual-de-Marca.md
│   ├── 03-Arquitectura-Rediseno.md
│   ├── 04-Propuesta-Comercial-LeadadGo.md
│   └── Nueva carpeta/                     ← (nombre sin limpiar — pendiente si se quiere renombrar)
│       ├── 01-Auditoria-Web-Actual.html
│       ├── 02-Manual-de-Marca.html
│       ├── 03-Arquitectura-Rediseno.html
│       ├── 04-Propuesta-Comercial.html    ← CONFIDENCIAL: precio/hora, márgenes, guion de objeciones
│       ├── 05-Presentacion-Cliente.html   ← presentación de 29 diapositivas para videollamada
│       ├── index.html                     ← portal interno con los 5 documentos
│       ├── assets/leadadgo.css            ← hoja compartida por 01/02/03
│       ├── netlify.toml / robots.txt      ← config del sitio interno
│       └── LEEME-NETLIFY.md               ← instrucciones de despliegue paso a paso
└── JOFEMESA-CLIENTE/
    ├── index.html                         ← copia exacta de 05-Presentacion-Cliente.html
    ├── netlify.toml / robots.txt          ← config del sitio público para el cliente
```

## Los 5 documentos

1. **Auditoría web actual** — revisión de las 24 páginas de jofemesa.com: 0 formularios, 13,2s
   de carga, teléfono roto, medidas de máquinas solo en 12 PDF, catálogo descargable sin captar
   datos, sin testimonios ni reseñas.
2. **Manual de marca** — sistema de color/tipografía para el rediseño, basado en lo que ya
   funciona de JOFEMESA (su rojo, WordPress como base técnica) más la identidad de LeadadGo para
   los propios documentos de propuesta.
3. **Arquitectura del rediseño** — nuevo menú (20 opciones → 6), 8 páginas de provincia, ficha de
   máquina con medidas visibles, panel de medición.
4. **Propuesta comercial** (interna/confidencial) — 3 paquetes: Lanzamiento 1.950 €, Conversión
   2.950 € (recomendado), Performance 3.900 €. Incluye guion de reunión, objeciones y argumento
   de garantía (0 → 15 leads/90 días o seguimos sin cobrar).
5. **Presentación para el cliente** (`05-Presentacion-Cliente.html`) — la misma propuesta pero
   traducida a lenguaje llano sin tecnicismos, pensada para compartir pantalla en videollamada.
   29 diapositivas con scroll-snap, navegables con flechas o rueda del ratón.

## Fixes de contraste WCAG aplicados

Se detectó y corrigió texto blanco sobre blanco en tablas dentro de secciones oscuras
(`section.dark strong{color:#fff}` se colaba en `<table>` de fondo claro), más dos variables de
color con ratio insuficiente (`--t3` y `--teal` usado como texto). Corregido en los 4 HTML y en
`assets/leadadgo.css`, verificado programáticamente (cálculo de luminancia/ratio), no solo a ojo.

## Despliegue en Netlify — DOS sitios separados, a propósito

Netlify free no tiene protección por contraseña por sitio, así que el documento 04 (confidencial)
no puede convivir en el mismo sitio que se le comparte al cliente:

- **Interno** → `https://jofemesa-interno.netlify.app` (se sube la carpeta `JOFEMESA/Nueva carpeta`)
  Sirve los 5 documentos, incluido el 04. Protegido solo con `X-Robots-Tag: noindex` — no indexado
  por Google, pero accesible por cualquiera con el enlace. **Este enlace nunca se le pasa a JOFEMESA.**
- **Cliente** → sitio aparte desde la carpeta `JOFEMESA-CLIENTE/` (solo `index.html` = la
  presentación). Este es el que sí se comparte con el cliente.

Instrucciones completas de subida en `JOFEMESA/Nueva carpeta/LEEME-NETLIFY.md`.

## Presentación replicada en Canva

Se importó `05-Presentacion-Cliente.html` a Canva como diseño editable de 29 páginas, usando
`import-design-from-url` sobre el HTML ya publicado en Netlify (con las 29 secciones marcadas
`data-document-role="page" data-label="..."` para que Canva las reconozca como diapositivas
independientes — sin esas marcas, Canva solo importa la primera pantalla visible).

- Diseño editable: https://www.canva.com/d/13vS_kG4_iZ9npa
- Ya existe un brand kit **"LeadAdGo"** en la cuenta de Canva con los colores/tipografías.
- Pendiente de confirmar a ojo: si la fuente de cuerpo quedó en **Outfit** o si Canva la sustituyó
  por otra — si no es Outfit, cambiarla a **Josefin Sans** (instrucción explícita del usuario).

## Nota sobre este repositorio

`gaston-leadadgo/jofemesa` es **público**, por decisión explícita del usuario (solo lo quiere para
sincronizar el proyecto entre dos ordenadores, no le preocupa la exposición). Se avisó antes de
subir que el documento 04 contiene precio/hora, márgenes y guion de objeciones — el usuario
confirmó que no le importa que sea público.

## Cómo continuar desde otro PC

1. `git clone https://github.com/gaston-leadadgo/jofemesa.git`
2. Abrir Claude Code con esa carpeta como working directory.
3. Pegarle este archivo (`CONTEXTO-SESION.md`) como primer mensaje, o simplemente decirle "lee
   CONTEXTO-SESION.md antes de seguir".
4. Para subir cambios de vuelta: `git add -A && git commit -m "..." && git push`. Para traer
   cambios hechos desde el otro PC: `git pull`.
