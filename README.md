# pocosaludable
𝑹.𝑷.𝑺 𝒅𝒂 𝒇𝒊𝒔𝒉𝒊𝒏
Modulo Sensor De Color Tcs3200
Microcontrolador: TCS3200
Voltaje de funcionamiento: 2.7-5.5V
Voltaje mínimo de entrada recomendado: 3-3V
Voltaje máximo de entrada recomendado: 5V
Voltaje mínimo de entrada límite: 3V
Voltaje máximo de entrada límite: 5V
El sensor de color con integrado TCS230 puede filtrar los datos RGB de la fuente de luz y la convierten en una onda cuadrada (50% ciclo de trabajo) con una frecuencia directamente proporcional a la intensidad de la luz de radiación. La frecuencia de salida se puede escalar por uno de los tres valores prestablecidos a través de dos pines de control de entrada S0 y S1, con opciones seleccionables del 2%, 20% y 100% de frecuencia; los pines S2 y S3 sirven para controlar el filtro de RGB.
- Opera desde una sola fuente de alimentación de 2.7 a 5.5V
- Escala la frecuencia de salida
- Pin de apagado de funciones.
- Error no lineal de 0.2% a 50 kHz.
- Alta Resolución de conversión de la intensidad de luz a frecuencia.
- Modo de bajo consumo de energía.
- Leds incluidos en el PCB para iluminar el objeto a reconocer.
- Se comunica directamente con un microcontrolador (PIC, Arduino, etc.)

  //
// Cableado de TCS3200 a Arduino
//
#define S0 8
#define S1 9
#define S2 12
#define S3 11
#define salidaSensor 10

// Para guardar las frecuencias de los fotodiodos
int frecuenciaRojo = 0;
int frecuenciaVerde = 0;
int frecuenciaAzul = 0;

void setup() {
  // Definiendo las Salidas
  pinMode(S0, OUTPUT);
  pinMode(S1, OUTPUT);
  pinMode(S2, OUTPUT);
  pinMode(S3, OUTPUT);
  
  // Definiendo salidaSensor como entrada
  pinMode(salidaSensor, INPUT);
  
  // Definiendo la escala de frecuencia a 20%
  digitalWrite(S0,HIGH);
  digitalWrite(S1,LOW);
  
   // Iniciar la comunicacion serie 
  Serial.begin(9600);
}
void loop() {
  // Definiendo la lectura de los fotodiodos con filtro rojo
  digitalWrite(S2,LOW);
  digitalWrite(S3,LOW);
  
  // Leyendo la frecuencia de salida del sensor
  frecuenciaRojo = pulseIn(salidaSensor, LOW);
  
  // Mostrando por serie el valor para el rojo (R = Red)
  Serial.print("R = ");
  Serial.print(frecuenciaRojo);
  delay(100);
  
  // Definiendo la lectura de los fotodiodos con filtro verde
  digitalWrite(S2,HIGH);
  digitalWrite(S3,HIGH);
  
  // Leyendo la frecuencia de salida del sensor
  frecuenciaVerde = pulseIn(salidaSensor, LOW);
  
  // Mostrando por serie el valor para el verde (G = Green)
  Serial.print(" G = ");
  Serial.print(frecuenciaVerde);
  delay(100);
 
  // Definiendo la lectura de los fotodiodos con filtro azul
  digitalWrite(S2,LOW);
  digitalWrite(S3,HIGH);
  
  // Leyendo la frecuencia de salida del sensor
  frecuenciaAzul = pulseIn(salidaSensor, LOW);
  
  // Mostrando por serie el valor para el azul (B = Blue)
  Serial.print(" B = ");
  Serial.println(frecuenciaAzul);
  delay(100);
}
//
// Cableado de TCS3200 a Arduino
//
#define S0 8
#define S1 9
#define S2 12
#define S3 11
#define salidaSensor 10

// Para guardar las frecuencias de los fotodiodos
int frecuenciaRojo = 0;
int frecuenciaVerde = 0;
int frecuenciaAzul = 0;
int colorRojo;
int colorVerde;
int colorAzul;

void setup() {
  // Definiendo las Salidas
  pinMode(S0, OUTPUT);
  pinMode(S1, OUTPUT);
  pinMode(S2, OUTPUT);
  pinMode(S3, OUTPUT);
  
  // Definiendo salidaSensor como entrada
  pinMode(salidaSensor, INPUT);
  
  // Definiendo la escala de frecuencia a 20%
  digitalWrite(S0,HIGH);
  digitalWrite(S1,LOW);
  
   // Iniciar la comunicacion serie 
  Serial.begin(9600);
}

void loop() {
  // Definiendo la lectura de los fotodiodos con filtro rojo
  digitalWrite(S2,LOW);
  digitalWrite(S3,LOW);
  
  // Leyendo la frecuencia de salida del sensor
  frecuenciaRojo = pulseIn(salidaSensor, LOW);

  // Mapeando el valor de la frecuencia del ROJO (RED = R) de 0 a 255
  // Usted debe colocar los valores que registro. Este es un ejemplo: 
  // colorRojo = map(frecuenciaRojo, 70, 120, 255,0);
  colorRojo = map(frecuenciaRojo, xx, xx, 255,0);
  
  // Mostrando por serie el valor para el rojo (R = Red)
  Serial.print("R = ");
  Serial.print(colorRojo);
  delay(100);
  
  // Definiendo la lectura de los fotodiodos con filtro verde
  digitalWrite(S2,HIGH);
  digitalWrite(S3,HIGH);
  
  // Leyendo la frecuencia de salida del sensor
  frecuenciaVerde = pulseIn(salidaSensor, LOW);

  // Mapeando el valor de la frecuencia del VERDE (GREEN = G) de 0 a 255
  // Usted debe colocar los valores que registro. Este es un ejemplo: 
  // colorVerde = map(frecuenciaVerde, 100, 199, 255,0);
  colorVerde = map(frecuenciaVerde, xx, xx, 255,0);

  // Mostrando por serie el valor para el verde (G = Green)
  Serial.print("G = ");
  Serial.print(colorVerde);
  delay(100);
 
  // Definiendo la lectura de los fotodiodos con filtro azul
  digitalWrite(S2,LOW);
  digitalWrite(S3,HIGH);
  
  // Leyendo la frecuencia de salida del sensor
  frecuenciaAzul = pulseIn(salidaSensor, LOW);

  // Mapeando el valor de la frecuencia del AZUL (AZUL = B) de 0 a 255
  // Usted debe colocar los valores que registro. Este es un ejemplo: 
  // colorAzul = map(frecuenciaAzul, 38, 84, 255, 0);
  colorAzul = map(frecuenciaAzul, xx, xx, 255, 0);
  
  // Mostrando por serie el valor para el azul (B = Blue)
  Serial.print("B = ");
  Serial.print(colorAzul);
  delay(100);

  // Comprobar cual es el color detectado y mostrarlo
  // con un mensaje en el monitor serie
  if(colorRojo > colorVerde && colorRojo > colorAzul){
      Serial.println(" - Detectado ROJO");
  }
  if(colorVerde > colorRojo && colorVerde > colorAzul){
    Serial.println(" - Detectado VERDE");
  }
  if(colorAzul > colorRojo && colorAzul > colorVerde){
    Serial.println(" - Detectado AZUL");
  }
}

Valentina Barrios
