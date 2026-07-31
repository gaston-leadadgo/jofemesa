# AUDITORÍA WEB — JOFEMESA
### Análisis técnico, visual, UX/UI y de conversión
**Cliente:** JOFEMESA — Alquiler de maquinaria para construcción e industria
**URL auditada:** https://jofemesa.unportfolio10.com/
**Auditoría realizada por:** LeadadGo
**Fecha:** 30 de julio de 2026

---

## 0. Nota metodológica

Todos los datos de este informe se han obtenido por medición directa sobre la web (inspección del DOM, hojas de estilo computadas, `Performance API` del navegador y recorrido manual de las 24 páginas y 6 entradas de blog). No hay estimaciones salvo donde se indica expresamente.

La URL auditada es un entorno de pruebas/clon alojado en `unportfolio10.com`, con la etiqueta `<meta name="robots" content="noindex, nofollow">`. Esto es correcto para un staging, pero implica dos cosas relevantes:

1. **No podemos medir tráfico ni posiciones reales** desde esta URL. Las conclusiones de SEO son estructurales, no de rendimiento orgánico.
2. **Si este entorno se publicase tal cual, la web sería invisible para Google.** Es el primer punto de la checklist de lanzamiento.

Última modificación registrada del contenido: `2026-02-03`.

---

## 1. Resumen ejecutivo

JOFEMESA tiene un activo comercial serio detrás: 39 años de historia (fundada en 1987), más de 4.000 máquinas en flota con antigüedad media inferior a 3 años, 12 centros operativos en España, triple certificación ISO y pertenencia a IPAF y ANAPAT. Es una empresa con autoridad real en su sector.

**Su web no comunica nada de eso y, sobre todo, no captura ni un solo lead.**

El hallazgo central de esta auditoría es contundente:

> **La web no tiene ningún formulario. Cero. En ninguna de sus 24 páginas.**

Se ha verificado programáticamente (`document.forms` devuelve un array vacío) en la página de inicio, en la página de sedes y en las fichas de producto. La única vía de contacto es un teléfono o un correo electrónico escritos en el pie. Esto significa que hoy:

- **No hay leads trazables.** Ni uno.
- **No se puede instalar una conversión de Google Ads ni de Meta.** No hay evento que disparar.
- **No hay datos de conversión que alimenten los algoritmos de puja.** Cualquier campaña de Ads que se lance sobre esta web trabajará a ciegas y quemará presupuesto.

A esto se suma un rendimiento crítico (13,2 s de carga completa, 2,8 MB de peso, de los cuales 1,99 MB son solo CSS), una página de inicio de 10.185 px de alto en móvil sin un solo punto de conversión, y una arquitectura de 24 páginas con un mega-menú de 20 entradas que fragmenta la autoridad y dispersa al usuario.

**Conclusión:** la web actual funciona como un folleto corporativo digitalizado. Para montar campañas de captación de leads es, literalmente, inutilizable en su estado presente. La buena noticia es que el punto de partida es cero, lo que convierte casi cualquier mejora estructurada en un salto medible.

---

## 2. Stack técnico detectado

| Componente | Detalle |
|---|---|
| CMS | WordPress |
| Tema padre | GeneratePress 3.5.1 |
| Tema hijo | `byensalza` (desarrollo de Ensalza.com, crédito en el pie) |
| Constructor | Elementor 4.2.1 + Elementor Pro 4.2.1 |
| Plugin de menú | Huger Elementor 1.1.4 (mega-menú) |
| Paginación | WP-PageNavi 2.70 |
| Librería de carrusel | Swiper 8.4.5 |
| Iconografía | Font Awesome 5.15.3 (Solid + Brands + Regular) |
| Tipografías | Google Fonts — Montserrat, Lora |
| Indexación | `noindex, nofollow` (entorno de pruebas) |

**Lectura estratégica:** WordPress + Elementor es una base perfectamente válida y es lo que recomendamos mantener. El problema no es el stack, es cómo está implementado. Elementor con 135 widgets en una sola página y 24 hojas de estilo separadas es la causa directa del problema de rendimiento. Se resuelve con arquitectura de plantillas, no cambiando de tecnología.

---

## 3. Rendimiento — el problema más grave después de los formularios

### 3.1 Datos medidos (`Performance API`, escritorio, red real)

| Métrica | Valor medido | Referencia sana | Veredicto |
|---|---|---|---|
| TTFB (respuesta del servidor) | **1.126 ms** | < 400 ms | 🔴 2,8× por encima |
| DOMContentLoaded | **8.706 ms** | < 2.000 ms | 🔴 4,3× por encima |
| Carga completa (`load`) | **13.202 ms** | < 4.000 ms | 🔴 3,3× por encima |
| Peso total transferido | **2.856 KB** | < 1.000 KB | 🔴 2,9× por encima |
| Número de peticiones | **108** | < 50 | 🔴 |
| Nodos del DOM | 1.272 | < 1.500 | 🟡 Aceptable |
| Widgets de Elementor | 135 | — | 🔴 Excesivo |

### 3.2 Desglose del peso — el CSS es el 70 % del problema

| Tipo | Ficheros | Peso |
|---|---|---|
| **CSS** | **24** | **1.989 KB (69,6 %)** |
| Imágenes | 14 | 632 KB (22,1 %) |
| JavaScript | 24 | 158 KB (5,5 %) |
| Preloads / links | 46 | 76 KB (2,7 %) |

Casi **2 MB de CSS repartidos en 24 ficheros** es un caso extremo de acumulación de hojas de estilo de Elementor: una por widget (`widget-image`, `widget-heading`, `widget-divider`, `widget-spacer`, `widget-social-icons`, `widget-post-info`, `widget-loop-carousel`…), una por página (`post-5.css`, `post-279.css`, `post-300.css`, `post-667.css`, `post-674.css`, `post-679.css`, `post-1214.css`, `post-10.css`), una por animación (`zoomIn`, `fadeInRight`, `e-animation-grow`), más las de Font Awesome en tres variantes y las del plugin Huger.

Además hay **46 etiquetas `<link>`**, lo que multiplica los round-trips de red antes de que el navegador pueda pintar nada.

### 3.3 Imágenes mal preparadas

| Fichero | Peso | Tamaño real | Tamaño mostrado | Problema |
|---|---|---|---|---|
| `dumper.jpg` | 219 KB | — | — | JPG sin optimizar, debería ser WebP |
| `1513166312_img1.-15-11.jpg` | 195 KB | — | — | Nombre sin valor SEO |
| `Home.webp` | 192 KB | — | — | WebP pero muy pesado |
| `miniexcavadoras.jpg` | 175 KB | — | — | JPG sin optimizar |
| `1740429355_...grupos-electrogenos_blog.jpg` | — | 480×640 | 480×260 | Se descarga 2,5× más alto de lo que se ve |
| `1740675975_plataforma-artic-40m...jpg` | — | 640×480 | 640×260 | Se descarga 1,8× más alto |
| `1739805789_alq-plataformas...jpg` | 111 KB | 531×440 | 531×260 | Se descarga 1,7× más alto |

**Hallazgos adicionales:**
- **16 de 16 imágenes no tienen atributo `alt`.** Cero. Esto es simultáneamente un fallo de accesibilidad (incumple WCAG 2.1 nivel A), un fallo de SEO (se pierde el 100 % del tráfico de Google Imágenes, muy relevante en maquinaria) y un fallo legal potencial en contratación pública.
- El logotipo (`logotipo-jofemesa.webp`) y el logo de ANAPAT (`logo-ANAPAT-1024x288.png`) devuelven `naturalWidth = 0`, lo que indica que no se están cargando correctamente en el momento de la medición.
- El logo de ANAPAT se muestra a 900×253 px: un sello de asociación ocupando casi el ancho completo del contenedor.
- El `lazy-loading` está aplicado de forma inconsistente (`loading="lazy"` en 4 imágenes, `auto` en 12), incluyendo imágenes de la parte superior que deberían cargarse con prioridad.

### 3.4 Impacto comercial directo sobre las campañas de Ads

Este punto es el que hay que llevar a la reunión comercial:

- Google penaliza en el **Nivel de calidad** la experiencia de la página de destino. Un LCP de esta magnitud sube el CPC de forma directa.
- Con 13 segundos de carga, **más de la mitad del tráfico pagado se pierde antes de ver el contenido**. Se está pagando por clics que nunca llegan a ver la oferta.
- En móvil (donde está el jefe de obra buscando una plataforma), el escenario es peor: 4G real, no fibra.

**Traducción:** cada euro invertido en Ads sobre la web actual rinde una fracción de lo que podría. El rediseño no es un gasto estético, es una palanca directa sobre el coste por lead.

---

## 4. Análisis de la estética visual

### 4.1 Paleta de color — medida sobre estilos computados

| Color | HEX | Usos detectados | Rol actual |
|---|---|---|---|
| Rojo oscuro | `#AC0000` | 24 | Botón primario, acentos |
| Rojo brillante | `#F60000` | 15 | Botón primario **duplicado** |
| Rojo medio | `#D30000` | 4 | Suelto |
| Rojo apagado | `#BF1F1F` | 1 | Suelto |
| Azul marino | `#1C3254` | 110 | Enlaces de navegación (`--base-3`) |
| Negro | `#000000` | 885 (texto) + 7 (fondos) | Texto de cuerpo y botón "Contacto" |
| Blanco | `#FFFFFF` | 143 / 23 | Texto sobre color y fondos |
| Gris medio | `#6D6D6D` | 16 / 6 | Texto secundario |
| Gris azulado | `#69727D` | 10 | Texto secundario |
| Grises de fondo | `#F5F5F5`, `#EBEBEB`, `#E9E9E9` | 7 | Separación de secciones |
| Amarillo | `#EFBB20` | **0** | **Declarado en `--base-2` y nunca usado** |

**Diagnóstico:**

🔴 **Cuatro rojos distintos.** No es una paleta, es una acumulación. Los botones "Ver todo" aparecen simultáneamente en `#AC0000` y en `#F60000` **en la misma página de inicio**, según la sección. Es el síntoma clásico de un diseño construido widget a widget en Elementor sin sistema de diseño detrás.

🔴 **Texto de cuerpo en negro puro `#000000`** (885 elementos). El negro absoluto sobre blanco absoluto genera fatiga visual y hace que la web se sienta cruda y antigua. El estándar actual es una tinta ligeramente desaturada.

🔴 **El botón "Contacto" es negro, no rojo.** El elemento más importante de conversión de toda la web está pintado con el color menos llamativo de la paleta, mientras que "Ver todo" — un enlace de navegación sin valor comercial — se lleva el rojo corporativo. La jerarquía de color está exactamente invertida.

🟢 **Hallazgo aprovechable:** el sistema ya declara `--base-3: #1C3254` (azul industrial) y `--base-2: #EFBB20` (amarillo señalización). Ambos son culturalmente correctísimos para el sector — el amarillo de señalización de obra y el azul de ingeniería —, y el amarillo está **completamente sin usar**. La tríada rojo + azul industrial + amarillo señalización es la paleta correcta para JOFEMESA y ya está a medio declarar en el código. Solo hay que activarla y ordenarla.

### 4.2 Tipografía — medida sobre estilos computados

| Uso | Fuente | Tamaño | Peso | Transform |
|---|---|---|---|---|
| H1 (escritorio) | Montserrat | 46 px | 700 | uppercase |
| H1 (móvil) | Montserrat | 25 px | 700 | uppercase |
| H2 grandes (ELEVACIÓN, MAQUINARIA, VENTA) | Montserrat | 56 px | 800 | uppercase |
| H2 de sección | Montserrat | 26 px | 400 / 700 | uppercase |
| H3 | Montserrat | 26 px | 800 | uppercase |
| Cuerpo (`body`) | **Lora** | 18 px / interlineado 27 px | 400 | none |
| Párrafos | **Lora** | 16 px | 400 | none |
| Navegación | Montserrat | 13 px | 500 | uppercase |
| Botones | Montserrat | **13 px** | 600 | uppercase |

**Diagnóstico:**

🔴 **Lora es una tipografía serif editorial** (diseñada para revistas y textos largos, con contraste caligráfico). Se está usando como fuente de cuerpo de una web de alquiler de maquinaria industrial. Es una disonancia de categoría: comunica "suplemento cultural", no "flota de 4.000 máquinas revisadas". Además está declarada con fallback `sans-serif` (`font-family: Lora, sans-serif`), lo que es un error técnico: si Lora no carga, el texto salta de serif a sans-serif y cambia toda la métrica de la página.

🔴 **Todo en mayúsculas, en todos los niveles.** H1, H2, H3, navegación y botones están en `uppercase`. Las mayúsculas eliminan las ascendentes y descendentes que el ojo usa para reconocer palabras, lo que reduce la velocidad de lectura de forma medida. Aplicado a titulares de 8-12 palabras — como `ALQUILER DE PLATAFORMAS DE ELEVACIÓN Y MAQUINARIA` o `RESULTADOS EXCEPCIONALES CON JOFEMESA: EL PODER DEL ALQUILER DE PLATAFORMAS EN PROYECTOS DE MADRID` — el efecto es un muro tipográfico que el usuario salta.

🔴 **Botones a 13 px.** Es el texto más pequeño de la web y está en el elemento que debe atraer el clic. En móvil, 13 px en mayúsculas es difícil de leer y contribuye al problema de tamaño de área táctil (ver §6).

🔴 **Interlineado de 1,5 con una serif de 18 px** es apretado. Para texto de cuerpo con esta tipografía, lo correcto está en 1,6-1,7.

🟡 **Montserrat sí funciona** como titular: geométrica, robusta, con pesos 700-800 que aguantan bien la escala grande. Es el activo tipográfico a conservar.

### 4.3 Sistema de componentes

| Propiedad | Valor actual | Valoración |
|---|---|---|
| Radio de borde de botones | `0px` | 🟢 Coherente con el registro industrial. Conservar. |
| Padding de botones | `15px 25px` | 🔴 Altura resultante inferior a 48 px |
| Tamaño de texto de botón | `13px` | 🔴 Demasiado pequeño |
| Elementos `position: sticky/fixed` | 4 (cabecera, 2× mega-menú, volver arriba) | 🟡 Existe cabecera fija, pero **no hay CTA fijo de llamada en móvil** |
| Animaciones | `zoomIn`, `fadeInRight`, `e-animation-grow` | 🟡 Decorativas, coste en CSS sin retorno |
| Sombras | Presets de WordPress sin usar de forma sistemática | 🔴 Sin sistema de elevación |
| Escala de espaciado | Presets de Elementor mezclados con valores manuales | 🔴 Sin ritmo vertical consistente |

### 4.4 Veredicto estético global

La web se lee como una **web corporativa española de sector industrial de la generación 2015-2018**: bloques de ancho completo con imagen de fondo y titular en mayúsculas encima, mega-menú desplegable, carrusel de noticias, banda de sellos ISO en el pie. Es competente y no es fea, pero es **indistinguible de sus competidores directos** (Gam, Loxam, Riwal, Transgruas, Alquiber…), que usan exactamente el mismo lenguaje visual.

Para una empresa con 39 años de historia y la flota más joven del sector, la web no está trabajando en su favor. No hay ni un elemento visual que un competidor no pudiera copiar en una tarde, y no hay ni un dato de autoridad presentado con la fuerza que merece.

---

## 5. Análisis de UX / arquitectura de la información

### 5.1 Inventario completo de la web actual — 30 URLs

**Nivel 1 — Menú principal (7 entradas):**
1. Alquiler maquinaria de elevación → `/alquiler-elevacion/`
2. Alquiler maquinaria de obra → `/alquiler-maquinaria/`
3. Venta → `/venta/`
4. Otros servicios → `/otros-servicios/`
5. Nosotros → `/nosotros/`
6. Noticias → `/noticias/`
7. Contacto → `/sedes-jofemesa/`

**Nivel 2-3 — Submenú de Elevación (11 URLs):**
- `/alquiler-elevacion/alquiler-de-plataformas-elevadoras/`
  - `/plataformas-tijera/`
  - `/plataformas-telescopicas/`
  - `/plataformas-articuladas/`
  - `/plataformas-de-oruga-compactas/`
- `/alquiler-de-manipuladores/`
- `/alquiler-de-carretillas-industriales/`
- `/alquiler-de-carretillas-todoterreno/`
- `/alquiler-de-maquinas-de-almacen/`
- `/alquiler-de-plataforma-sobre-camion/`

**Nivel 2 — Submenú de Maquinaria de obra (7 URLs):**
- `/miniexcavadoras/`, `/minicargadoras/`, `/dumper/`, `/grupos-electrogenos/`, `/torres-de-iluminacion/`, `/compresores/`, `/rodillos/`

**Otras (5 URLs + 6 entradas de blog + 4 PDF):**
- `/venta/`, `/otros-servicios/`, `/nosotros/`, `/noticias/`, `/sedes-jofemesa/`, `/politica-privacidad/`
- 6 entradas de blog (todas de febrero-abril de 2025)
- 4 PDF: certificados ISO 9001, ISO 45001, ISO 14001, catálogo `8101-JOFEMEv2.pdf`, política de sistema de gestión

**Total: 24 páginas + 6 entradas + 5 PDF.**

### 5.2 Problemas de arquitectura

🔴 **Mega-menú con 20 entradas visibles simultáneamente.** Un jefe de obra que necesita una plataforma de tijera de 10 metros tiene que atravesar tres niveles (`Alquiler maquinaria de elevación` → `Alquiler de plataformas elevadoras` → `Plataformas Tijera`) para llegar a una página que, cuando llega, no tiene ni el precio ni un formulario. Es un embudo con tres fricciones antes del contenido y ninguna salida hacia la conversión.

🔴 **18 páginas de producto de 400-450 palabras cada una.** Se ha auditado `/plataformas-tijera/` en detalle: unas 400-450 palabras de texto descriptivo genérico, sin tabla de especificaciones en HTML, sin modelos concretos, sin alturas ni capacidades visibles, sin precios. Toda la información técnica útil está encerrada en **12 PDF descargables** (6 fichas técnicas + 6 manuales de uso y seguridad).

Esto tiene tres consecuencias:
- **SEO:** Google no puede indexar las alturas y capacidades que la gente busca ("plataforma tijera 12 metros alquiler"). El contenido diferenciador está oculto.
- **Conversión:** el usuario tiene que descargar un PDF y abrirlo para saber si la máquina le sirve. La mayoría abandona.
- **Búsqueda con IA:** ChatGPT, Perplexity y las AI Overviews de Google no leen esos PDF. JOFEMESA es invisible en el canal de descubrimiento que más crece.

🔴 **La página de contacto no es una página de contacto.** El menú "Contacto" apunta a `/sedes-jofemesa/`, un directorio de 12 centros con dirección, teléfono y correo. Sin formulario, sin horarios (**ninguna de las 12 sedes indica horario de apertura**), sin mapa interactivo verificado, sin selector de provincia. Es una página de información logística, no de conversión.

🔴 **`/otros-servicios/` mezcla líneas de negocio incompatibles.** Junta servicios portuarios (estiba en puertos de Asturias y Levante), embalado y gestión de almacenes siderúrgicos, y mantenimiento de maquinaria industrial. Son tres negocios B2B distintos, con tres compradores distintos, apilados en una página. Para campañas de Ads esto es ruido puro: diluye el mensaje y contamina las audiencias.

🔴 **Blog abandonado.** 6 entradas, la última del 15/04/2025 — más de 15 meses sin publicar. Los títulos son *keyword stuffing* geográfico evidente: "Obras Con Energía: Alquiler De Maquinaria En Málaga Con Grupos Electrógenos De Alta Potencia", "Sostenibilidad En Acción: Alquiler De Maquinaria En Asturias Con JOFEMESA". Aportan cero autoridad y proyectan abandono.

🔴 **Contenido duplicado dentro de la propia página de inicio.** Al inspeccionar las 24 secciones de nivel superior de la home se detecta que las secciones 1-2 se repiten idénticas en las posiciones 4-5, y que el bloque de noticias se renderiza **dos veces** (una como carrusel, otra como cuadrícula), con los mismos 6 posts. Es peso muerto que el navegador descarga y procesa dos veces.

### 5.3 Inconsistencias de contenido detectadas

| Dónde | Qué dice | Problema |
|---|---|---|
| Home, párrafo introductorio | "Con más de **30 años** de experiencia" | Contradice el resto de la web |
| Home, eslogan destacado | "Más de **35 años** impulsando los proyectos…" | |
| `/nosotros/` | Fundada en **1987** → 39 años en 2026 | El dato real es mejor que los dos anteriores |
| `/nosotros/` | "**7 delegaciones** estratégicas" | `/sedes-jofemesa/` lista **12 centros** |
| Cabecera (todas las páginas) | `tel:034985985212` | **Prefijo malformado** (`034` en lugar de `+34`) y número de Asturias en la cabecera global, mientras la home muestra el 91 de Madrid |
| Home | Teléfono visible: 91 361 31 31 | Distinto del enlace `tel:` de la cabecera |

El teléfono de la cabecera merece mención aparte: **el único enlace de contacto directo persistente de toda la web está mal formado y apunta a la delegación equivocada.** En móvil, `tel:034985985212` puede no marcar correctamente según el dispositivo. Es un fallo de conversión de primer orden, y es gratis de arreglar.

---

## 6. Análisis de la experiencia móvil

Medido con viewport de 375 × 812 px (iPhone estándar).

| Métrica | Valor medido | Veredicto |
|---|---|---|
| Alto total de la página de inicio | **10.185 px** | 🔴 ≈ 12,5 pantallas de scroll |
| Desbordamiento horizontal del documento | No | 🟢 |
| Contenedores internos que desbordan | 8 (`swiper-wrapper` a 998 px, secciones a 767 px) | 🟡 Contenidos, pero fuerzan reflow |
| Tamaño de H1 en móvil | 25 px | 🟡 Justo, pero legible |
| Áreas táctiles por debajo de 40 px | **45 de 126 (36 %)** | 🔴 Incumple recomendación de Google (48 px) y de Apple (44 pt) |
| CTA fijo de llamada / WhatsApp | **No existe** | 🔴 |
| Formularios | **0** | 🔴 |

**El dato que hay que poner en la presentación:**

> En móvil, un usuario recorre **12 pantallas y media** de la web de JOFEMESA sin encontrar un solo formulario, un solo botón de WhatsApp ni un solo botón fijo de llamada.

**Único CTA visible sobre la línea de flotación en móvil:** `NUESTRO VÍDEO PRESENTACIÓN`. El primer y único llamado a la acción que ve el usuario es un vídeo institucional. No es una conversión, es una distracción.

---

## 7. Auditoría de conversión — los 12 fallos que impiden captar leads

Ordenados por impacto sobre el coste por lead de una campaña de Ads.

### 🔴 CRÍTICO

**1. No existe ningún formulario en la web.**
Verificado programáticamente. Sin formulario no hay lead, sin lead no hay evento de conversión, sin evento de conversión Google Ads y Meta no pueden optimizar. Es el bloqueo absoluto.

**2. No existe página de agradecimiento (thank-you page).**
Consecuencia de lo anterior. Sin una URL de confirmación no hay dónde disparar el píxel de conversión ni asignar valor a la conversión.

**3. El enlace de teléfono de la cabecera está roto.**
`tel:034985985212`. Prefijo incorrecto y sede equivocada.

**4. No hay WhatsApp.**
En el sector de obra e industria en España, WhatsApp es el canal de contacto por defecto entre jefes de obra, encargados y proveedores. Su ausencia es una pérdida directa de leads que el mercado espera poder generar.

**5. El catálogo se regala sin capturar el correo.**
El PDF `8101-JOFEMEv2.pdf` se descarga con un clic. Es el mejor imán de leads que tiene la empresa — un catálogo completo de flota — y se está entregando a cambio de nada. Igual ocurre con las 12 fichas técnicas y manuales de `/plataformas-tijera/`.

### 🟠 ALTO

**6. Los CTA no piden nada.**
Inventario completo de los 24 botones de la home: `Ver todo` (×7), `Leer más` (×10), `Contacto` (×2), `Nuestro vídeo presentación`, `Conozca más sobre nosotros`, `Más información`, `Ver todas las noticias`, `Descarga nuestro catálogo`, `Encuentre su sede más cercana`.

Ninguno pide un presupuesto. Ninguno tiene urgencia. Ninguno especifica qué pasa después del clic. `Ver todo` y `Leer más` son etiquetas de navegación, no llamadas a la acción.

**7. Cero prueba social.**
No hay testimonios, no hay logotipos de clientes, no hay casos de éxito con cifras, no hay reseñas de Google. Una empresa que lleva 39 años trabajando con constructoras e industria tiene material de sobra y no está usando nada.

**8. Cero señales de disponibilidad o plazo.**
No se dice en ningún sitio cuánto tarda una entrega, si hay stock hoy, si se entrega en obra, si el transporte está incluido. Son las tres primeras preguntas de cualquier persona que quiere alquilar una máquina, y ninguna tiene respuesta.

**9. No hay precios ni horquillas de precio.**
Es legítimo no publicar tarifas en B2B. Pero no ofrecer ni una horquilla ni un "presupuesto en X horas" deja al usuario sin ningún ancla y lo empuja a pedir precio a tres competidores a la vez.

**10. Las especificaciones técnicas están en PDF, no en HTML.**
Ya descrito en §5.2. El usuario no puede filtrar por altura de trabajo ni capacidad de carga sin descargar documentos.

### 🟡 MEDIO

**11. 36 % de las áreas táctiles por debajo del mínimo recomendado en móvil.**

**12. Sin horarios de apertura en ninguna de las 12 sedes.**
Además de la fricción para el usuario, es una señal de posicionamiento local perdida y un dato que Google Business Profile cruza con la web.

---

## 8. Auditoría SEO estructural

| Elemento | Estado |
|---|---|
| `<title>` de la home | 🔴 **139 caracteres** de *keyword stuffing*: "Inicio - Alquiler de Plataformas, Alquiler de Maquinaria, Venta de Carretillas, Manipuladores, Carretillas Industriales, Carretillas Todoterreno – JOFEMESA" |
| `<meta description>` | 🔴 No existe una propia; el `og:description` es un volcado del primer párrafo cortado con "… Leer más" |
| Un solo `<h1>` por página | 🟢 Correcto (1 en la home) |
| Jerarquía de encabezados | 🔴 H3 (26 px) aparecen antes del H1 en el orden del DOM, y hay H2 con peso 400 y H2 con peso 800 sin criterio |
| `alt` en imágenes | 🔴 **0 de 16** |
| Nombres de fichero de imagen | 🔴 `1513166312_img1.-15-11.jpg`, `1509450327__RSG9913.jpg` — sin valor semántico |
| Datos estructurados (Schema.org) | 🔴 No se detecta ninguno. Faltan `LocalBusiness` ×12, `Organization`, `Product`, `FAQPage`, `BreadcrumbList` |
| Indexación | 🔴 `noindex, nofollow` (correcto en staging, bloqueante en producción) |
| Contenido único por página de producto | 🟡 400-450 palabras genéricas, muy solapadas entre sí |
| Optimización local | 🔴 12 centros sin página propia optimizada, sin `LocalBusiness`, sin horarios, sin reseñas incrustadas |

**La oportunidad orgánica desaprovechada más grande:** JOFEMESA tiene presencia física en Madrid (×3), Valencia (×2), Castellón, Alicante, Asturias (×2), Málaga, Sevilla y Valladolid. Eso son **9 provincias con instalación real**. Búsquedas como "alquiler plataformas elevadoras Málaga" o "alquiler miniexcavadora Valladolid" tienen intención comercial altísima y baja competencia relativa, y hoy JOFEMESA no tiene ni una página construida para capturarlas. Su ventaja competitiva real — estar físicamente cerca — no está representada en la web.

---

## 9. Activos a conservar en el rediseño

No todo hay que tirarlo. Estos son los activos con valor real:

| Activo | Por qué conservarlo |
|---|---|
| **Rojo corporativo** | Reconocible, potente, correcto para el sector. Se consolida, no se cambia. |
| **Montserrat** | Titular robusto y adecuado. Se mantiene. |
| **Fundación en 1987** | 39 años es un dato de autoridad de primer orden. Hay que usarlo bien, no esconderlo tras un "más de 30 años". |
| **+4.000 máquinas en flota** | Cifra dura, verificable, diferencial. Debe estar en el hero. |
| **Antigüedad media < 3 años** | **El mejor argumento comercial de toda la empresa** y hoy está enterrado en `/nosotros/`. Flota joven = menos averías = menos parón de obra. |
| **12 centros en 9 provincias + Portugal** | Base para toda la estrategia de captación geolocalizada. |
| **ISO 9001 + 14001 + 45001, IPAF, ANAPAT** | Requisito de acceso a licitaciones y grandes constructoras. Hay que darle un bloque propio. |
| **12 fichas técnicas + manuales en PDF** | Materia prima de los imanes de leads y del contenido HTML de las páginas pilar. |
| **Catálogo completo de flota (PDF)** | El imán de leads principal, una vez puesto tras formulario. |
| **Vídeo de presentación** | Buen activo. Debe estar más abajo, no como CTA principal. |
| **Servicios industriales (puertos, embalado, mantenimiento)** | Línea de negocio B2B con margen. Necesita su propia página y su propio embudo, separada del alquiler. |
| **Stack WordPress + Elementor** | Válido. Se reconstruye la implementación, no la tecnología. |

---

## 10. Cuadro de mando: antes y objetivo

| Indicador | Hoy (medido) | Objetivo post-rediseño |
|---|---|---|
| Formularios en la web | **0** | 6 |
| Leads trazables/mes | **0** | 25-40 |
| Eventos de conversión configurados | **0** | 6 (formulario, teléfono, WhatsApp, catálogo, sede, presupuesto) |
| Carga completa (escritorio) | 13,2 s | < 3,5 s |
| LCP | > 8 s (estimado a partir de DCL) | < 2,5 s |
| Peso de la página | 2.856 KB | < 900 KB |
| Ficheros CSS | 24 (1.989 KB) | ≤ 3 (< 150 KB) |
| Peticiones HTTP | 108 | < 45 |
| Imágenes con `alt` | 0 % | 100 % |
| URLs en el sitio | 24 páginas + 6 posts | 16 URLs |
| Entradas en el menú principal | 20 | 6 |
| Alto de la home en móvil | 10.185 px | ≈ 5.500 px |
| Áreas táctiles < 40 px | 36 % | 0 % |
| Páginas con datos estructurados | 0 | 16 |
| Páginas de captación geolocalizada | 0 | 7 (una por provincia con sede) |

---

*Documento 1 de 4. Continúa en `02-Manual-de-Marca.md`.*
