# Cómo subirlo a Netlify

## Resumen en una línea

Son **dos sitios distintos**, no uno. Uno público para JOFEMESA y otro privado para ti.

| Carpeta a arrastrar | Sitio | Se comparte con |
|---|---|---|
| `JOFEMESA-CLIENTE` | Público | ✅ JOFEMESA |
| `JOFEMESA` | Privado | ❌ Solo LeadadGo |

---

## Por qué dos sitios y no uno

El documento `04-Propuesta-Comercial.html` contiene:

- El cálculo de horas y el precio por hora del proyecto
- La recomendación interna de no vender el paquete de 3.900 € sin el contrato recurrente
- El guion de respuestas a las ocho objeciones de JOFEMESA
- El anclaje de precio y los márgenes previstos

**Netlify no ofrece protección con contraseña en el plan gratuito.** No existe forma de publicar ese fichero y que no sea accesible: cualquiera que escriba la dirección `tu-sitio.netlify.app/04-Propuesta-Comercial.html` lo abre. No hay enlace desde la presentación del cliente, pero la dirección es adivinable.

Por eso la presentación del cliente va en su propia carpeta, como sitio independiente. Ese enlace lo puedes enviar sin pensarlo.

*(Si en algún momento pasas al plan Pro de Netlify, ahí sí existe protección con contraseña por sitio y podrías unificarlo.)*

---

## Paso a paso · Sitio para el cliente

1. Entra en **https://app.netlify.com/drop**
2. Arrastra la carpeta **`JOFEMESA-CLIENTE`** completa a la zona de subida
3. Netlify te da una dirección tipo `random-name-123456.netlify.app`
4. Pulsa **Site configuration → Change site name** y ponle algo presentable:
   `jofemesa-propuesta-leadadgo` → `https://jofemesa-propuesta-leadadgo.netlify.app`
5. Abre el enlace, comprueba que carga y ya lo puedes enviar

La presentación se abre directamente porque el fichero se llama `index.html`.

## Paso a paso · Sitio interno

Lo mismo, arrastrando la carpeta **`JOFEMESA`**. Se abrirá el portal con los cinco documentos.

Direcciones cortas ya configuradas en ese sitio:

- `/presentacion` → presentación del cliente
- `/auditoria` → documento 01
- `/marca` → documento 02
- `/arquitectura` → documento 03

---

## Qué contiene cada carpeta

### `JOFEMESA-CLIENTE` — súbela tal cual

```
JOFEMESA-CLIENTE/
├── index.html               ← la presentación (29 diapositivas)
├── assets/
│   ├── logo.png             ← logo LeadadGo para fondos claros
│   └── logo-negativo.png    ← logo LeadadGo para fondos oscuros
├── netlify.toml             ← cabeceras de seguridad y noindex
└── robots.txt               ← bloquea a los buscadores
```

El CSS y el JavaScript siguen dentro del propio `index.html`, pero desde que el logo real sustituyó a la reconstrucción en CSS, **la carpeta `assets` ya es imprescindible aquí también** — sin ella, el logo saldrá roto en las 29 diapositivas.

### `JOFEMESA` — súbela tal cual

```
JOFEMESA/
├── index.html                      ← portal con los 5 documentos
├── 01-Auditoria-Web-Actual.html
├── 02-Manual-de-Marca.html
├── 03-Arquitectura-Rediseno.html
├── 04-Propuesta-Comercial.html     ← CONFIDENCIAL
├── 05-Presentacion-Cliente.html
├── assets/
│   └── leadadgo.css                ← imprescindible: lo usan los documentos 01, 02 y 03
├── netlify.toml
├── robots.txt
├── LEEME-NETLIFY.md                (este fichero, da igual que se suba)
└── *.md                            (los originales en markdown, dan igual)
```

---

## Lo que NO puedes tocar para que no se rompa

**1. La carpeta `assets` tiene que ir dentro — en las dos carpetas.**
En `JOFEMESA`, los documentos 01, 02 y 03 cargan `assets/leadadgo.css`; sin esa carpeta aparecerán como texto sin formato. En `JOFEMESA-CLIENTE`, `assets/logo.png` y `assets/logo-negativo.png` son los que pintan el logo de las 29 diapositivas; sin ellos, el logo sale roto (aunque el resto de la presentación funcione).

**2. No cambies los nombres de los ficheros ni las mayúsculas.**
Netlify corre sobre Linux y distingue mayúsculas de minúsculas. En tu Windows `01-auditoria...` y `01-Auditoria...` son el mismo fichero; en Netlify no. Si renombras uno, los enlaces del portal dejarán de funcionar.

**3. Arrastra la carpeta, no los ficheros sueltos.**
Si seleccionas los ficheros y los arrastras sin la carpeta, `assets/` se queda fuera.

**4. No metas la carpeta dentro de otra carpeta.**
`index.html` tiene que quedar en la raíz del sitio. Si subes una carpeta que contiene la carpeta `JOFEMESA`, la dirección pasará a ser `tu-sitio.netlify.app/JOFEMESA/` y la raíz dará error 404.

---

## Las tipografías

Barlow Condensed y Outfit se cargan desde Google Fonts. En Netlify funciona sin más, no hay que configurar nada.

Si prefieres que la presentación no dependa de una conexión externa —por si la videollamada va con mal wifi—, dímelo y las incrusto dentro del fichero. Ahora mismo, si Google Fonts no cargara, el navegador usaría Arial Narrow y una sans-serif del sistema: se vería peor pero seguiría siendo legible.

---

## Cuando actualices algo

Netlify no detecta cambios por su cuenta con este método:

1. Ve al sitio en Netlify → pestaña **Deploys**
2. Arrastra otra vez la carpeta a la zona de **Drag and drop your site output folder here**
3. La dirección se mantiene igual

**Ojo con la presentación del cliente:** existe en dos sitios. Si editas `05-Presentacion-Cliente.html` tienes que copiarlo otra vez a `JOFEMESA-CLIENTE\index.html`, o el sitio público se queda con la versión antigua. Si además cambias el logo, hay que volver a copiar la carpeta `assets` también.

Comando para copiarlo (PowerShell, desde `D:\Gutmark\CAPTABILIDADES\Clientes\JoseMesa`):

```powershell
Copy-Item ".\JOFEMESA\Nueva carpeta\05-Presentacion-Cliente.html" ".\JOFEMESA-CLIENTE\index.html" -Force
Copy-Item ".\JOFEMESA\Nueva carpeta\assets\logo*.png" ".\JOFEMESA-CLIENTE\assets\" -Force
```

---

## Para pasarlo a PDF

Los cinco documentos tienen estilos de impresión preparados. Abre el que quieras en Chrome y `Ctrl+P`:

- **La presentación (05)**: sale en horizontal, una diapositiva por página. Marca **Gráficos de fondo** en «Más configuraciones» o los fondos oscuros saldrán en blanco.
- **Los documentos 01-04**: salen en vertical, como un informe. Marca también **Gráficos de fondo**.

Es la forma de tener un PDF que enviar por correo después de la reunión.
