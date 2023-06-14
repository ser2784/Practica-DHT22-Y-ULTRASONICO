# Practica DHT22 Y ULTRASONICO
Este repositorio muestra como podemos programar una ESP32 con el sensor DHT11.

## Introducción

### Descripción

La ```Esp32``` la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (```DTH22  Y HC-SR84```) para adquirir temperatura y humedad del entorno; Cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/).


## Material Necesario

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- Sensor DHT22
- HC-SR84
- DGN
- LCD 16X2
- VCC




## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Abrir la terminal de programación y colocar la siguente programación:

```
#include <LiquidCrystal_I2C.h>
#include "DHTesp.h"
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int Trigger = 14;   //Pin digital 2 para el Trigger del sensor
const int Echo = 26;   //Pin digital 3 para el Echo del sensor

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);
void setup() {
  Serial.begin(9600);
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print(" Cm");
  Serial.println();
  delay(1000);          //Hacemos una pausa de 100ms

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
   delay(1000); 

  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) +"Cm ");
  lcd.setCursor(0, 1);
  lcd.print(" ING.SERGIO RB ");
  delay(1000);          //Hacemos una pausa de 100ms
  
  lcd.setCursor(0, 0);
  lcd.println("  Temp: " + String(data.temperature, 1) + " C ");
  lcd.setCursor(0, 1);
  lcd.println("  Humidity: " + String(data.humidity, 1) + "%");
  lcd.println("---");
   delay(1000);  
}


```
2. Instalar la libreria de **DHT sensor library for ESPx** como se muestra en la siguente imagen.

![](https://github.com/ser2784/Practica-DHT22-Y-ULTRASONICO/blob/main/Practica%20DHT22%20Y%20ULTRASONICO%20LIBRERIA.png)

3. Hacer la conexion de **DHT22 Y HC-SR84** con la **ESP32** como se muestra en la siguente imagen.

![](https://github.com/ser2784/Practica-DHT22-Y-ULTRASONICO/blob/main/Practica%20DHT22%20Y%20ULTRASONICO%20DIAGRAMA.png)

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
3. Colocar la temperatura y humedad dando *doble click* al sensor **DHT22**
4. cColocas la distancia a medir en el **HC-SR84**
5. Posterior en el **LCD** muetras los datos 

## Resultados

Cuando haya funcionado, verás los valores dentro del monitor serial como se muestra en la siguente imagen.

![](https://github.com/ser2784/Practica-DHT22-Y-ULTRASONICO/blob/main/Practica%20DHT22%20Y%20ULTRASONICO%20NOMBRE.png)
![](https://github.com/ser2784/Practica-DHT22-Y-ULTRASONICO/blob/main/Practica%20DHT22%20Y%20ULTRASONICO%20TEMPERATURA.png)



## Evidencias

[Video de Youtube](por el momento no contamos con el video )


# Créditos

Desarrollado por Ing. Sergio Rivera

- [GitHub](https://github.com/ser2784)