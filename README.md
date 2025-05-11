# clasificador_basura_automatico
Clasificador de basura automatico con python , webcam(IP) y nodemcu , servomotores y pantalla 20x4, con mecanismo banda transportadora

![c18e113d-ea07-4f96-ad5f-178e776bae4f](https://github.com/user-attachments/assets/199d7575-fc7c-4f28-a614-ef0987d80e9c)


✅ 📊 Tabla de Conexiones del Sistema Clasificador de Basura
Componente	Pin NodeMCU	Descripción	Notas
📗 LED Orgánico	D7 (GPIO13)	Encendido cuando se detecta residuo orgánico	Con resistencia de 220Ω
📘 LED Reciclable	D4 (GPIO2)	Encendido para reciclables	Con resistencia de 220Ω
🔴 LED Inorgánico	D8 (GPIO15)	Encendido para inorgánicos	Con resistencia de 220Ω
⚙️ Servo 1	D5 (GPIO14)	Posición 0°/90°/180° según clasificación	Utilizado para ambos tipos (orgánico e inorgánico)
⚙️ Servo 2	D6 (GPIO12)	Gira solo para inorgánico	Se activa junto con Servo 1 para doble movimiento
🚚 Motor Banda (L298N)	D0 (GPIO16)	Controla IN1 del L298N (encender motor)	IN2 puede ir a GND para un solo sentido
🔳 Pantalla LCD 20x4 I2C	D1 (GPIO5) / D2 (GPIO4)	SCL / SDA	Requiere librería LiquidCrystal_I2C y dirección 0x27 u 0x3F
📷 Cámara IP (celular)	Vía Wi-Fi	Transmite imagen a través de http://...	No conexión física; se accede desde Python por red Wi-Fi
🔌 GND común	GND	Tierra para todos los módulos	Unir GND de NodeMCU, servos, L298N, LCD y fuente externa
🔌 Fuente externa 5V	No directo a NodeMCU	Alimenta servos y motor vía L298N	No alimentar servos directamente desde el NodeMCU

🧠 Consideraciones:
No alimentes los servos desde el NodeMCU, usa una fuente externa de 5V 2A mínimo.

Conecta todas las tierras (GND) entre NodeMCU, L298N, servos y LCD.

La pantalla LCD puede ir alimentada desde el NodeMCU si tu pantalla no consume mucho.

La cámara IP se comunica por red (no se conecta físicamente).

Sistema Automatizado Clasificador de Residuos
🎯 Objetivo General:
Clasificar residuos automáticamente en orgánicos, inorgánicos y reciclables utilizando visión por computadora, inteligencia artificial y un microcontrolador (NodeMCU), todo sin intervención humana directa.

🧩 Componentes Principales:
🔹 Hardware:
📷 Cámara IP (celular con IP Webcam)

🟢🔴🔵 3 LEDs (indicadores de tipo de basura)

⚙️ 2 servomotores (clasifican residuos)

🚚 1 motor (banda transportadora)

🖥️ Pantalla LCD 20x4 (muestra estado e IP)

🔌 NodeMCU ESP8266 (controlador central)

🔹 Software:
🐍 Python con:
TensorFlow + Keras (clasificación IA)
OpenCV (captura y preprocesamiento de imagen)
Flask (interfaz web, opcional)
🌐 Comunicación HTTP entre Python ↔ NodeMCU

🔁 Funcionamiento General del Sistema:
Inicio:
El sistema carga el modelo entrenado (Teachable Machine) y toma una imagen de referencia del entorno vacío.

Monitoreo continuo:
La cámara captura nuevas imágenes y las compara con la imagen de referencia.

Detección de objeto:
Si hay una diferencia visual significativa (nuevo objeto), el sistema:
Espera 1.5 segundos (para estabilizar).
Captura una imagen clara
Clasifica el tipo de residuo con el modelo IA.

Acción física automática:
El script Python envía el resultado al NodeMCU. Este:
Activa la banda transportadora (motor).
Enciende el LED correspondiente.
Mueve el/los servos según la clasificación.

Reinicio del ciclo:
Una vez procesado, espera que el objeto sea retirado, actualiza la imagen de referencia y continúa monitoreando.

🧠 Tipos de basura detectados:
Tipo	Color dominante o modelo	Acción física
Orgánico	IA entrenada	Servo 1: 180°
Inorgánico	IA entrenada	Servo 1: 0°, Servo 2: 180°
Reciclable	IA entrenada	Solo motor (cae al final)

💾 (Opcional) Registro y respaldo:
Guardar cada imagen clasificada con nombre, fecha y tipo.

Registrar los datos en CSV o Google Sheets para auditoría.

✅ Ventajas del sistema:
Completamente automatizado
Basado en visión e IA (sin sensores físicos)
Escalable y adaptable a nuevos tipos de residuos
Puede funcionar localmente (sin internet)

