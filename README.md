# Cupra Car Launcher

Un launcher Android avanzado y de alta gama diseñado específicamente para pantallas de vehículos (Car Head Units), tablets Android en salpicaderos y sistemas embebidos como Raspberry Pi. Inspirado en el diseño deportivo y tecnológico de Cupra (acentos cobre/neón, interfaz oscura inmersiva y widgets de alto rendimiento).

---

## 🌟 Pantallas y Paneles Principales

El launcher se estructura en una interfaz limpia de **3 paneles principales** + **Barra de Navegación Inferior (Dock)**:

1. **Panel Izquierdo (Reproductor de Multimedia)**
   - Carátula de álbum / disco de vinilo dinámica (40% de altura para máximo impacto visual).
   - Control de reproducción (Play/Pause, Pistas Siguiente/Anterior, Favoritos, Volumen).
   - Título y artista con marquesina deslizante automática.
   - Sintonización con sesiones activas de media (Spotify, YouTube Music, Radio, etc.).

2. **Panel Central (Cluster Digital & Clima)**
   - **Velocímetro Digital en tiempo real (km/h)** con filtro de suavizado exponencial (Exponential Moving Average) para evitar saltos bruscos.
   - **Widget del Tiempo en 3 Tarjetas Cuadradas** (+2h, +4h, +6h) con iconos de 24dp, temperatura, hora y porcentaje de lluvia sin recortes.
   - Cabecera con nombre de ciudad en marquesina, temperatura actual y condición meteorológica.
   - Controles de estado del vehículo (Modo de conducción, Luces).

3. **Panel Derecho (Navegación & Mapa en Vivo)**
   - **Mapa interactivo OpenStreetMap (Leaflet)** incrustado mediante WebView que sigue de forma fluida la posición GPS real del vehículo (`map.setView` y `marker.setLatLng` cada 500ms).
   - Indicador de estado GPS (Verde = Activo con señal / Rojo = Sin señal de satélite).
   - Botón de acceso rápido para abrir la aplicación de navegación predeterminada (Google Maps, Waze, etc.).

---

## 🧭 Barra de Navegación Inferior (Dock)

Situada en la parte inferior de la pantalla, incluye:
- **Logotipo de Cupra** escalado a 50dp (botón central o acceso rápido).
- **Accesos directos por categorías**:
  - **Música** (Music & Audio)
  - **Audio-Libros** (Audiobooks)
  - **Navegación** (Maps / GPS)
  - **Multimedia** (Video / Apps generales)
- **Gestión inteligente en Modo Invitado**: Si una categoría no tiene app asignada, en modo invitado muestra un aviso flotante y evita abrir el cajón de aplicaciones completo.

---

## ⚙️ Ajustes y Opciones Configurables

Desde el panel de Ajustes (protegido opcionalmente por PIN de Administrador) se puede configurar:
- **Modo Invitado / Modo Administrador**: Restricción de apps y ajustes.
- **Ocultar Aplicaciones**: Selección mediante casillas de verificación de las apps que no deseas mostrar en el cajón ni en modo invitado.
- **Modo de Clima**: `AUTO_GPS` (actualización dinámica por coordenadas) o `FIXED_CITY` (ciudad fija configurable).
- **Navegación Predeterminada**: Elección de app de mapas favorita.
- **Atenuado Leve al Arrancar (20%)**: Oscurecimiento sutil al encender el sistema que se desactiva automáticamente con el primer toque en pantalla.
- **Salvaspantallas por Inactividad**: Tiempo configurable (5, 10 o 15 minutos).
- **Variantes de Tema**: Personalización de colores y acentos visuales Cupra.
- **Estilo de Gráfico del Vehículo**: Visualización del coche (ej. Cupra Formentor).

---

## 🛰️ Guía de Diagnóstico: GPS en Raspberry Pi

Si en tu **Raspberry Pi** el indicador GPS se queda en **Rojo**, la zona de navegación no se mueve y no marca los km/h (mientras que en otros dispositivos móviles funciona perfectamente), ten en cuenta lo siguiente:

1. **Ausencia de Hardware GPS Interno**:
   - A diferencia de los smartphones, las placas Raspberry Pi (4 o 5) **no disponen de un chip GPS integrado**.
   - Si no tienes conectado un **receptor GPS USB** (ej. u-blox u-7/u-8) o un módulo GPS Bluetooth/serial externo compatible con NMEA, el `LocationManager` de Android no recibe ninguna trama de satélites.
2. **Proveedores de Red (Network Location)**:
   - Los smartphones obtienen ubicación mediante torres de telefonía y redes Wi-Fi cercanas (Google Play Services / Fused Location). Las Raspberry Pi montadas en vehículos suelen carecer de conexión celular y a menudo de geolocalización Wi-Fi estática, por lo que `NETWORK_PROVIDER` devuelve nulo.
3. **Cómo verificar y solucionar en Raspberry Pi**:
   - Conecta un dongle GPS USB compatible con Android (asegúrate de que los drivers del kernel de tu ROM de Android para Raspberry Pi soporten dispositivos ttyACM / ttyUSB).
   - Instala una app de diagnóstico en la Pi (como *GPS Test*) para comprobar si el sistema operativo ve los satélites.
   - Si usas posicionamiento simulado o mock locations desde otro dispositivo, asegúrate de activar las opciones de desarrollador y permitir ubicaciones falsas (Mock Locations) en Android.

---

## 🌙 Modo Noche para el Mapa (Opcional)

Si deseas añadir un **modo noche** al mapa OpenStreetMap sin sobrecargar de recursos el sistema:
- **Método recomendado (CartoDB Dark Tiles)**:
  Modifica la URL de las tesolas en `RightNavWeatherPanel.kt`:
  ```javascript
  L.tileLayer('https://{s}.basemaps.cartocdn.com/dark_all/{z}/{x}/{y}{r}.png', {
      maxZoom: 19,
      attribution: '&copy; OpenStreetMap contributors &copy; CARTO'
  }).addTo(window.map);
  ```
  Esto proporciona mapas oscuros nativos optimizados, consumiendo los mismos o incluso menos recursos que las tesolas estándar.
- **Método alternativo (CSS Inversion)**:
  Añadir un filtro CSS en el HTML del WebView:
  ```css
  .leaflet-tile-pane { filter: brightness(0.6) invert(1) contrast(3) hue-rotate(200deg) saturate(0.3); }
  ```

---

## 🖼️ Configuración del Icono de la Aplicación (`icono.png`)

Para utilizar tu archivo `icono.png` como icono oficial de la aplicación:

1. **Ubicación recomendada**:
   - Coloca tu imagen en `app/src/main/res/drawable/icono.png` (o `ic_launcher.png`).
2. **Declaración en el Manifiesto (`AndroidManifest.xml`)**:
   Dentro de la etiqueta `<application>`:
   ```xml
   android:icon="@drawable/icono"
   android:roundIcon="@drawable/icono"
   ```
3. **Tamaño óptimo**:
   - Se recomienda que `icono.png` sea de al menos **512x512 píxeles** (formato PNG con transparencia opcional). Android se encargará de escalarlo automáticamente para las distintas densidades de pantalla (hdpi, xhdpi, xxhdpi, xxxhdpi).
