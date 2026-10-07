# Cupra Car Launcher

Aplicación Android personalizada diseñada específicamente para su uso en pantallas de vehículos (Car Head Units), tablets en salpicaderos y sistemas embebidos como Raspberry Pi. 

El proyecto consiste en un launcher vehicular completo, inspirado en las líneas de diseño de la marca Cupra (interfaz oscura inmersiva con acentos neón/cobre). Su objetivo es unificar multimedia, telemetría básica (GPS/Velocidad) y navegación en una sola pantalla, incorporando además un sistema de perfiles de usuario para restringir el acceso al sistema.
<img width="1837" height="1172" alt="Captura de pantalla 2026-10-07 095259" src="https://github.com/user-attachments/assets/0b4e84a3-c110-40cd-af64-30cb5c2b8261" />

---

## 🌟 Estructura de la Interfaz

La pantalla principal está dividida en 3 paneles funcionales y un dock inferior para facilitar el manejo táctil rápido:

### 1. Panel Izquierdo: Reproductor Multimedia
Integración de un widget multimedia avanzado que captura las sesiones activas de audio del sistema (compatible con Spotify, YouTube Music, Radio, etc.).
* Renderizado de la carátula del álbum con diseño dinámico en formato disco de vinilo (ocupando el 40% de la altura del panel).
* Controles de reproducción integrados (Play/Pause, Anterior/Siguiente, Favoritos y Volumen).
* Sistema de marquesina deslizante automática para títulos de canciones y artistas largos.

### 2. Panel Central: Cluster Digital y Clima
Actúa como cuadro de instrumentos secundario.
* **Velocímetro Digital (km/h):** Utiliza un algoritmo de suavizado exponencial para procesar los datos de ubicación en tiempo real, evitando saltos bruscos en la numeración en pantalla.
* **Previsión Meteorológica:** Sistema de tarjetas que muestra el clima actual y una previsión escalonada (+2h, +4h, +6h), incluyendo porcentajes de precipitación y temperatura.
* **Estado del Vehículo:** Indicadores visuales para el modo de conducción y el estado de las luces.

### 3. Panel Derecho: Navegación Integrada
* **Mapa Interactivo:** Visor de mapas integrado (vía OpenStreetMap) que rastrea de forma fluida y en tiempo real la posición GPS del vehículo.
* **Monitor de Señal:** Indicador de estado que refleja si el hardware está recibiendo señal de satélites (Verde/Rojo).
* **Modo Noche:** El mapa invierte su paleta de colores automáticamente entre las 20:00 y las 06:00.
* **Acceso Directo:** Botón flotante para lanzar la aplicación de navegación primaria del sistema (Maps, Waze, etc.).

---

## 🧭 Dock de Navegación Inferior

Barra persistente para cambiar entre los modos de la pantalla:
* Botón central principal (logotipo de la marca).
* Accesos directos categorizados: **Música, Audiolibros, Navegación y Multimedia**.
* **Lógica de cajón inteligente:** En caso de que una categoría no tenga aplicaciones asignadas o estén restringidas, el sistema muestra un aviso flotante y cancela la apertura del cajón de apps, mejorando la experiencia del Modo Invitado.

---

## ⚙️ Configuración y Gestión de Perfiles

El launcher cuenta con un panel de ajustes propio para personalizar el comportamiento del sistema. Incluye un sistema de seguridad para proteger el dispositivo:

* **Modo Administrador e Invitado:** Posibilidad de bloquear los ajustes mediante PIN. El Modo Invitado restringe los cambios y la apertura de aplicaciones no autorizadas.
* **Gestor de Aplicaciones:** Herramienta para ocultar selectivamente (mediante checkboxes) cualquier aplicación instalada, haciéndola invisible en el cajón general.
* **Configuración del Clima:** Selección entre actualización dinámica por coordenadas (Auto GPS) o ciudad estática.
* **Personalización Visual:** Selector de variantes de tema (colores/acentos), selección del modelo de vehículo a mostrar en el gráfico de la pantalla principal y configuración del tiempo de inactividad para el salvapantallas.
* **Confort Visual:** Función de atenuado leve de pantalla (20%) durante el arranque inicial, que se desactiva con la primera interacción táctil.

---

## 🛰️ Notas sobre Hardware (Instalaciones en Raspberry Pi)

El launcher está preparado para funcionar en placas de desarrollo como Raspberry Pi (4 o 5), pero requiere consideraciones específicas de hardware debido a la ausencia de componentes móviles estándar:

1. **Requisito de GPS Externo:** Las placas Raspberry no integran hardware de geolocalización. Para que el velocímetro y el panel de navegación funcionen, es necesario conectar un módulo GPS por USB (ej. receptores u-blox compatibles con NMEA) o Bluetooth.
2. **Proveedores de Red:** Dado que estas placas no suelen contar con geolocalización por redes móviles/Wi-Fi como los smartphones, el sistema depende 100% de la recepción de satélites física.
3. **Solución de problemas:** Si el indicador de satélite se muestra en rojo, es necesario verificar que el sistema operativo Android instalado en la Pi tiene los drivers del kernel correctos (ttyACM/ttyUSB) y está configurado para leer el puerto del dongle externo.
