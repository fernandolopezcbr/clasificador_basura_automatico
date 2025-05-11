# clasificador_basura_automatico
Clasificador de basura automatico con python , webcam(IP) y nodemcu , servomotores y pantalla 20x4, con mecanismo banda transportadora

![c18e113d-ea07-4f96-ad5f-178e776bae4f](https://github.com/user-attachments/assets/199d7575-fc7c-4f28-a614-ef0987d80e9c)

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

