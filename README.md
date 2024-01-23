# PRACTICA-5
ESTA PRACTICA NOS ENSEÑA COMO PROGRAMAR ESP32 CON SENSOR ULTRASONICO, PANTALLA LCD Y SENSOR DHT.

## INTRODUCCION 
LA ESP32 SE UTILIZA COMO UNA TARJETA DE DATOS , AL CUAL SE LE ANEXARA UN SENSOR ULTRASONICO QUE MIDE LA PROXIMIDAD DE LOS OBJETOS, EL SENSOR DHT11(SE UTILIZA PARA MEDIR TEMPERATURA Y HUMEDAD ).
### MATERIAL NECESARIO 

WOKWI
TARJETA ESP 32
SENSOR DHT11
HC-SR04 Ultrasonic Distance Sensor
LCD 16x2 (I2C)

#### INSTRUCCIONES
YA ESTANDO DENTRO DE LA PLATAFORMA WOKWI SE ANEXARA EL SIGUIENTE ALGORITMO:
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

DHTesp dhtSensor;

const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 2;   //Pin digital 3 para el Echo del sensor
const int DHT_PIN = 17;
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
   Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();
}

void loop()
{

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---"); 
  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros
 
  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trigger, LOW);

  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo en cm

  lcd.setCursor(0, 0);
  lcd.print("Temp: " + String(data.temperature, 1) + "\xDF"+"°C");
  lcd.setCursor(0, 1);
  lcd.print("Humidity: " + String(data.humidity, 1) + "%");
  lcd.print("Wokwi Online IoT");
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("Dis:" + String(d) + "CM" );

  delay(2000);
  lcd.clear();
  delay(2000);
  lcd.clear();


 

  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) + "cm  ");
  lcd.print("Wokwi Online IoT");
  delay(2000);
  lcd.clear();

  
  

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("ARMANDO  GL");
  lcd.setCursor(0, 1);
  lcd.print("INDUSTRIAL");
  delay(2000);
  lcd.clear();

}

"INSTALAR LOS SENSORES A UTILIZAR O REQUERIDOS "
"REALIZAR LAS CONEXIONES DE LOS COMPONENTES "
![](https://github.com/ArmandoGl98/PRACTICA-5/blob/main/Captura%20de%20pantalla%202024-01-22%20201215.png)

ESTE ES EL RESULTADO FINAL DE ESTA PRACTICA :
![](https://github.com/ArmandoGl98/PRACTICA-5/blob/main/Captura%20de%20pantalla%202024-01-22%20194635.png)
![](https://github.com/ArmandoGl98/PRACTICA-5/blob/main/Captura%20de%20pantalla%202024-01-22%20194546.png)
![](https://github.com/ArmandoGl98/PRACTICA-5/blob/main/Captura%20de%20pantalla%202024-01-22%20194532.png)
