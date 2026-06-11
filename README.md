# Tablero · Clientes Se Lo Lleva

Tablero web estático que muestra las entregas de **Clientes Se Lo Lleva**, con KPIs, gráficos, filtros y **alertas para fechas con más de 15 días de antigüedad**.

## Archivos

- `index.html` — el tablero (todo en un solo archivo, sin build).
- `data.json` — datos que alimentan el tablero. Se regenera importando un Excel.
- `CLIENTES SE LO LLEVA - PROCESADO.xlsx` — Excel base con la información consolidada.

## Cómo publicarlo en GitHub Pages

1. Crea un repositorio en GitHub (puede ser privado o público).
2. Sube estos tres archivos a la raíz del repo (`index.html`, `data.json`, y opcionalmente el `.xlsx`).
3. Ve a **Settings → Pages**.
4. En **Source** elige la rama (`main`) y carpeta `/ (root)` → **Save**.
5. En 1–2 minutos tendrás la URL: `https://<usuario>.github.io/<repo>/`.

## Cómo actualizar los datos

Tienes tres caminos, de más automático a más manual:

### Opción A — Reemplazar `data.json` en el repo (recomendado)
1. En tu PC, abre el tablero localmente o publicado.
2. Click en **Importar Excel** y selecciona el nuevo `.xlsx`.
3. Click en **Descargar JSON** → se baja un `data.json` actualizado.
4. Sube ese `data.json` al repo (drag & drop en GitHub o `git push`).
5. El tablero se actualiza solo al abrirlo (botón **Recargar data.json**).

### Opción B — Importar manualmente sin tocar el repo
- Solo abre el tablero y usa **Importar Excel** o **Importar JSON**. Útil para revisar datos sin publicarlos.

### Opción C — Trabajar offline
- Descarga `index.html` y `data.json` a una carpeta y abre `index.html` directamente. Funciona sin servidor (al abrir local con `file://` puede que la carga automática de `data.json` falle por CORS; en ese caso usa **Importar JSON**).

## Funcionalidades

- **KPIs**: total registros, alertas (>15 días), por vencer (8–15), al día (≤7).
- **Gráfico de barras**: top 12 tiendas por número de entregas.
- **Gráfico de torta**: distribución por zona.
- **Tabla filtrable**: búsqueda libre + filtro por tienda, zona y estado.
- **Alertas visuales**: filas con fechas >15 días se resaltan en rojo y se etiquetan automáticamente.
- **Import/Export**: Excel (.xlsx) ↔ JSON.

## Estructura del JSON

```json
{
  "generatedAt": "2026-06-11T00:00:00Z",
  "columns": ["Transportes","y","entregas","StatusGlob","Entrg.ext.","Cl.entrega","Tienda","RutaTransp","Zona","Nombre","Fe.picking","Fe.entrega"],
  "rows": [
    { "Transportes": 84047681, "Tienda": "ALMACEN METROPOLITANO", "Fe.entrega": "2026-06-08", "...": "..." }
  ]
}
```

Las fechas se guardan en formato `YYYY-MM-DD`.

## Tecnología

100% estático, sin backend ni build:
- **SheetJS** para leer Excel en el navegador
- **Chart.js** para los gráficos
- HTML/CSS/JS puro
