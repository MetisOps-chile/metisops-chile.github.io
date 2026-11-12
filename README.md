# Sitio web de MetisOps

Sitio estático de una sola página (`index.html`) en español, inglés y portugués.

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
  "news": [
    { "fecha": "AAAA-MM-DD", "fuente": "", "url": "https://...",
      "tema": { "es": "", "en": "", "pt": "" },
      "titular": { "es": "", "en": "", "pt": "" },
      "resumen": { "es": "", "en": "", "pt": "" } }
  ]
}
```

Claves de `fallback`: `dolar`, `euro`, `uf`, `utm`, `ipc`, `tpm`, `libra_cobre`, `imacec`, `tasa_desempleo`.
Las `url` de noticias deben empezar con `https://`. Los textos se muestran como texto plano.

## Reglas editoriales

- Solo datos de fuentes públicas verificables, con su fuente y fecha. Nunca inventar cifras.
- No usar información de Fosfoquim ni de sus clientes, proveedores o transportistas.
- Noticias: 6, de los últimos 7 días, sobre economía chilena, minería, logística, comercio exterior, energía y combustibles.
