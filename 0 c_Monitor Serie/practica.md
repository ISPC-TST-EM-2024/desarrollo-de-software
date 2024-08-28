
# Introducción a la Programación de Sistemas Embebidos en C++ con Arduino

## Paradigmas de Programación

### Paradigma Imperativo
El **paradigma imperativo** es uno de los estilos más fundamentales de programación. Se basa en la idea de que un programa es una secuencia de instrucciones que cambian el estado del sistema. En este paradigma, el enfoque está en describir los *pasos* que la computadora debe seguir para alcanzar un objetivo específico.

#### Algoritmo
Un **algoritmo** es un conjunto bien definido de instrucciones o pasos a seguir para resolver un problema o realizar una tarea específica. Un algoritmo debe ser finito, claro y efectivo, es decir, debe terminar después de un número finito de pasos, y cada paso debe ser preciso y realizable.

**Ejemplo de Algoritmo en C++/Arduino:**
```cpp
void loop() {
    // Algoritmo para encender y apagar un LED
    digitalWrite(LED_BUILTIN, HIGH);  // Paso 1: Encender el LED
    delay(1000);                      // Paso 2: Esperar 1 segundo
    digitalWrite(LED_BUILTIN, LOW);   // Paso 3: Apagar el LED
    delay(1000);                      // Paso 4: Esperar 1 segundo
}
```

### Teorema de la Programación Estructurada
El teorema de la programación estructurada establece que cualquier algoritmo se puede implementar utilizando solo tres estructuras de control:

1. **Secuencia:** Ejecución de instrucciones en un orden específico.
2. **Selección (o decisión):** Ejecución condicional de instrucciones (por ejemplo, `if`, `else`).
3. **Iteración (o bucles):** Repetición de instrucciones (por ejemplo, `for`, `while`).

Estas estructuras permiten construir programas que son fáciles de entender y mantener.

### Implementación en C++
En C++, estas estructuras son fundamentales y se usan para escribir programas de manera clara y organizada.

**Ejemplo de Secuencia:**
```cpp
int a = 10;
int b = 20;
int suma = a + b;
```

**Ejemplo de Selección:**
```cpp
if (a > b) {
    Serial.println("a es mayor que b");
} else {
    Serial.println("a no es mayor que b");
}
```

**Ejemplo de Iteración:**
```cpp
for (int i = 0; i < 10; i++) {
    Serial.println(i);
}
```

### Bloques de Código: Funciones y Procedimientos

Los **bloques de código** son agrupaciones de sentencias que realizan una tarea específica. Estos bloques son cruciales para la reutilización del código y la organización de programas.

#### Funciones y Procedimientos en C++
- **Función:** Es un bloque de código que recibe entradas, realiza alguna operación, y retorna un valor.
  ```cpp
  int suma(int x, int y) {
      return x + y;
  }
  ```
- **Procedimiento:** En C++, no existe una distinción formal entre funciones y procedimientos, ya que todo se maneja como funciones. Un procedimiento es una función que no retorna ningún valor (`void`).
  ```cpp
  void encenderLed(int pin) {
      digitalWrite(pin, HIGH);
  }
  ```

## Comunicación en el Framework Arduino

La comunicación en Arduino se basa en varios tipos de interfaces, siendo la más común la **comunicación serial**. A través de la librería `Serial`, se puede enviar y recibir datos entre la placa Arduino y otros dispositivos (como un ordenador).

### Librería Serial

La librería `Serial` en Arduino es fundamental para la comunicación serial entre la placa y otros dispositivos. Se utiliza para enviar y recibir datos a través del puerto serial.

### Métodos de la Clase Serial

- **`if(Serial)`**: Verifica si la comunicación serial está activa.
- **`available()`**: Retorna el número de bytes disponibles para leer desde el buffer serial.
- **`availableForWrite()`**: Retorna la cantidad de espacio libre en el buffer de salida.
- **`begin(baud_rate)`**: Inicializa la comunicación serial a una velocidad específica.
- **`end()`**: Finaliza la comunicación serial.
- **`find(target)`**: Lee datos de entrada hasta encontrar la cadena objetivo especificada.
- **`findUntil(target, terminator)`**: Lee hasta encontrar la cadena objetivo o el terminador.
- **`flush()`**: Espera hasta que todos los datos en el buffer de transmisión hayan sido enviados.
- **`parseFloat()`**: Lee y retorna el siguiente número de punto flotante (`float`).
- **`parseInt()`**: Lee y retorna el siguiente número entero (`int`).
- **`peek()`**: Retorna el próximo byte de la entrada serial sin removerlo del buffer.
- **`print(data)`**: Envía datos a través de la conexión serial en formato texto.
- **`println(data)`**: Similar a `print()`, pero añade un salto de línea.
- **`read()`**: Lee un byte de la entrada serial.
- **`readBytes(buffer, length)`**: Lee un número específico de bytes desde la entrada serial en un buffer.
- **`readBytesUntil(character, buffer, length)`**: Lee bytes de la entrada serial hasta un carácter específico.
- **`readString()`**: Lee la entrada serial como una cadena de texto.
- **`readStringUntil(character)`**: Lee la entrada serial como una cadena hasta un carácter específico.
- **`setTimeout(milliseconds)`**: Configura el tiempo máximo que los métodos de lectura esperarán por los datos antes de que expiren.
- **`write(data)`**: Envía un byte o una serie de bytes a través de la conexión serial.
- **`serialEvent()`**: Función especial que se llama cuando llegan nuevos datos a la entrada serial.

## Ejercicios Prácticos

### Ejercicio 1: Inicialización y Verificación de la Comunicación Serial
**Función:** `begin()`, `if(Serial)`, `end()`

**Descripción:** Inicializa la comunicación serial a 9600 baudios, verifica si la conexión está activa, y luego la finaliza.

```cpp
void setup() {
    Serial.begin(9600);  // Inicializa la comunicación serial a 9600 baudios
    if (Serial) {
        Serial.println("Conexión serial activa");
    }
    Serial.end();  // Finaliza la comunicación serial
}

void loop() {
    // Nada que hacer en el loop
}
```

### Ejercicio 2: Lectura Básica de Datos Seriales
**Función:** `available()`, `read()`, `print()`, `println()`

**Descripción:** Lee datos del puerto serial y los imprime en la consola serial.

```cpp
void setup() {
    Serial.begin(9600);
}

void loop() {
    if (Serial.available() > 0) {  // Verifica si hay datos disponibles
        char c = Serial.read();  // Lee un byte de la entrada serial
        Serial.print("Recibido: ");
        Serial.println(c);  // Imprime el byte recibido
    }
}
```

### Ejercicio 3: Escribir Datos en el Puerto Serial
**Función:** `availableForWrite()`, `write()`

**Descripción:** Escribe una serie de bytes en el puerto serial si hay espacio suficiente en el buffer de salida.

```cpp
void setup() {
    Serial.begin(9600);
}

void loop() {
    if (Serial.availableForWrite() > 3) {  // Verifica si hay espacio para escribir 3 bytes
        byte data[] = {0x41, 0x42, 0x43};  // Bytes a enviar (A, B, C)
        Serial.write(data, sizeof(data));  // Envía los bytes
    }
    delay(1000);  // Espera 1 segundo antes de volver a enviar
}
```

### Ejercicio 4: Encontrar una Cadena en la Entrada Serial
**Función:** `find()`, `findUntil()`

**Descripción:** Busca una cadena específica en la entrada serial y realiza una acción si la encuentra.

```cpp
void setup() {
    Serial.begin(9600);
}

void loop() {
    if (Serial.find("START")) {  // Busca la cadena "START"
        Serial.println("Cadena START encontrada");
    }
    if (Serial.findUntil("END", '\n')) {  // Busca "END" hasta un salto de línea
        Serial.println("Cadena END encontrada antes de nueva línea");
    }
}
```

### Ejercicio 5: Procesamiento de Números desde la Entrada Serial
**Función:** `parseFloat()`, `parseInt()`

**Descripción:** Lee números enteros y flotantes desde la entrada serial y los muestra.

```cpp
void setup() {
    Serial.begin(9600);
}

void loop() {
    if (Serial.available()) {
        float f = Serial.parseFloat();  // Lee un número flotante
        int i = Serial.parseInt();  // Lee un número entero
        Serial.print("Flotante: ");
        Serial.println(f);
        Serial.print("Entero: ");
        Serial.println(i);
    }
}
```

### Ejercicio 6: Uso del Buffer de Entrada Serial
**Func

ión:** `peek()`, `readBytes()`, `readBytesUntil()`

**Descripción:** Muestra cómo leer bytes desde la entrada serial sin consumirlos y hasta un carácter específico.

```cpp
void setup() {
    Serial.begin(9600);
}

void loop() {
    if (Serial.available()) {
        char peeked = Serial.peek();  // Lee el siguiente byte sin consumirlo
        Serial.print("Siguiente byte: ");
        Serial.println(peeked);

        char buffer[10];
        int bytesRead = Serial.readBytes(buffer, 10);  // Lee hasta 10 bytes
        Serial.print("Bytes leídos: ");
        Serial.println(bytesRead);

        int bytesReadUntil = Serial.readBytesUntil('\n', buffer, 10);  // Lee bytes hasta nueva línea
        Serial.print("Bytes leídos hasta nueva línea: ");
        Serial.println(bytesReadUntil);
    }
}
```

### Ejercicio 7: Leer y Mostrar Cadenas de Texto
**Función:** `readString()`, `readStringUntil()`

**Descripción:** Lee y muestra cadenas de texto completas desde la entrada serial, terminando en un carácter específico.

```cpp
void setup() {
    Serial.begin(9600);
}

void loop() {
    if (Serial.available()) {
        String texto = Serial.readString();  // Lee una cadena completa
        Serial.print("Texto leído: ");
        Serial.println(texto);

        String textoHasta = Serial.readStringUntil('\n');  // Lee hasta un salto de línea
        Serial.print("Texto leído hasta nueva línea: ");
        Serial.println(textoHasta);
    }
}
```

### Ejercicio 8: Configuración de Timeout en la Lectura Serial
**Función:** `setTimeout()`

**Descripción:** Configura el tiempo de espera máximo para las operaciones de lectura en la entrada serial.

```cpp
void setup() {
    Serial.begin(9600);
    Serial.setTimeout(5000);  // Configura un timeout de 5 segundos
}

void loop() {
    Serial.println("Escribe un número entero:");
    int numero = Serial.parseInt();  // Espera hasta 5 segundos para leer un número
    Serial.print("Número leído: ");
    Serial.println(numero);
}
```

### Ejercicio 9: Uso de `flush()` para Asegurar la Transmisión Completa
**Función:** `flush()`

**Descripción:** Envía todos los datos pendientes en el buffer de salida serial antes de continuar.

```cpp
void setup() {
    Serial.begin(9600);
}

void loop() {
    Serial.print("Enviando datos...");
    Serial.flush();  // Asegura que todos los datos se envíen antes de continuar
    Serial.println("Todos los datos han sido enviados");
    delay(1000);
}
```

### Ejercicio 10: Manejo de Eventos Seriales
**Función:** `serialEvent()`

**Descripción:** Implementa una función que se ejecuta automáticamente cuando llegan nuevos datos seriales.

```cpp
void setup() {
    Serial.begin(9600);
}

void loop() {
    // Código principal del loop
}

void serialEvent() {
    while (Serial.available()) {
        char c = Serial.read();
        Serial.print("Caracter recibido en evento: ");
        Serial.println(c);
    }
}
```

Estos ejercicios proporcionan una introducción completa al manejo de la clase `Serial` en Arduino, cubriendo desde la inicialización básica hasta el procesamiento avanzado de datos. Al trabajar a través de estos ejemplos, ganarás una comprensión sólida de cómo manejar la comunicación serial en tus proyectos de sistemas embebidos.

---


```

Este `README.md` proporciona una guía estructurada que cubre conceptos clave, explicaciones detalladas, y ejemplos prácticos, lo que facilitará el aprendizaje y la aplicación de los conocimientos en proyectos de sistemas embebidos con Arduino.