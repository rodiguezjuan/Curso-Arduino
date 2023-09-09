# 3. Mis primeros programas 

## 1. Hola Mundo (Básico)

Uno de los primeros pasos con Arduino es comprender, como interactúan las entradas y salidas de nuestro microcontrolador. Para esto construiros un proyecto muy simple que enciende y apaga un LED conectado a la placa de Arduino. 

- Diseñar nuestro circuito.

    Es hacer que un pequeño LED (diodo emisor de luz) conectado a la placa de Arduino parpadee, es decir, que se encienda y apague en intervalos regulares.

    Para ello conectarás un LED a uno de los pines digitales de un andino con una resistencia de 1000 ohm. ([Esquema del circuito](https://www.tinkercad.com/things/biiOq5rp1ol?sharecode=nGda1yS8YBr-QEH9FFotG9IEl6kvTM-I1hzRE0aPqHk))

- Creando nuestro programa.

    El primer paso es abrir nuestro editor Arduino IDE y crear un nuevo archivo con extensión .ino.

    Segundo, definir Setup (Configuración) y Loop (Bucle)

    ```
    void setup(){
        ...
    }

    void loop(){
        ...
    }
    ```

- Configuraciones.

    En esta etapa le dirás a tu microcontrolador que hacer con cada una de sus entras y salidas.

    Para este proyecto definiremos pin digital como salida, usando la función `pinMode()`. Recuerda que las configuraciones deben encontrar en el interior del `setup`.  

    ```
        pinMode(LED_BUILTIN, OUTPUT);
    ```

- Ciclo de vida de nuestra aplicación.

    La función loop nos permite ejecutar de manera infinita nuestro código, por lo que dentro de ella deberá en contratarse la lógica necesaria para encender y apagar nuestro LED.

    Para activar y desactivar un pin digital en Arduino usamos `digitalWrite()` y para temporizar una tarea `delay()`. Para este proyecto en específico reflexiona un segundo, busca la forma de combinar las dos funciones para crear el efecto de parpadeo. (Encender, Apagar, Encender...)

    ```
    digitalWrite(LED_BUILTIN, HIGH);
    delay(1000);

    digitalWrite(LED_BUILTIN, LOW);
    delay(1000);
    ```

# 2. Hola Mundo (Avanzado) 

Ya que conocemos como controlar un LED con Arduino, es hora de conocer como leer el estado de una de sus estradas digitales, para ello agregaran un botón al proyecto anterior. Con el objetivo de encender nuestro LED y mostrar un mensaje, cuando presionemos nuestro botón.

- Diseñar el circuito.

    El circuito a emplear debe contener un LED con una residencia de 1000 omh, un botón con una resistencia de 1000 omh en cualquiera de sus dos configuraciones ([Pull Up y Pull Down](https://programarfacil.com/blog/arduino-blog/resistencia-pull-up-y-pull-down/)). ([Esquema del circuito](https://www.tinkercad.com/things/9XWyWrFgkkV?sharecode=Ka9XmmV3m_KzQQjAy5YmmUiR6ohsYwO3UxPosGOeJ8s))

- Configuraciones.

    Para este proyecto definiremos un pin digital como salida y otro como entrada, usando la función `pinMode()` y activaremos la comunicación serial con `begin()`. Recuerda que las configuraciones deben encontrar en el interior del `setup`.  

    ```
        Serial.begin(9600);

        pinMode(LED_BUILTIN, OUTPUT);
        pinMode(2, INPUT);
    ```

- Ciclo de vida de nuestra aplicación.

    Para usar como entrada o salida un pin digital en Arduino usamos `digitalWrite() y digitalRead()`, para temporizar una tarea `delay()` y para mostrar un mensaje en nuestra consola usamos `println`.

    Primero debemos definir una variable para guardar el estado del botón, para ello lo definiremos de manera global (Parte superior de nuestro condigo y fuera de todas las funciones).

    ```
    int buttonState = 0;
    ```

    Segundo paso leeremos el estado de nuestro botón. Recuerda que esto hace parte del ciclo de vida de nuestra aplicación, por lo que debe estar en el `loop`.

    ```
    buttonState = digitalRead(2);
    ```

    Tercero escribimos la lógica que nos permite decidir si encender a apagar nuestro LED, cuando presionemos el botón. 

    ```
    if (buttonState == HIGH) {
        // turn LED on
        digitalWrite(LED_BUILTIN, HIGH);
  } else {
        // turn LED off
        digitalWrite(LED_BUILTIN, LOW);
  }
    delay(10);
    ```

    Y por último analizar donde agregar la función `println` para mostrar un mensaje cada vez que presiones el botón.

## Hola Mundo (Experto)

Ya que conocemos como controlar un LED con Arduino y usar un botón para activarlo, es hora de conocer Como usar las salidas analógicas.

- Diseñar el circuito.

    El circuito a emplear debe contener un LED con una residencia de 1000 omh, un botón con una resistencia de 1000 omh en cualquiera de sus dos configuraciones ([Pull Up y Pull Down](https://programarfacil.com/blog/arduino-blog/resistencia-pull-up-y-pull-down/))([Esquema del circuito](https://www.tinkercad.com/things/cGuROltb4rT?sharecode=J1lEpTN9lD9VCD8rz8h7MN-YtgWe6NwTfsCsBsa9-W8))

- Configuraciones.

    La configuración para este proyecto no cambian de las realizadas en el proyecto anterior a acepción de la definición del pin de salida que debe ser PWM. 

- Ciclo de vida de nuestra aplicación.

    Para este proyecto deberemos definir una nueva variable global para controlar el brillo de nuestro LED.

    ```
    int brightness = 0;
    ```

   Y adaptar nuestro bucle para que envés de encenderse y apagarse nuestro LED al presionar el botón, este altere su brillo del mínimo al máximo y del máximo al mínimo, cuando se presiona el botón. 

   Esta nueva lógica debe reemplazar simplemente la lógica de encendido de nuestro led. 

   ```
   for (brightness = 0; brightness <= 255; brightness += 5) {
        analogWrite(9, brightness);
        delay(50); // Wait for 30 millisecond(s)
    }
    
    for (brightness = 255; brightness >= 0; brightness -= 5) {
        analogWrite(9, brightness);
        delay(50); // Wait for 30 millisecond(s)
    }
   ```