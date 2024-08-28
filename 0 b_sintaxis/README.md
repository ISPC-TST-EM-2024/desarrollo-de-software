# Guía Básica sobre el Framework Arduino y su Sintaxis

---

## 1. **Introducción al Framework Arduino**

### ¿Qué es Arduino?

Arduino es una plataforma de hardware y software de código abierto diseñada para facilitar la creación de proyectos electrónicos interactivos. Está compuesta por:
- **Placa Arduino:** Un microcontrolador que actúa como el "cerebro" del proyecto, ejecutando las instrucciones programadas.
- **Arduino IDE:** Un entorno de desarrollo integrado donde se escribe y carga el código en la placa.

### Componentes del Ecosistema Arduino

1. **Placas Arduino:** Varían en tamaño y capacidad, desde el popular Arduino Uno hasta el Arduino Mega, con más pines y memoria.
2. **Shields:** Placas adicionales que se conectan a la placa base para ampliar sus capacidades (conexiones Wi-Fi, control de motores, etc.).
3. **Sensores y Actuadores:** Dispositivos que permiten interactuar con el entorno, como sensores de temperatura, luz, motores, LEDs, entre otros.

### Instalación y Configuración del Arduino IDE

Para comenzar a trabajar con Arduino, se debe:
1. Descargar e instalar el Arduino IDE desde el [sitio oficial](https://www.arduino.cc/en/software).
2. Conectar la placa Arduino al ordenador mediante un cable USB.
3. Seleccionar el modelo de placa y el puerto COM correspondiente en el menú "Herramientas" del IDE.
4. Escribir o cargar un sketch (programa) y subirlo a la placa.

## 2. **Sintaxis y Estructura Básica del Código Arduino**

### Estructura del Código en Arduino

Cada programa en Arduino (denominado **sketch**) contiene al menos dos funciones esenciales:

1. **setup():** Esta función se ejecuta una vez al iniciar el programa. Se utiliza para configurar pines, inicializar variables, y establecer la comunicación serie. Ejemplo:
   ```cpp
   void setup() {
       pinMode(LED_BUILTIN, OUTPUT);  // Configura el pin del LED integrado como salida
   }
   ```

2. **loop():** Esta función se repite indefinidamente y es donde se escribe el código que ejecutará las acciones del dispositivo de manera continua. Ejemplo:
   ```cpp
   void loop() {
       digitalWrite(LED_BUILTIN, HIGH);  // Enciende el LED
       delay(1000);                      // Espera 1 segundo
       digitalWrite(LED_BUILTIN, LOW);   // Apaga el LED
       delay(1000);                      // Espera 1 segundo
   }
   ```

### Comentarios en el Código

Los comentarios se utilizan para documentar y explicar el código:
- **Comentario de línea:** Se inicia con \`//\` y se extiende hasta el final de la línea.
- **Comentario de bloque:** Se encierra entre \`/*\` y \`*/\` para abarcar múltiples líneas.

### Declaración de Variables

Las variables almacenan datos que el programa utiliza. Se declaran con un tipo de dato (como `int`, `float`, `boolean`) y un nombre:
```cpp
int ledPin = 13;  // Declara una variable ledPin de tipo entero
```

### Tipos de Datos Comunes

- **int:** Enteros.
- **float:** Números con punto decimal.
- **char:** Caracteres individuales.
- **boolean:** Valores `true` o `false`.

## 3. **Control de Entradas y Salidas**

### Configuración de Pines

Arduino permite configurar pines como entradas o salidas digitales:
- **pinMode(pin, mode):** Define un pin como entrada (`INPUT`) o salida (`OUTPUT`).
  ```cpp
  pinMode(2, INPUT);    // Configura el pin 2 como entrada
  pinMode(13, OUTPUT);  // Configura el pin 13 como salida
  ```

### Escritura en Salidas Digitales

- **digitalWrite(pin, value):** Establece el estado de un pin de salida como `HIGH` (encendido) o `LOW` (apagado).
  ```cpp
  digitalWrite(13, HIGH);  // Enciende el LED en el pin 13
  ```

### Lectura de Entradas Digitales

- **digitalRead(pin):** Lee el estado de un pin de entrada, devolviendo \`HIGH\` o `LOW`.
  ```cpp
  int buttonState = digitalRead(2);  // Lee el estado del botón en el pin 2
  ```

### Lectura de Entradas Analógicas

Arduino puede leer valores analógicos en pines específicos (A0 a A5 en el Arduino Uno):
- **analogRead(pin):** Retorna un valor entre 0 y 1023, dependiendo del voltaje leído.
  ```cpp
  int sensorValue = analogRead(A0);  // Lee el valor del sensor en el pin A0
  ```

### Escritura de Salidas Analógicas (PWM)

Para simular una salida analógica, Arduino utiliza modulación por ancho de pulso (PWM):
- **analogWrite(pin, value):** Envía un valor PWM entre 0 (0% de ciclo de trabajo) y 255 (100% de ciclo de trabajo).
  ```cpp
  analogWrite(9, 128);  // Envía una señal PWM al 50% al pin 9
  ```

## 4. **Estructuras de Control y Bucles**

### Condicionales

Las estructuras condicionales permiten que el programa tome decisiones basadas en condiciones:
- **if-else:**
  ```cpp
  if (digitalRead(2) == HIGH) {
      digitalWrite(13, HIGH);  // Enciende el LED si el botón está presionado
  } else {
      digitalWrite(13, LOW);   // Apaga el LED si el botón no está presionado
  }
  ```

### Bucles

Los bucles permiten ejecutar un bloque de código varias veces:
- **for:**
  ```cpp
  for (int i = 0; i < 10; i++) {
      digitalWrite(13, HIGH);
      delay(100);
      digitalWrite(13, LOW);
      delay(100);
  }
  ```
- **while:**
  ```cpp
  while (digitalRead(2) == LOW) {
      // Espera mientras el botón no esté presionado
  }
  ```

## 5. **Funciones y Modularización**

Las funciones permiten agrupar código reutilizable, mejorando la organización y la legibilidad:
```cpp
void blinkLED(int times) {
    for (int i = 0; i < times; i++) {
        digitalWrite(13, HIGH);
        delay(500);
        digitalWrite(13, LOW);
        delay(500);
    }
}

void loop() {
    blinkLED(3);  // Hace parpadear el LED tres veces
}
```

## 6. **Interrupciones**

Las interrupciones permiten que Arduino responda instantáneamente a ciertos eventos:
- **attachInterrupt(digitalPinToInterrupt(pin), ISR, mode):** Vincula una función de interrupción a un pin.
- **ISR:** Función que se ejecuta cuando ocurre la interrupción.
  ```cpp
  void setup() {
      pinMode(2, INPUT);
      attachInterrupt(digitalPinToInterrupt(2), handleInterrupt, RISING);
  }

  void handleInterrupt() {
      digitalWrite(13, HIGH);  // Enciende el LED cuando ocurre la interrupción
  }
  ```

## 7. **Uso del Monitor Serie**

El Monitor Serie es una herramienta del Arduino IDE que permite enviar y recibir datos desde y hacia la placa, útil para depuración:
- **Serial.begin(baud rate):** Inicia la comunicación serie a la velocidad especificada.
  ```cpp
  Serial.begin(9600);  // Inicia la comunicación a 9600 baudios
  ```
- **Serial.print() y Serial.println():** Envía datos al monitor serie.
  ```cpp
  Serial.println("Hola, Arduino!");  // Imprime un mensaje en el monitor serie
  ```

## 8. **Buenas Prácticas de Programación**

### Documentación del Código

Es esencial comentar el código para mejorar su mantenimiento y legibilidad, especialmente en proyectos colaborativos.

### Modularización

Dividir el código en funciones y mantener una estructura clara ayuda a organizar el proyecto, facilita la depuración, y mejora la reutilización del código.

### Depuración y Pruebas

Utilizar el Monitor Serie para imprimir valores de variables y mensajes de estado es una práctica clave para identificar y corregir errores en el código.

## 9. **Conclusión**

Arduino es una herramienta poderosa y accesible para desarrolladores de todos los niveles. Entender su framework y sintaxis básica es esencial para empezar a crear proyectos interactivos. Con esta guíaAquí tienes el script `create_readme.sh` que generará el archivo `README.md` con el contenido que proporcionaste:
