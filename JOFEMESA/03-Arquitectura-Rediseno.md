# ARQUITECTURA DEL REDISEÑO — JOFEMESA
### De folleto corporativo a máquina de captación de leads
**Elaborado por:** LeadadGo · 30 de julio de 2026
**Objetivo del rediseño:** maximizar la captación de leads cualificados y habilitar campañas rentables de Google Ads y Meta Ads

---

## 1. El principio rector

La web actual está construida para **informar**. El rediseño se construye para **capturar**.

Esto significa una regla que atraviesa todas las decisiones de este documento:

> **Toda página tiene exactamente una acción principal, y esa acción es siempre pedir presupuesto o llamar.**
> Si una página no puede convertir, no existe.

De esta regla se deduce todo lo demás: por qué se eliminan 14 URLs, por qué el mega-menú de 20 entradas pasa a 6, y por qué el blog sale del proyecto en la fase 1.

---

## 2. Decisión de arquitectura: de 30 URLs a 16

### 2.1 Cuadro de decisión completo

| # | URL actual | Decisión | Destino / justificación |
|---|---|---|---|
| 1 | `/` (Inicio) | 🔄 **REHACER** | Nueva home orientada a conversión (§4) |
| 2 | `/alquiler-elevacion/` | 🔄 **REHACER como pilar** | Pilar 1: Plataformas elevadoras |
| 3 | `/alquiler-elevacion/alquiler-de-plataformas-elevadoras/` | ❌ **ELIMINAR** | 301 → Pilar 1. Es un nivel intermedio redundante. |
| 4 | `…/plataformas-tijera/` | ❌ **ELIMINAR** | 301 → Pilar 1, sección `#tijera`. Se convierte en bloque con tabla de especificaciones. |
| 5 | `…/plataformas-telescopicas/` | ❌ **ELIMINAR** | 301 → Pilar 1, sección `#telescopicas` |
| 6 | `…/plataformas-articuladas/` | ❌ **ELIMINAR** | 301 → Pilar 1, sección `#articuladas` |
| 7 | `…/plataformas-de-oruga-compactas/` | ❌ **ELIMINAR** | 301 → Pilar 1, sección `#orugas` |
| 8 | `…/alquiler-de-plataforma-sobre-camion/` | ❌ **ELIMINAR** | 301 → Pilar 1, sección `#camion` |
| 9 | `…/alquiler-de-manipuladores/` | ❌ **ELIMINAR** | 301 → Pilar 2, sección `#manipuladores` |
| 10 | `…/alquiler-de-carretillas-industriales/` | ❌ **ELIMINAR** | 301 → Pilar 2, sección `#carretillas-industriales` |
| 11 | `…/alquiler-de-carretillas-todoterreno/` | ❌ **ELIMINAR** | 301 → Pilar 2, sección `#carretillas-todoterreno` |
| 12 | `…/alquiler-de-maquinas-de-almacen/` | ❌ **ELIMINAR** | 301 → Pilar 2, sección `#almacen` |
| 13 | `/alquiler-maquinaria/` | 🔄 **REHACER como pilar** | Pilar 3: Maquinaria de obra |
| 14 | `…/miniexcavadoras/` | ❌ **ELIMINAR** | 301 → Pilar 3, sección `#miniexcavadoras` |
| 15 | `…/minicargadoras/` | ❌ **ELIMINAR** | 301 → Pilar 3, sección `#minicargadoras` |
| 16 | `…/dumper/` | ❌ **ELIMINAR** | 301 → Pilar 3, sección `#dumper` |
| 17 | `…/rodillos/` | ❌ **ELIMINAR** | 301 → Pilar 3, sección `#rodillos` |
| 18 | `…/compresores/` | ❌ **ELIMINAR** | 301 → Pilar 3, sección `#compresores` |
| 19 | `…/grupos-electrogenos/` | ❌ **ELIMINAR** | 301 → **Pilar 4 (nuevo)**: Energía e iluminación |
| 20 | `…/torres-de-iluminacion/` | ❌ **ELIMINAR** | 301 → Pilar 4, sección `#torres` |
| 21 | `/venta/` | 🔄 **REHACER** | Página de venta con formulario propio |
| 22 | `/otros-servicios/` | 🔄 **REHACER y RENOMBRAR** | → `/servicios-industriales/`. Se separa del embudo de alquiler. |
| 23 | `/nosotros/` | 🔄 **REHACER** | Página de autoridad con las cifras al frente |
| 24 | `/sedes-jofemesa/` | 🔄 **REHACER** | → `/sedes/`. Con formulario por sede, horarios y mapa. |
| 25 | `/noticias/` | ❌ **ELIMINAR del menú** | 301 → `/` . Se saca del proyecto en fase 1. |
| 26-31 | 6 entradas de blog | ❌ **ELIMINAR** | 301 a la página pilar temáticamente más cercana |
| 32 | `/politica-privacidad/` | 🔄 **ACTUALIZAR** | Debe cubrir los nuevos formularios y el tratamiento de datos |
| — | — | ✅ **NUEVA** | `/contacto/` — página de conversión pura |
| — | — | ✅ **NUEVA** | `/catalogo/` — imán de leads con formulario |
| — | — | ✅ **NUEVA** | `/gracias/` — página de agradecimiento (obligatoria para el píxel) |
| — | — | ✅ **NUEVA** | `/aviso-legal/` |
| — | — | ✅ **NUEVA** | `/politica-de-cookies/` |
| — | — | ✅ **NUEVA** | 2 landings de campaña (§6) |

**Resultado: 24 páginas + 6 entradas → 16 URLs indexables + 2 landings de campaña + 1 página de agradecimiento.**

### 2.2 El mapa nuevo

```
JOFEMESA.COM
│
├── 🏠 HOME ...................................... conversión
│
├── 🔧 ALQUILER (pilares — el 80 % del tráfico y de los leads)
│   ├── /alquiler-plataformas-elevadoras/ ........ Pilar 1
│   │     └ tijera · telescópica · articulada · orugas · sobre camión
│   ├── /alquiler-carretillas-manipuladores/ ..... Pilar 2
│   │     └ manipuladores · carretilla industrial · todoterreno · almacén
│   ├── /alquiler-maquinaria-obra/ ............... Pilar 3
│   │     └ miniexcavadora · minicargadora · dumper · rodillo · compresor
│   └── /alquiler-energia-iluminacion/ ........... Pilar 4  ← NUEVO
│         └ grupo electrógeno · torre de iluminación
│
├── 🛒 /venta-carretillas-recambios/
├── 🏭 /servicios-industriales/ .................. puertos · embalado · mantenimiento
│
├── 🏢 /empresa/ ................................. autoridad
├── 📍 /sedes/ ................................... 12 centros + formulario por sede
├── 📞 /contacto/ ................................ conversión pura
├── 📕 /catalogo/ ................................ imán de leads
│
├── ✅ /gracias/ ................................. thank-you page (noindex)
│
├── ⚖ /aviso-legal/
├── ⚖ /politica-de-privacidad/
└── ⚖ /politica-de-cookies/

FUERA DEL MENÚ — LANDINGS DE CAMPAÑA
├── /lp/alquiler-plataformas-elevadoras/ ......... Google Ads (7 variantes de ciudad)
└── /lp/alquiler-maquinaria-obra/ ................ Google Ads + Meta
```

### 2.3 El menú nuevo: de 20 entradas a 6

**HOY** — 20 entradas visibles en un mega-menú de 3 niveles:
```
ALQUILER MAQUINARIA DE ELEVACIÓN ▾ (11 subentradas)
ALQUILER MAQUINARIA DE OBRA ▾ (7 subentradas)
VENTA
OTROS SERVICIOS
NOSOTROS
NOTICIAS
CONTACTO
```

**PROPUESTA** — 6 entradas, un solo nivel de desplegable, con CTA persistente:
```
ALQUILER ▾        VENTA    SERVICIOS INDUSTRIALES    EMPRESA    SEDES    [📞 91 361 31 31]  [PEDIR PRESUPUESTO]
   │
   ├─ Plataformas elevadoras
   ├─ Carretillas y manipuladores
   ├─ Maquinaria de obra
   └─ Energía e iluminación
```

El teléfono y el botón de presupuesto están **siempre visibles** en la cabecera fija, en escritorio y en móvil.

### 2.4 Por qué colapsar 18 páginas de producto en 4 pilares

Esta es la decisión de arquitectura que más resistencia genera y la que más valor aporta. La justificación:

**A) Consolidación de autoridad SEO.** Hoy, la autoridad de dominio se reparte entre 18 páginas de 400-450 palabras que se solapan entre sí ("Alquiler de plataformas tijera" y "Alquiler de plataformas telescópicas" compiten por las mismas consultas genéricas). Cuatro páginas pilar de 1.800-2.500 palabras con tablas de especificaciones reales concentran esa autoridad y compiten mucho mejor.

**B) Contenido más rico, no menos.** No se elimina información: se traslada. Cada subcategoría se convierte en una **sección ancorada** con su tabla de especificaciones, sus fotos y su CTA. La página pilar es más larga y más útil que las 5 páginas delgadas que sustituye.

**C) Filtrado en lugar de navegación.** El usuario no quiere elegir entre "tijera" y "telescópica": quiere una máquina que llegue a 12 metros y quepa por una puerta de 90 cm. La página pilar incorpora un **filtro por altura de trabajo, capacidad de carga y tipo de motor** que resuelve la intención real. Eso no se puede construir con 5 páginas separadas.

**D) Un solo destino para las campañas.** Con 18 páginas de producto, una campaña de Ads tiene 18 destinos posibles y ninguno convierte. Con 4 pilares + 2 plantillas de landing, cada grupo de anuncios tiene un destino claro y medible.

**E) Menos mantenimiento.** 4 páginas que actualizar cuando cambia la flota, no 18.

**Riesgo y mitigación:** eliminar 14 URLs indexadas puede causar una caída temporal de tráfico orgánico. Mitigación: **301 permanentes de todas y cada una** de las URLs eliminadas hacia la sección ancorada correspondiente, mapa del sitio actualizado, envío a Search Console y monitorización de las 14 redirecciones durante 90 días. Con el mapeo bien hecho, la recuperación es de 4-8 semanas y el resultado neto positivo.

---

## 3. Qué se elimina y por qué

### 3.1 El blog sale del proyecto en la fase 1

**Estado actual:** 6 entradas, la última del 15/04/2025 (más de 15 meses sin publicar). Títulos con relleno geográfico evidente ("Obras Con Energía: Alquiler De Maquinaria En Málaga Con Grupos Electrógenos De Alta Potencia").

**Decisión:** se elimina `/noticias/` del menú y las 6 entradas se redirigen (301) a la página pilar correspondiente.

**Justificación honesta:** un blog abandonado resta credibilidad ("¿siguen operando?") y las 6 entradas actuales no generan ni tráfico ni autoridad. Reactivarlo requiere un compromiso editorial sostenido de 2-4 artículos al mes que ni el presupuesto ni el objetivo de este proyecto contemplan. Dedicar recursos a contenido de blog antes de tener un solo formulario funcionando sería invertir en el orden equivocado.

**Cuándo volver:** una vez que las campañas generen leads de forma estable y se conozca qué preguntas hacen realmente los prospectos, el blog vuelve como **`/recursos/`**: guías técnicas orientadas a la intención de compra ("¿Qué altura de plataforma necesito para trabajar a 10 metros?", "Alquilar o comprar carretilla: cuándo sale a cuenta cada opción"). Es la fase 2, y hay que decírselo al cliente con claridad para que no lo perciba como una pérdida.

### 3.2 `/otros-servicios/` se separa, no se elimina

Puertos, embalado siderúrgico y mantenimiento industrial son negocios reales con margen, pero:
- Tienen compradores distintos del alquiler
- Tienen ciclos de venta de meses, no de días
- Contaminan las audiencias de las campañas de alquiler si comparten formulario y píxel

**Decisión:** una sola página `/servicios-industriales/`, fuera del embudo de alquiler, con formulario propio y evento de conversión propio. Se enlaza desde el menú y desde el pie, pero **no** desde la home ni desde las páginas pilar.

### 3.3 El nivel intermedio de plataformas desaparece

`/alquiler-elevacion/alquiler-de-plataformas-elevadoras/` es una página que existe únicamente para contener a sus hijas. No aporta contenido propio y añade un clic entre el usuario y el producto. Se elimina.

---

## 4. La nueva página de inicio, bloque a bloque

**Objetivo único:** que el usuario pida presupuesto o llame en los primeros 15 segundos, y que si no lo hace, encuentre otras cinco oportunidades de hacerlo mientras baja.

**Alto objetivo en móvil: ≈ 5.500 px** (hoy: 10.185 px).

### Bloque 1 — HERO CON FORMULARIO
*El cambio más importante de todo el proyecto.*

```
┌───────────────────────────────────────────────────────────────┐
│  [Foto: plataforma articulada trabajando, operario con arnés]  │
│                                                                │
│  ALQUILER DE MAQUINARIA        ┌──────────────────────────┐   │
│  PARA OBRA E INDUSTRIA         │  PIDA SU PRESUPUESTO     │   │
│  EN TODA ESPAÑA                │  Respuesta en menos de 2h │   │
│                                │                          │   │
│  Más de 4.000 máquinas con     │  ¿Qué máquina necesita?▾ │   │
│  menos de 3 años de            │  Provincia            ▾ │   │
│  antigüedad media.             │  Teléfono               │   │
│  12 centros. Desde 1987.       │  Correo electrónico     │   │
│                                │  ☐ Acepto la política…  │   │
│  [ 📞 Llamar 91 361 31 31 ]    │  [ PEDIR PRESUPUESTO ]   │   │
│                                └──────────────────────────┘   │
└───────────────────────────────────────────────────────────────┘
```

- **Formulario visible sin hacer scroll.** 4 campos. No hay que hacer clic en nada para llegar a él.
- El vídeo de presentación **sale del hero** y baja al bloque 8. Un vídeo no es una conversión.
- En móvil, el formulario se coloca inmediatamente bajo el titular, no al final.
- Botón de llamada secundario, con el número visible (no "Contacto").

### Bloque 2 — BARRA DE CONFIANZA
```
Desde 1987  ·  +4.000 máquinas  ·  Antigüedad media <3 años  ·  12 centros  ·  ISO 9001·14001·45001  ·  IPAF  ·  ANAPAT
```
Franja de una línea, fondo `#1C3254`, texto blanco. Sin imágenes pesadas: los sellos ISO en SVG.

### Bloque 3 — SELECTOR POR NECESIDAD (no por categoría)

Cuatro tarjetas grandes que hablan el idioma del usuario, no el del catálogo:

| Tarjeta | Titular | Va a |
|---|---|---|
| 🔼 | **Trabajar en altura** — de 6 a 43 metros | Pilar 1 |
| 📦 | **Mover cargas** — hasta 16 toneladas | Pilar 2 |
| ⛏ | **Movimiento de tierras** — obra y reforma | Pilar 3 |
| ⚡ | **Energía e iluminación** — obra y eventos | Pilar 4 |

Cada tarjeta lleva su propio CTA: `Ver máquinas y precios`.

### Bloque 4 — CÓMO FUNCIONA (3 pasos)
Reduce la incertidumbre, que es la principal barrera de conversión en B2B.
```
1️⃣ Díganos qué necesita    2️⃣ Presupuesto en 2 horas    3️⃣ La máquina en su obra
   Si no sabe qué máquina       Precio cerrado con           Entrega en 24-48 h,
   le sirve, se lo decimos      transporte y seguro.         revisada y con manual.
   nosotros.                    Sin sorpresas.
```
*(Los plazos exactos deben confirmarse con el cliente antes de publicarse.)*

### Bloque 5 — MÁQUINAS MÁS ALQUILADAS
6 a 8 tarjetas de máquina (componente §9.4 del manual de marca), **con especificaciones visibles**: altura de trabajo, capacidad, peso, tipo de motor. CTA por tarjeta: `Pedir precio de esta máquina`.

Esto es lo que hoy no existe: el usuario ve la especificación sin descargar un PDF.

### Bloque 6 — PRUEBA SOCIAL
- 3 casos de éxito con cifras (obra, máquina, plazo, resultado)
- Banda de 8-12 logotipos de clientes
- 3 testimonios con nombre, cargo y empresa
- Puntuación media de Google si las fichas están verificadas

**Requiere material del cliente.** Es el bloque con más impacto de conversión de la página y el único que no podemos escribir nosotros solos.

### Bloque 7 — COBERTURA NACIONAL
Mapa de España con los 12 centros marcados + selector de provincia. Al elegir provincia: dirección, teléfono directo, horario y botón `Pedir presupuesto a esta sede`.

Es el argumento diferencial de JOFEMESA convertido en herramienta de conversión.

### Bloque 8 — POR QUÉ JOFEMESA
Cuatro diferenciales con prueba, no con adjetivos:

| Diferencial | Prueba |
|---|---|
| Flota con menos de 3 años | Antigüedad media documentada, revisión antes de cada salida |
| Servicio técnico propio | Taller en las 12 instalaciones, no red de terceros |
| Seguridad certificada | ISO 45001, IPAF, manual de seguridad con cada equipo |
| 39 años asesorando | Desde 1987. Le decimos qué máquina necesita antes de alquilársela |

Aquí se coloca el **vídeo de presentación**.

### Bloque 9 — PREGUNTAS FRECUENTES
Las 8 preguntas del §4.4 del manual de marca. Acordeón, con marcado `FAQPage` de Schema.org (elegible para aparecer en resultados enriquecidos y en respuestas de IA).

### Bloque 10 — CTA FINAL
Franja `#1C3254` a ancho completo con el formulario repetido (los mismos 4 campos) + teléfono + WhatsApp.

### Bloque 11 — PIE COMPACTO
4 columnas: Alquiler (4 pilares) · Empresa · Sedes (12 enlaces) · Contacto y legales. Sellos de certificación. Redes.

**Se elimina del pie** la lista completa de 18 subcategorías que hay hoy.

### Componente fijo — BARRA DE ACCIÓN EN MÓVIL
`[📞 Llamar] [💬 WhatsApp] [Pedir presupuesto]` fija en la parte inferior, en todas las páginas, por debajo de 768 px.

---

## 5. Plantilla de página pilar

Se aplica a los 4 pilares. Es la plantilla que soporta la mayoría del tráfico orgánico y de pago.

| # | Bloque | Contenido |
|---|---|---|
| 1 | **Hero + formulario lateral fijo** | H1 específico del pilar + 3 datos + formulario de 4 campos que acompaña al scroll en escritorio |
| 2 | Barra de confianza | La misma de la home |
| 3 | **Filtro de máquinas** | Altura de trabajo · Capacidad de carga · Tipo de motor (eléctrico/diésel/híbrido) · Ancho de paso |
| 4 | **Tabla / cuadrícula de máquinas** | Todas las subcategorías como secciones ancoradas. **Especificaciones en HTML, no en PDF.** CTA por fila. |
| 5 | Aplicaciones y sectores | ¿Para qué sirve cada tipo? Fachadas, naves, mantenimiento industrial, eventos, poda… |
| 6 | Guía de elección | "¿Qué plataforma necesito?" — tabla altura de trabajo → tipo recomendado → limitaciones de acceso |
| 7 | Seguridad y normativa | ISO 45001, IPAF, formación de operador, manual de cada equipo, revisiones |
| 8 | Cobertura | Los 12 centros que sirven este pilar + selector de provincia |
| 9 | FAQ específica del pilar | 6-8 preguntas propias, con `FAQPage` schema |
| 10 | CTA final | Formulario repetido |

**Longitud objetivo:** 1.800-2.500 palabras de contenido real y específico por pilar. Hoy: 400-450 palabras genéricas por subpágina.

**El trabajo de contenido crítico:** extraer las especificaciones de los 12+ PDF de fichas técnicas y volcarlas a tablas HTML. Es el mayor esfuerzo del proyecto y el que produce más retorno simultáneo (SEO + conversión + visibilidad en IA).

---

## 6. Plantillas de landing de campaña

Las landings **no son páginas de la web**. Están fuera del menú, tienen una sola salida y existen solo para convertir tráfico pagado.

### 6.1 Reglas de la landing

| Regla | Motivo |
|---|---|
| **Sin menú de navegación** | Solo logotipo + teléfono. Cada enlace de salida es una fuga de conversión. |
| **Ratio de atención 1:1** | Un único objetivo por página. Un formulario, un teléfono, un WhatsApp. Nada más. |
| **Formulario sobre la línea de flotación** | Sin excepciones, en móvil y en escritorio. |
| **Correspondencia de mensaje** | El H1 repite literalmente la consulta del anuncio. Si el anuncio dice "Alquiler de plataformas elevadoras en Málaga", el H1 lo dice igual. Sube el nivel de calidad y baja el CPC. |
| **Longitud máxima** | 6 bloques. No más. |
| **Sin pie completo** | Solo enlaces legales. |
| **Velocidad prioritaria** | LCP objetivo < 2,0 s. Es tráfico pagado: cada décima cuesta dinero. |

### 6.2 Estructura de la landing (6 bloques)

```
1. HERO ......... H1 = consulta del anuncio · 3 datos de prueba · FORMULARIO · teléfono
2. CONFIANZA .... 1987 · +4.000 máquinas · <3 años · ISO · IPAF · ANAPAT
3. LA OFERTA .... 4-6 máquinas con especificaciones + "Pedir precio"
4. PRUEBA ....... 2 testimonios + logos de clientes + "sede en [ciudad]"
5. FAQ .......... 5 objeciones: precio, plazo, transporte, formación, mínimo de días
6. CIERRE ....... Formulario repetido + teléfono + WhatsApp
```

### 6.3 Las 2 plantillas y sus 7+ variantes geográficas

| Plantilla | Variantes de ciudad | Campaña |
|---|---|---|
| **LP-1: Alquiler de plataformas elevadoras** | Madrid · Valencia · Alicante · Castellón · Málaga · Sevilla · Valladolid · Asturias | Google Ads Búsqueda (intención alta) |
| **LP-2: Alquiler de maquinaria de obra** | Las mismas 8 | Google Ads Búsqueda + Meta (retargeting) |

Cada variante cambia: H1, ciudad en el copy, sede y teléfono locales, foto local si existe, y testimonios de la zona si existen. El resto es idéntico.

**Estas 8+8 variantes se generan a partir de 2 plantillas**, no se diseñan una a una. Es el mismo esfuerzo de diseño con 16 destinos de campaña.

### 6.4 Página de agradecimiento — `/gracias/`

Obligatoria. Es el disparador del evento de conversión. Contenido:
- Confirmación: "Hemos recibido su solicitud. Le llamamos en menos de 2 horas."
- Teléfono directo de su sede, por si prefiere llamar ya
- Descarga del catálogo de flota (recompensa inmediata + segunda micro-conversión)
- Cualificación adicional opcional: fecha de inicio, duración estimada, nombre de la obra
- `noindex, nofollow`

---

## 7. Plan de medición — sin esto no hay campañas

Este es el capítulo que convierte el rediseño en una inversión medible. Hoy JOFEMESA tiene **cero** de todo lo que sigue.

### 7.1 Infraestructura

| Herramienta | Función |
|---|---|
| **Google Tag Manager** | Contenedor único. Todo se dispara desde aquí. |
| **Google Analytics 4** | Analítica y audiencias |
| **Google Ads** — etiqueta de conversión | Optimización de puja |
| **Meta Pixel + Conversions API** | Seguimiento en Meta con resiliencia a bloqueos de navegador |
| **Consent Mode v2** | **Obligatorio legalmente en España.** Sin esto, riesgo de sanción y pérdida de datos en Google. |
| **Banner de cookies conforme al RGPD** | Rechazo tan fácil como aceptación, granular por finalidad |
| **LinkedIn Insight Tag** | Opcional, útil para el perfil de compras B2B |
| **Microsoft Clarity o Hotjar** | Mapas de calor y grabaciones. Coste cero (Clarity) y valor altísimo para las primeras optimizaciones. |

### 7.2 Eventos de conversión a configurar

| Evento | Disparador | Valor asignado | Prioridad |
|---|---|---|---|
| `lead_presupuesto` | Envío del formulario principal → `/gracias/` | 🔴 Principal | Alta |
| `lead_sede` | Envío del formulario de una sede | 🔴 Principal | Alta |
| `click_telefono` | Clic en cualquier `tel:` | 🟠 Secundario | Alta |
| `click_whatsapp` | Clic en el botón de WhatsApp | 🟠 Secundario | Alta |
| `descarga_catalogo` | Formulario del catálogo enviado | 🟡 Micro | Media |
| `descarga_ficha_tecnica` | Clic en un PDF de ficha técnica | 🟡 Micro | Media |
| `lead_venta` | Formulario de la página de venta | 🟠 Secundario | Media |
| `lead_industrial` | Formulario de servicios industriales | 🟠 Secundario | Media |
| `scroll_75` | 75 % de la página | ⚪ Interacción | Baja |
| `ver_video` | Reproducción del vídeo | ⚪ Interacción | Baja |

**Nota sobre la asignación de valor:** hay que acordar con el cliente un valor monetario estimado por tipo de lead (por ejemplo, un lead de plataforma para larga duración vale más que uno de miniexcavadora de fin de semana). Sin valores, Google Ads optimiza a volumen de leads, no a valor. Con valores, optimiza a facturación.

### 7.3 Enrutado de leads

Cada formulario incluye un campo oculto con la **sede de destino**, calculado a partir de la provincia seleccionada. El lead llega:
1. Al correo de la delegación correspondiente
2. Al correo central (`jofemesa@jofemesa.com`) como copia
3. A una hoja de cálculo o CRM, con marca de tiempo, origen (`utm_source`, `utm_campaign`), página de entrada y consentimiento registrado

Sin este enrutado, un lead de Málaga llega a Madrid y se pierde el tiempo de respuesta, que es el factor número uno de cierre en alquiler de maquinaria.

### 7.4 Seguimiento de llamadas

En este sector, una parte importante de los leads llega por teléfono. Recomendación mínima viable:
- **Números de reenvío de Google** en las campañas de Búsqueda (gratis, nativo en Google Ads)
- Enlaces `tel:` con evento de GTM en toda la web
- **Y arreglar el `tel:034985985212` roto de la cabecera actual** antes que nada

Opcional en fase 2: plataforma de *call tracking* con número único por canal, que permite atribuir cada llamada a su campaña y palabra clave.

### 7.5 Panel de control

Un panel de Looker Studio, actualizado a diario, con:
- Leads totales por mes, por fuente y por tipo
- Coste por lead por campaña
- Leads por sede
- Tasa de conversión por página
- Core Web Vitals
- Palabras clave que generan leads (no solo clics)

---

## 8. Objetivos técnicos de rendimiento

| Métrica | Hoy (medido) | Objetivo | Cómo |
|---|---|---|---|
| **LCP** | > 8 s (est.) | **< 2,5 s** | Imagen del hero en AVIF con `fetchpriority=high`, CSS crítico en línea, fuentes autoalojadas con preload |
| **INP** | — | < 200 ms | Reducción de JS, eliminación de Huger Elementor |
| **CLS** | — | < 0,1 | `width`/`height` en todas las imágenes, reserva de espacio para el banner de cookies |
| **Carga completa** | 13,2 s | **< 3,5 s** | Suma de todo lo anterior |
| **Peso total** | 2.856 KB | **< 900 KB** | Ver desglose |
| **Ficheros CSS** | 24 (1.989 KB) | **≤ 3 (< 150 KB)** | Elementor con CSS optimizado, purga de estilos no usados, un único fichero por plantilla |
| **Ficheros JS** | 24 (158 KB) | ≤ 8 (< 90 KB) | Eliminar Huger Elementor, jQuery Migrate, animaciones decorativas |
| **Peticiones HTTP** | 108 | **< 45** | Consolidación de CSS/JS, iconos en SVG en línea, fuentes autoalojadas |
| **TTFB** | 1.126 ms | < 400 ms | Caché de página + CDN + revisión de alojamiento |
| **Imágenes** | 632 KB, 0 % con `alt` | < 400 KB, 100 % con `alt` | AVIF/WebP, dimensiones correctas, lazy-load selectivo |
| **Widgets Elementor por página** | 135 | < 60 | Plantillas reutilizables en lugar de construcción widget a widget |

### 8.1 Acciones concretas

1. **Purgar hojas de estilo.** 24 ficheros CSS es el resultado de que Elementor cargue una hoja por widget y una por página. Se resuelve activando el CSS optimizado de Elementor, purgando estilos no utilizados y consolidando en un fichero por plantilla.
2. **Eliminar Huger Elementor.** El mega-menú de 20 entradas desaparece; con él, su CSS y su JS.
3. **Eliminar Font Awesome (3 variantes).** Sustituido por SVG en línea.
4. **Autoalojar las 6 fuentes.** Elimina peticiones a Google y mejora el cumplimiento del RGPD.
5. **Eliminar las animaciones decorativas** (`zoomIn`, `fadeInRight`, `e-animation-grow`) y su CSS.
6. **Reprocesar el 100 % de las imágenes:** AVIF con fallback WebP, servidas al tamaño mostrado, `alt` descriptivo, nombre de fichero semántico.
7. **Caché de página + CDN.**
8. **Eliminar el contenido duplicado de la home** (secciones repetidas y el bloque de noticias renderizado dos veces).
9. **Arreglar el logotipo y el logo de ANAPAT**, que hoy no cargan correctamente.

---

## 9. SEO técnico y datos estructurados

### 9.1 Marcado Schema.org a implementar (hoy: ninguno)

| Tipo | Dónde | Qué habilita |
|---|---|---|
| `Organization` | Global | Panel de conocimiento, autoridad de marca |
| `LocalBusiness` × 12 | Una por sede | Posicionamiento local, aparición en el mapa |
| `Product` / `Offer` | Cada máquina de las páginas pilar | Resultados enriquecidos, comparadores |
| `FAQPage` | Home, 4 pilares, landings | Resultados enriquecidos y respuestas de IA |
| `BreadcrumbList` | Todas | Migas en el resultado de búsqueda |
| `WebSite` + `SearchAction` | Global | Caja de búsqueda en Google |

### 9.2 Correcciones obligatorias

- ✅ Retirar `noindex, nofollow` en el lanzamiento
- ✅ `<title>` de 55-60 caracteres, únicos (hoy la home tiene 139 caracteres de relleno)
- ✅ `<meta description>` propia de 150-155 caracteres por página
- ✅ `alt` en el 100 % de las imágenes (hoy: 0 %)
- ✅ Nombres de fichero de imagen semánticos
- ✅ Jerarquía correcta de encabezados: un H1, H2 de sección, H3 de bloque, sin saltos
- ✅ Mapa del sitio XML + `robots.txt` correcto
- ✅ Canónicas autorreferenciales
- ✅ Las 14 redirecciones 301 mapeadas y verificadas
- ✅ `hreflang` si se activa versión en portugués (Portugal está en el ámbito comercial)

### 9.3 Optimización para búsqueda con IA

Las especificaciones en HTML (en lugar de en PDF), el marcado `FAQPage` y las tablas de datos estructuradas hacen que JOFEMESA sea citable por ChatGPT, Perplexity y las AI Overviews de Google. Hoy, con toda la información técnica en PDF, es invisible en ese canal.

Es una ventaja de primer movimiento en un sector donde ningún competidor lo está haciendo todavía.

---

## 10. Cumplimiento legal (España / RGPD)

| Requisito | Estado hoy | Acción |
|---|---|---|
| Aviso legal | 🔴 Enlazado en el pie pero sin página propia detectada | Crear |
| Política de privacidad | 🟢 Existe (`/politica-privacidad/`) | Actualizar para cubrir los nuevos formularios |
| Política de cookies | 🔴 Enlazada, sin página | Crear |
| Banner de cookies conforme | 🔴 No detectado | Implementar con rechazo tan accesible como la aceptación, granular por finalidad |
| **Consent Mode v2** | 🔴 No | Obligatorio para operar con Google Ads en el EEE |
| Consentimiento en formularios | 🔴 No hay formularios | Casilla no premarcada + finalidad + enlace a la política |
| Registro de consentimientos | 🔴 | Marca de tiempo, IP y texto aceptado, almacenados |
| Información al interesado | 🔴 | Responsable, finalidad, base jurídica, plazo de conservación y derechos en cada formulario |

**Nota:** el cumplimiento no es un extra opcional. Sin Consent Mode v2 correctamente implementado, Google restringe el uso de datos para audiencias y remarketing en el EEE, lo que degrada directamente el rendimiento de las campañas.

---

## 11. Plan de lanzamiento por fases

### FASE 0 — Preparación (semana 0)
- Recopilación de material del cliente: logos de clientes, testimonios, casos, marcas, horarios de las 12 sedes, compromiso de plazo publicable
- Accesos: WordPress, alojamiento, DNS, Google Ads, Analytics, Search Console
- **Quick win inmediato: arreglar el `tel:` roto de la cabecera** — 10 minutos de trabajo, efecto inmediato

### FASE 1 — Fundamentos (semanas 1-2)
- Manual de marca aplicado: variables CSS, tipografías, sistema de componentes
- Diseño de las 5 plantillas: Home · Pilar · Landing · Sedes · Contacto/Gracias
- Validación con el cliente antes de maquetar

### FASE 2 — Construcción (semanas 3-5)
- Maquetación de las 16 URLs
- Redacción orientada a conversión
- **Extracción de especificaciones de los PDF a tablas HTML** (el trabajo más pesado)
- 6 formularios con enrutado por sede
- Reprocesado de imágenes

### FASE 3 — Medición y campañas (semana 5-6)
- GTM + GA4 + Consent Mode v2 + banner de cookies
- 10 eventos de conversión
- Meta Pixel + CAPI
- Las 2 landings + variantes de ciudad
- Panel de Looker Studio

### FASE 4 — Optimización técnica (semana 6)
- Purga de CSS/JS, caché, CDN
- Core Web Vitals hasta objetivo
- Schema.org
- Accesibilidad (WCAG 2.1 AA)

### FASE 5 — Lanzamiento (semana 7)
- Las 14 redirecciones 301 verificadas una a una
- Retirada de `noindex`
- Mapa del sitio a Search Console
- Verificación de los 10 eventos en producción
- Prueba de los 6 formularios en 3 navegadores y 2 dispositivos

### FASE 6 — Monitorización y ajuste (semanas 8-11, 30 días posteriores)
- Vigilancia de las 301 y de las posiciones
- Mapas de calor con Clarity
- Primeras optimizaciones de conversión basadas en datos reales
- Formación al equipo del cliente

---

## 12. Resumen de la transformación

| | Hoy | Después |
|---|---|---|
| **Formularios** | 0 | 6 |
| **Eventos de conversión** | 0 | 10 |
| **Leads trazables** | 0 | 25-40/mes (objetivo) |
| **Destinos de campaña** | 0 | 2 plantillas × 8 ciudades = 16 |
| **URLs** | 24 páginas + 6 posts | 16 + 2 landings + gracias |
| **Entradas de menú** | 20 | 6 |
| **Carga completa** | 13,2 s | < 3,5 s |
| **Peso** | 2.856 KB | < 900 KB |
| **CSS** | 24 ficheros / 1.989 KB | ≤ 3 / < 150 KB |
| **Alto de home en móvil** | 10.185 px | ≈ 5.500 px |
| **CTA fijo en móvil** | No | Sí (llamar · WhatsApp · presupuesto) |
| **WhatsApp** | No | Sí |
| **Especificaciones técnicas** | En 12 PDF | En HTML, filtrables |
| **Imágenes con `alt`** | 0 % | 100 % |
| **Datos estructurados** | 0 | 6 tipos, 16 páginas |
| **Páginas de captación local** | 0 | 8 landings de ciudad |
| **Consent Mode v2** | No | Sí |
| **Panel de leads** | No | Looker Studio diario |

---

*Documento 3 de 4. Continúa en `04-Propuesta-Comercial-LeadadGo.md`.*
