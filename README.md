# Panel de Entregas

Tablero BI de servicios de entrega (KPIs, distribución por estado, cliente, ciudad de destino y tendencia creados vs. finalizados), construido en HTML/CSS/JS puro — sin backend ni build step.

## Archivos

- `index.html` — el tablero completo.
- `servicios.json` — el dataset **compartido**: lo que ve cualquiera que abra el link sin haber subido nada. Es la fuente de verdad para todo el equipo.
- `recolectado.json` — mapa guía → fecha de recolección (extraído de la hoja de Google Sheets de control), usado para corregir "Fecha de creación" cuando el CSV del día trae ese dato mal o vacío. Las guías que no aparecen ahí conservan su fecha original.
- `entregas_coordinadora.json` — mapa guía → fecha real de entrega para las guías que Coordinadora ampara (consultado en coordinadora.com/rastreo). Al cargar cualquier CSV, esas guías se marcan como "Finalizado" con su fecha real. Solo incluye guías que Coordinadora ya reporta como "Entregado"; las que siguen en tránsito no se tocan.

## Actualizar los datos a diario

Hay dos formas de actualizar, y **no son lo mismo**:

- **Para todo el equipo** (recomendado): envía el CSV del día a Claude para que lo revise, aplique las correcciones (recolectado/Coordinadora) y reemplace `servicios.json`. Al hacer `git push`, GitHub Pages se reconstruye solo en 1-2 minutos y esa es la versión que ve cualquiera que abra el link sin haber subido nada.
- **Solo para vista local**: el botón **"Cargar CSV del día"** en la página deja subir un archivo directamente en el navegador (mismo formato: separado por `;`, con las columnas `Estado`, `Cliente`, `CEDI`, `Ciudad`, `Fecha de creacion`, `finalizado`, etc.). Se procesa ahí mismo — no se sube a ningún servidor — y el tablero lo recuerda solo en ese navegador (vía `localStorage`). **Nadie más lo ve.** Sirve para previsualizar antes de mandarlo, o para revisar un archivo puntual sin afectar lo que ve el resto.

## Cliente unificado (CEDI)

El filtro "Cliente" y el gráfico "Servicios por cliente" agrupan todos los CEDI de una misma marca bajo un único nombre (p. ej. `CEDI LOREAL BOGOTA`, `CEDI LOREAL MEDELLIN` y `LOREAL SANTANDER` se unifican como `LOREAL`). La columna "Cliente" de las tablas muestra ese nombre unificado; el CEDI original queda visible al pasar el cursor sobre la celda.

## Publicar en GitHub Pages

1. Crea un repositorio en GitHub y sube estos archivos (`index.html`, `servicios.json`, este `README.md`).
2. En **Settings → Pages**, elige la rama `main` y la carpeta `/ (root)`.
3. GitHub publicará el sitio en `https://<usuario>.github.io/<repositorio>/`.
