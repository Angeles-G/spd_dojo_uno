/*
2 - LA SEGUNDA ENTREGA AGREGA LO SIGUIENTE EN UN NUEVO PROYECTO, 
8-  Durante el amarillo: Tiene que sonar 1 vez por segundo en un tono SUAVE. 
9- Al cambiar de verde a amarillo debe titilar 3 veces el verde antes de pasar al amarillo
10- Al cambiar de amarillo a rojo se debe titilar 3 veces el amarillo
11- Al cambiar de rojo a Amarillo se debe titilar 3 veces el rojo
12- Al cambiar de amarillo a verde se debe titilar 3 veces el amarillo.
*/

//leds
#define LEDROJO1 13
#define LEDROJO2 12
#define LEDAMARILLO1 11
#define LEDAMARILLO2 10
#define LEDVERDE1 9
#define LEDVERDE2 8
//buzzer
#define BUZZER 7
//frecuencias
#define FRROJO 1000
#define FRAMARILLO 500
#define FRVERDE 0
//milisegundos
#define MILISROJOVERDE 250
#define MILISAMARILLO 500

void setup()
{
  Serial.begin(9600);
  pinMode(LEDROJO1, OUTPUT);
  pinMode(LEDROJO2, OUTPUT);
  pinMode(LEDAMARILLO1, OUTPUT);
  pinMode(LEDAMARILLO2, OUTPUT);
  pinMode(LEDVERDE1, OUTPUT);
  pinMode(LEDVERDE2, OUTPUT);
  pinMode(BUZZER, OUTPUT);
}

void loop()
{
  titilarRojoVerde(10, LEDROJO1, LEDROJO2, BUZZER, FRROJO, MILISROJOVERDE, 3, 500);
  titilarAmarillo(3, LEDAMARILLO1, LEDAMARILLO2, BUZZER, FRAMARILLO, MILISAMARILLO, 800, 200);
  titilarRojoVerde(10, LEDVERDE1, LEDVERDE2, BUZZER, FRVERDE, MILISROJOVERDE, 3, 500);
  titilarAmarillo(3, LEDAMARILLO1, LEDAMARILLO2, BUZZER, FRAMARILLO, MILISAMARILLO, 800, 200);
}

//funcion que enciende las leds sin un tiempo de delay.
void encenderSinDelay(int led1, int led2)
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
}

//funcion que enciende las leds normalmente con delay.
void encender(int led1, int led2, int tiempo)
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  delay(tiempo);
}

//funcion que apaga las leds normalmente con delay.
void apagar(int led1, int led2, int tiempo)
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  delay(tiempo);
}

//funcion que suena el buzzer y titila las leds ROJOS o VERDES segun las iteraciones, los milisegundos del Buzzer y el tiempo de delay. (en caso del VERDE, hay que ingresar "0" a la frecuencia para que no suene).
//      8 parametros (cantidad de iteraciones en el "for", primer led, segundo led, pin del buzzer, frecuencia del tono del buzzer, milisegundos del buzzer, iteracion que le das al "if" para titilar las leds, tiempo que mantiene el buzzer y las leds encendidos o apagados).
void titilarRojoVerde(int iteracionesFor, int led1, int led2, int buzzer, int frecuencia, int milis, int iteracionIf, int tiempo)
{
  for(int i=0; i<iteracionesFor; i++){
    Serial.println(i);
    encenderSinDelay(led1, led2);
    tone(BUZZER, frecuencia, milis);
    
    if(i<iteracionIf){
      delay(tiempo);
    }else{
      if(i%2 == 1){
        apagar(led1, led2, tiempo);
      }else{
        if(i%2 == 0){
          encender(led1, led2, tiempo);
        }
      }
    }
  }
}

//funcion que suena el buzzer y titila las leds AMARILLAS. Lo mismo que la anterior funcion, solo que "iteracionesIf" no existe. "tiempo" lo cambiamos por "tiempo1" y le agregamos "tiempo2".
//      8 parametros (parametros con misma logica de la anterior funcion. "tiempo1" representa el delay para encender led y "tiempo2" para el apagado.
void titilarAmarillo(int iteracionesFor, int led1, int led2, int buzzer, int frecuencia, int milis, int tiempo1, int tiempo2)
{
  for(int i=0; i<iteracionesFor; i++){
    Serial.println(i);
    tone(buzzer, frecuencia, milis);
  	encender(led1, led2, tiempo1);
  	apagar(led1, led2, tiempo2);
  }