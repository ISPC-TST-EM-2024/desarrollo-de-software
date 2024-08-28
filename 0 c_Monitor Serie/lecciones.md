
# Práctica del Monitor Serie con Arduino en Proteus

## 1. **Descripción General del Virtual Terminal en Proteus**

El **Virtual Terminal** en Proteus permite la simulación de la comunicación serie (RS232) entre un microcontrolador y el PC. Esta herramienta es fundamental para la depuración, ya que muestra los datos enviados desde el microcontrolador y permite enviar comandos al mismo.

### **Características Principales:**
- **Comunicación bidireccional:** Envía y recibe datos en formato ASCII.
- **Interfaz de dos cables:** RXD (datos recibidos) y TXD (datos transmitidos).
- **Configuraciones ajustables:** Velocidad en baudios, bits de datos, paridad y bits de parada.
- **Compatibilidad:** Directamente compatible con los UARTs de muchos microcontroladores.

## 2. **Pasos para Configurar y Utilizar el Monitor Serie en Proteus**

### **Paso 1: Añadir el Virtual Terminal al Esquema**
1. En Proteus, selecciona el **Virtual Terminal** desde la biblioteca de componentes.
2. Coloca el **Virtual Terminal** en el esquema.
3. Conecta los pines **RX** y **TX** del Virtual Terminal a los pines correspondientes del microcontrolador (por ejemplo, **TX** del microcontrolador a **RX** del terminal y viceversa).

### **Paso 2: Configuración del Virtual Terminal**
1. Haz doble clic en el Virtual Terminal para abrir sus propiedades.
2. Configura la velocidad en baudios a **9600**.
3. Ajusta los parámetros de datos:
   - **8 bits de datos**
   - **Paridad: Ninguna**
   - **1 bit de parada**
4. Si usas un driver RS232 como el MAX232, ajusta la polaridad de los pines RX/TX a invertido.

### **Paso 3: Configuración en el Código Arduino**
En tu sketch de Arduino, configura la comunicación serie con la misma velocidad en baudios:

```cpp
void setup() {
    Serial.begin(9600);  // Inicia la comunicación serie a 9600 baudios
}

void loop() {
    Serial.println("Hola, Monitor Serie!");  // Envía un mensaje al terminal
    delay(1000);  // Espera 1 segundo
}
```

### **Paso 4: Simulación y Uso del Virtual Terminal**
1. Inicia la simulación en Proteus.
2. Observa cómo el **Virtual Terminal** muestra los datos enviados desde Arduino.
3. Puedes escribir texto en el terminal para enviarlo de vuelta al microcontrolador.

## 3. **Consejos para Depuración**
- **Verifica la Conexión RX/TX:** Asegúrate de que los pines están correctamente conectados (TX a RX y RX a TX).
- **Ajuste de Polos:** Si usas un MAX232, recuerda que debes invertir la polaridad de RX/TX.
- **Depuración con Echo:** Si no ves los datos que envías, habilita "Echo Typed Characters" para verificar que el terminal esté recibiendo los datos correctamente.

## 4. **Explicación del Código y Flujo de Datos**
El código de Arduino utiliza la función `Serial.begin(9600)` para iniciar la comunicación serie a 9600 baudios. La función `Serial.println()` se utiliza para enviar datos al terminal. Estos datos se muestran en tiempo real en el Virtual Terminal de Proteus, lo que te permite verificar que el Arduino está funcionando correctamente y enviando datos como se espera.

## 5. **Prueba Completa**
Con todo configurado, puedes usar el Virtual Terminal para monitorear la salida de datos de tu microcontrolador, depurar mensajes, y enviar comandos desde el teclado a tu microcontrolador en una simulación interactiva.

## **Conclusión**
El uso del **Virtual Terminal** en Proteus es una herramienta poderosa para simular la comunicación serie en proyectos Arduino, especialmente en fases de desarrollo y depuración. Con los pasos anteriores, deberías poder configurar y utilizar el Monitor Serie en Proteus de manera efectiva.



# Ejercicios de Práctica: Monitor Serie

1. Configura la comunicación serie a 9600 baudios.
2. Envía un mensaje desde Arduino al Monitor Serie.
3. Recibe un comando desde el ordenador y realiza una acción en Arduino.


## Ejemplo

El siguiente código de Arduino envía un mensaje al Monitor Serie y espera un comando para encender o apagar un LED:

```cpp

void setup() {
    // Inicia la comunicación serial a 9600 baudios
    Serial.begin(9600);
    Serial.println("Arduino está listo para recibir comandos.");
}

void loop() {
    // Verifica si hay datos disponibles para leer
    if (Serial.available() > 0) {
        // Lee el comando recibido
        String comando = Serial.readStringUntil('\n');

        // Responde según el comando recibido
        if (comando == "ON") {
            Serial.println("El LED está encendido.");
            // Aquí podrías agregar código para encender un LED, por ejemplo.
        } else if (comando == "OFF") {
            Serial.println("El LED está apagado.");
            // Aquí podrías agregar código para apagar un LED, por ejemplo.
        } else {
            Serial.println("Comando no reconocido.");
        }
    }
}
```
