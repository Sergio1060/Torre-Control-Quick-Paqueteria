# Panel de Entregas

Tablero BI de servicios de entrega (KPIs, distribución por estado, cliente, ciudad de destino y tendencia creados vs. finalizados), construido en HTML/CSS/JS puro — sin backend ni build step.

## Archivos

- `index.html` — el tablero completo.
- `servicios.json` — datos de muestra que se cargan si no hay ningún CSV subido en el navegador.
- `recolectado.json` — mapa guía → fecha de recolección (extraído de la hoja de Google Sheets de control), usado para corregir "Fecha de creación" cuando el CSV del día trae ese dato mal o vacío. Las guías que no aparecen ahí conservan su fecha original.

## Actualizar los datos a diario

Abre la página y usa el botón **"Cargar CSV del día"** para seleccionar el export diario (mismo formato: separado por `;`, con las columnas `Estado`, `Cliente`, `CEDI`, `Ciudad`, `Fecha de creacion`, `finalizado`, etc.). El archivo se procesa en el navegador — no se sube a ningún servidor — y el tablero recuerda el último archivo cargado en ese navegador (vía `localStorage`).

## Cliente unificado (CEDI)

El filtro "Cliente" y el gráfico "Servicios por cliente" agrupan todos los CEDI de una misma marca bajo un único nombre (p. ej. `CEDI LOREAL BOGOTA`, `CEDI LOREAL MEDELLIN` y `LOREAL SANTANDER` se unifican como `LOREAL`). La columna "Cliente" de las tablas muestra ese nombre unificado; el CEDI original queda visible al pasar el cursor sobre la celda.

## Publicar en GitHub Pages

1. Crea un repositorio en GitHub y sube estos archivos (`index.html`, `servicios.json`, este `README.md`).
2. En **Settings → Pages**, elige la rama `main` y la carpeta `/ (root)`.
3. GitHub publicará el sitio en `https://<usuario>.github.io/<repositorio>/`.
