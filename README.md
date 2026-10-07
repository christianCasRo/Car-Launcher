# Cupra Car Launcher

Transforma la pantalla de tu vehículo, tablet o sistema integrado en un centro de mando de alta gama. Inspirado en el diseño deportivo de Cupra, este launcher ofrece una interfaz inmersiva, oscura y con acentos de color que moderniza por completo el salpicadero de tu coche.

Diseñado para evitar distracciones al volante, cuenta con controles grandes, información en tiempo real y un sistema de perfiles para proteger tu configuración.

---

## 🌟 Experiencia de Conducción en 3 Paneles

La pantalla principal está dividida de forma inteligente para que tengas todo lo importante a un solo vistazo:

### 1. Panel Multimedia
Controla tu música sin perder de vista la carretera.
* Visualización dinámica con carátula de álbum y estilo de disco de vinilo.
* Controles rápidos (Reproducir/Pausar, Anterior, Siguiente y Volumen).
* Títulos deslizantes y sincronización total con tus apps favoritas (Spotify, YouTube Music, Radio, etc.).

### 2. Cuadro de Instrumentos y Clima
Toda la información vital de tu entorno y conducción en el centro de la pantalla.
* **Velocímetro Digital en tiempo real (km/h)**, diseñado con un sistema de suavizado para mostrar la velocidad de forma fluida y sin saltos.
* **Previsión del tiempo inteligente** que te muestra el clima actual y la predicción de las próximas 6 horas de forma gráfica.
* Indicadores de estado del vehículo (Modo de conducción y Luces).

### 3. Navegación y Mapa en Vivo
Tu ruta siempre visible.
* **Mapa interactivo integrado** que sigue la posición GPS de tu vehículo de forma fluida y automática.
* Indicador visual de cobertura satelital.
* Acceso directo con un solo toque a tu navegador favorito (Google Maps, Waze, etc.).
* **Modo Noche Automático:** El mapa oscurece sus colores entre las 20:00 y las 06:00 para no deslumbrar en la conducción nocturna.

---

## 🧭 Acceso Rápido (Dock Inferior)

En la parte inferior de la pantalla encontrarás un menú de acceso rápido diseñado para pulsarse fácilmente en movimiento:
* Botón central con el logo de Cupra.
* Categorías organizadas: **Música, Audiolibros, Navegación y Multimedia**.

---

## 🔒 Privacidad y Perfiles (Admin / Invitado)

¿Prestas el coche o lo dejas en el taller? El launcher incluye un sistema de seguridad para proteger tu privacidad:
* **Modo Administrador (Protegido por PIN):** Acceso total a todas las aplicaciones y ajustes del sistema.
* **Modo Invitado:** Restringe el acceso. Si el invitado intenta abrir aplicaciones no permitidas o categorías vacías, el sistema bloqueará la acción de forma inteligente.
* **Ocultar Apps:** Selecciona qué aplicaciones instaladas en el dispositivo quieres que sean totalmente invisibles.

---

## ⚙️ Personalización a tu Medida

Desde el panel de ajustes puedes adaptar el launcher a tu gusto:
* **Tema y Colores:** Adapta los acentos visuales al estilo Cupra.
* **Gráfico del Vehículo:** Cambia la imagen de tu coche en la pantalla (ej. Cupra Formentor).
* **Comportamiento del Clima:** Haz que se actualice por GPS a medida que viajas, o fíjalo en tu ciudad de residencia.
* **Salvapantallas:** Configura el tiempo de inactividad (5, 10 o 15 minutos).
* **Modo Confort Visual:** Atenuado suave de la pantalla al arrancar, que vuelve a su brillo normal con el primer toque.

---

## 🛠️ Notas para instalaciones en Raspberry Pi

Si estás montando este sistema en una **Raspberry Pi** en lugar de una tablet o radio Android nativa y el mapa no se mueve o el velocímetro está a cero, se debe a una limitación del hardware:

A diferencia de los móviles, las placas Raspberry Pi no tienen antena GPS integrada. 
* **Solución:** Necesitarás conectar un receptor GPS por USB (como los modelos u-blox). Una vez conectado y detectado por el sistema Android de tu Raspberry, el launcher comenzará a marcar la velocidad y el mapa te seguirá automáticamente.

---
