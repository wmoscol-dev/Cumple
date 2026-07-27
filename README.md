# Cumples Yape · Control de Recaudo Avanzado

Aplicación web progresiva (PWA) para gestionar colectas de cumpleaños mediante **Yape** (Perú).

## Funcionalidades

- **Carga de Excel** — Lee archivos `.xlsx` con hojas por grupo/categoría. Detecta columnas automáticamente: nombre, fecha, estado, teléfono, cuota, mora.
- **Pestañas múltiples** — Cada hoja del Excel (excepto "otros") se convierte en una pestaña navegable.
- **Gestión de estados por persona:**
  - **Pagó (1)** — Marca con toggle; calcula cuota + mora acumulada.
  - **No pagó (2)** — Pendiente; mora sigue corriendo.
  - **Cumpleañero (0)** — Doble click en el toggle; muestra corona, candado y "Recibe".
- **Mora automática** — Se calcula `moraPorDia * díasDesdeElCumpleaños` para cada pendiente.
- **Progreso visual** — Barra de progreso, porcentaje recaudado, contador de pagos.
- **Exportar imagen** — Genera PNG del resumen limpio (sin UI) con número Yape del cumpleañero.
- **Recordatorios vía WhatsApp** — Enlace directo a `wa.me` con mensaje personalizado.
- **Persistencia automática:**
  1. File System Access API (guarda directo al archivo original).
  2. Servidor local (`localhost:8765`) como respaldo.
  3. Descarga del archivo modificado como fallback.
- **Próximos cumpleaños** — Banner con los cumpleaños más cercanos y botón de recordatorio.
- **Modo offline** — Service Worker registrado para funcionar sin conexión.

## Tecnologías

- Vanilla JS (sin frameworks)
- [XLSX.js](https://cdn.jsdelivr.net/npm/xlsx) — lectura/escritura de Excel
- [html2canvas](https://cdn.jsdelivr.net/npm/html2canvas) — captura de pantalla
- Google Fonts (Sora, Inter, JetBrains Mono)
- Service Worker para offline

## Uso

1. Abrir `index.html` en un navegador moderno (Chrome recomendado).
2. Click en **"Excel"** (arriba a la derecha) y seleccionar un archivo `.xlsx`.
3. Navegar entre pestañas y gestionar estados.
4. Usar botones inferiores para copiar número Yape o enviar recordatorio.

## Estructura del Excel

Cada hoja debe contener filas con columnas detectables por nombre:

| Nombre | Fecha | Estado | Teléfono | Cuota | Mora |
|--------|-------|--------|----------|-------|------|

- La hoja **"otros"** se ignora como pestaña y se usa para configurar cuotas y mora por día por pestaña.
- **Estado:** `0` = cumpleañero, `1` = pagó, `2` = no pagó.
