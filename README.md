# Tablero · Clientes Se Lo Lleva

Tablero web estático con KPIs, gráficos, filtros y **alertas para entregas con más de 15 días de antigüedad**.

## Archivos

- `index.html` — el tablero (todo en un solo archivo, sin build).
- `data.json` — datos que alimentan el tablero. Se regenera importando un Excel.
- `CLIENTES SE LO LLEVA - PROCESADO.xlsx` — Excel base con la información consolidada.

## Catálogo de tiendas dentro del código

El mapeo de **código → nombre de tienda** vive dentro de `index.html`, en la constante `TIENDA_MAP` (al inicio del bloque `<script>`).
El tablero **siempre** recalcula la columna `Tienda` a partir de `Cl.entrega` usando ese catálogo — incluso si el `data.json` trae nombres viejos.

Para agregar o cambiar una tienda, edita esa lista. Ejemplo actual:

```js
const TIENDA_MAP = {
  3000: 'ALMACEN PRINCIPAL',
  3001: 'ALMACEN HIPER',
  3002: 'ALMACEN NORTE',
  3004: 'ALMACEN SANTA MARTA',
  // ... resto
};
```

Hacer un cambio aquí y subirlo al repo basta — no hace falta regenerar `data.json`.

## Publicar en GitHub Pages

1. Crea un repositorio en GitHub.
2. Sube `index.html`, `data.json` (y opcionalmente el `.xlsx`) a la raíz.
3. **Settings → Pages** → Source = `main`, carpeta `/ (root)` → Save.
4. En 1–2 minutos la URL será `https://<usuario>.github.io/<repo>/`.

## Actualizar los datos

### Opción A — Reemplazar `data.json` (recomendado)
1. Abre el tablero (local o publicado).
2. Click **Importar Excel** → selecciona el nuevo `.xlsx`.
3. Click **Descargar JSON** → se baja un `data.json` actualizado.
4. Sube ese `data.json` al repo (drag & drop o `git push`).
5. El tablero se actualiza al recargar.

### Opción B — Solo revisar sin tocar el repo
- Usa **Importar Excel** o **Importar JSON** dentro del tablero. Los cambios viven solo en tu navegador.

## Funcionalidades

- **KPIs**: total registros, alertas (>15 días), por vencer (8–15), al día (≤7).
- **Gráfico de barras**: top 12 tiendas por número de entregas.
- **Gráfico de torta**: distribución por zona.
- **Tabla filtrable**: búsqueda libre + filtro por tienda, zona y estado.
- **Alertas visuales**: filas con fechas >15 días se resaltan en rojo y se etiquetan automáticamente.
- **Import/Export**: Excel (.xlsx) ↔ JSON.
- **Re-mapeo automático de tiendas**: usa `TIENDA_MAP` del código sobre cualquier dataset cargado.

## Importar Excel "crudo"

El tablero detecta el formato original (con nombres separados en columnas I–M y fechas en `DD.MM.YYYY`) y lo normaliza automáticamente al importarlo: combina los nombres, llena `Tienda` desde `Cl.entrega`, y convierte las fechas.

## Tecnología

100% estático, sin backend ni build: SheetJS (lectura de Excel) + Chart.js (gráficos) + HTML/CSS/JS puro.
