# Sitio web de MetisOps

Sitio estático en español, inglés y portugués: `index.html` (portada, servicios, quiénes somos y contacto) y `pulso.html` (Pulso económico: indicadores y noticias). Ambos comparten el mismo código; el atributo `data-page` del `<html>` decide qué secciones se muestran.

Foto de portada: `hero-santiago-torre-*.jpg/webp` (foto de Gerald, editada).

## Qué se actualiza y cómo

- **Indicadores de Chile** (dólar, euro, UF, UTM, IPC, TPM, cobre, Imacec, desempleo): el navegador de cada visitante los consulta en vivo en `https://mindicador.cl/api`. Si esa fuente no responde, se muestran los valores de `fallback` de `data.json`.
- **Precios internacionales, divisas y noticias**: se leen de `data.json`. Una tarea programada lo actualiza cada día y hace commit en este repositorio; el hosting publica el cambio solo.

## Formato de `data.json`

```json
{
  "actualizado": "AAAA-MM-DD",
  "fallback": { "dolar": { "valor": 0, "fecha": "AAAA-MM-DD" }, "...": {} },
  "commodities": [
    { "nombre": { "es": "", "en": "", "pt": "" }, "valor": 0, "fecha": "AAAA-MM-DD", "fuente": "" }
  ],
  "fx": [
    { "codigo": "EUR", "clp": 0, "moneda": { "es": "", "en": "", "pt": "" } }
  ],
  "semana": {
    "desde": "AAAA-MM-DD", "tema": "",
    "pregunta": { "es": "", "en": "", "pt": "" },
    "post_url": "https://www.linkedin.com/... (opcional)"
  },
  "news": [
    { "fecha": "AAAA-MM-DD", "fuente": "", "url": "https://...",
      "tema": { "es": "", "en": "", "pt": "" },
      "titular": { "es": "", "en": "", "pt": "" },
      "resumen": { "es": "", "en": "", "pt": "" } }
  ]
}
```

`semana` es la pregunta de la semana que encabeza el sitio: la pregunta de cierre del post de LinkedIn de esa semana. Solo cambia cuando hay un post nuevo.

Claves de `fallback`: `dolar`, `euro`, `uf`, `utm`, `ipc`, `tpm`, `libra_cobre`, `imacec`, `tasa_desempleo`.
Las `url` de noticias deben empezar con `https://`. Los textos se muestran como texto plano.

## Reglas editoriales

- Solo datos de fuentes públicas verificables, con su fuente y fecha. Nunca inventar cifras.
- No usar información de Fosfoquim ni de sus clientes, proveedores o transportistas.
- Noticias: 6, de los últimos 7 días, sobre economía chilena, minería, logística, comercio exterior, energía y combustibles.

## Publicaciones en la portada (`publicaciones`)

Lista de hasta 4 publicaciones de LinkedIn, la más reciente primero. La portada las muestra rotando cada 8 segundos (la primera con el rótulo "Pregunta de la semana"; las demás con "Publicación · fecha").

```json
"publicaciones": [
  { "fecha": "AAAA-MM-DD", "texto": { "es": "", "en": "", "pt": "" }, "url": "https://www.linkedin.com/feed/update/urn:li:activity:..." }
]
```

`texto` es la pregunta de cierre del post o su titular. `url` debe empezar con `https://www.linkedin.com/` o `https://lnkd.in/` (si no, el enlace se oculta). Si la lista falta o está vacía, la portada usa `semana`.
