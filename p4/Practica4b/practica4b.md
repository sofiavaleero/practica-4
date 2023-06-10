## Practica 4 Parte 2
***Raul Gonzalez / Sofia Valero***
## Codigo:

```
#include "BluetoothSerial.h"
#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
#endif
BluetoothSerial SerialBT;
void setup() {
Serial.begin(115200);
SerialBT.begin("ESP32test"); //Bluetooth device name
Serial.println("The device started, now you can pair it with bluetooth!");
}
void loop() {
if (Serial.available()) {
SerialBT.write(Serial.read());
}
if (SerialBT.available()) {
Serial.write(SerialBT.read());
}
delay(20);
}

```
### Salida:

Este codigo proporcionado hace la funcion de conectar el microprocesador con un dispositivo bluetooth y tras conectarse con el, es capaz de leer en pantalla lo que se escribe desde el telefono con el que se ha conectado y viceversa.

![](demostracionbluetooth.mp4)

### Funcionamiento del Programa:
Para que el programa funcione necesitamos añadir la libreria *BluetoothSerial.h*, esta libreria se encarga de que el modem bluetooth del esp32 se active y se pueda conectar a otros dispositivos.
```
#include "BluetoothSerial.h"

```

Posteriormente le damos un nombre a la placa que en este caso ha sido *ESP32test* y hacemos que nos enseñe un mensaje indicando que ya se puede conectar mediante bluetooth.<br>
```

void setup() {
Serial.begin(115200);
SerialBT.begin("ESP32test"); //Bluetooth device name
Serial.println("The device started, now you can pair it with bluetooth!");
}

```
<br>

```

void loop() {
if (Serial.available()) {
SerialBT.write(Serial.read());
}
if (SerialBT.available()) {
Serial.write(SerialBT.read());
}
delay(20);
}

```

Por ultimo en el loop tenemos el funcionamiento del programa, hace que cuando el serialBT escriba entonces el serial lea y lo mismo pero al reves para que se puedan comunicar los dos dispositivos.
