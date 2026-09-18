# Disney 2027 · Cuenta atrás para Disneyland Paris

Página web estática de cuenta atrás para el viaje a Disneyland París el **14 de noviembre de 2027**. Todo el proyecto es un único archivo `index.html` sin dependencias externas: una ilustración animada en canvas con el **Hotel Disney Newport Bay Club** y el **Castillo de la Bella Durmiente**, conectada al clima real de Marne-la-Vallée.

## Características

- **Cuenta atrás en directo** hasta el 14 de noviembre de 2027 (días, horas, minutos, segundos) y reloj en hora de París.
- **Dos escenas animadas** — cambia haciendo clic en el título:
  - Hotel Disney Newport Bay Club (puerto, faro, patos, bandera, ventanas iluminadas).
  - Castillo de la Bella Durmiente (fuegos artificiales por la noche).
- **Simulador de entorno** (botón *Simular entorno*): automático, día, noche, atardecer, lluvia, nieve, tormenta y viento.
- **Clima real** de Disneyland París vía [Open-Meteo](https://open-meteo.com): temperatura, estado del cielo, lluvia, nieve, viento y niebla.
- **Efectos dinámicos**: lluvia, nieve, hojas arrastradas por el viento, relámpagos, estrellas, niebla, reflejos en el agua y destellos del faro.
- **PWA instalable**: manifest + service worker, funciona sin conexión.
- **Responsive**: se escala a móvil, tablet y escritorio (diseño base 1600×900, hasta 2× retina).

## Uso

No requiere build ni instalación. Se despliega como estática:

```bash
# servir localmente con cualquier servidor estático
python3 -m http.server 8080
```

o simplemente abrir `index.html` en el navegador.

## Estructura

| Archivo | Descripción |
| --- | --- |
| `index.html` | Toda la aplicación (estilos, HTML y motor canvas). |
| `manifest.webmanifest` | Metadatos PWA (nombre, iconos, theme). |
| `sw.js` | Service worker con estrategia *stale-while-revalidate* y cache de la app shell. |
| `favicon.svg`, `icon-*.png`, `apple-touch-icon.png` | Iconos de la app. |

## Datos

- **Destino**: Disneyland Paris, Marne-la-Vallée (48.8722, 2.7762).
- **Fecha objetivo**: 14 de noviembre de 2027 (medianoche local).
- **Clima**: API pública `api.open-meteo.com/v1/forecast`, refrescada cada 20 minutos.

## Personalización

Los parámetros principales están al inicio del `<script>` en `index.html`:

- `TARGET`: fecha de la cuenta atrás.
- `LAT` / `LON`: coordenadas para el clima.
- `DESIGN_W` / `DESIGN_H`: lienzo de diseño de referencia.
- Los modos del simulador se definen en `applyMode()` y los estados del cielo en `codeInfo()`.