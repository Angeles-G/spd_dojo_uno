/Ángeles Belén García - 1B - Turno mañana 
/*
ENUNCIADO DEL EJERCICIO:1

1 - LA PRIMER  ENTREGA SERÁ LO SIGUIENTE, 
1- El semáforo tiene que tener 2 leds de cada color como mínimo,
en caso de que uno se  rompa. 
2- Tiene que implementar los tiempos correctos como se detallan 
a continuación. 
3- El verde dura 5 segundos. 
4- El amarillo dura 3 segundos. 
5- Rojo dura 5 segundos. 
6- Tiene que tener señalización para personas no videntes 
como se detalla a continuación. (Buzzer o piezo)
7- Durante el rojo: Tiene que sonar 2 vez por segundo 
en un tono FUERTE.

*/

// definimos los pines que utilizamos
#define LED_ROJO 13
#define LED_ROJODOS 11
#define LED_AMARILLO 8
#define LED_AMARILLODOS 7
#define LED_VERDE 4
#define LED_VERDEDOS 2
#define BUZZER 5

//definimos variables: 
int tiempo_verde_rojo;
int tiempo_amarillo;

void setup()
{
  pinMode(LED_ROJO, OUTPUT);
  pinMode(LED_VERDE, OUTPUT);
  pinMode(LED_AMARILLO, OUTPUT);
  pinMode(LED_ROJODOS, OUTPUT);
  pinMode(LED_VERDEDOS, OUTPUT);
  pinMode(LED_AMARILLODOS, OUTPUT);
  pinMode(BUZZER, OUTPUT);
  tiempo_verde_rojo = 5000;
  tiempo_amarillo = 3000;
  Serial.begin(9600); 
  
}

//Se introduce las variables para hacer el juego de luces
//con sus descripción en el serial
void loop()
{
  Serial.println("se prenden las luces rojas");
  Serial.println("Se enciende el buzzer");
  encender_apagar_semaforo(LED_ROJO, LED_ROJODOS, tiempo_verde_rojo);
  Serial.println("se prenden las luces amarillas");
  encender_apagar_semaforo(LED_AMARILLO, LED_AMARILLODOS, tiempo_amarillo);
  Serial.println("se prenden las luces verdes");
  encender_apagar_semaforo(LED_VERDE, LED_VERDEDOS, tiempo_verde_rojo);
  Serial.println("se prenden las luces amarillas");
  encender_apagar_semaforo(LED_AMARILLO, LED_AMARILLODOS, tiempo_amarillo);
}

//Se realiza la función de prender,que recibe como parametros
//los luces que queremos prender
void encender(int led, int led_dos, int tiempo)
{
  Serial.println("Enciendo led"); 
  digitalWrite(led, HIGH);
  digitalWrite(led_dos, HIGH);
  
  if (led == LED_ROJO)
  {
    prenderBuzzer();
  }
  else{
    delay (tiempo);
  } 
}

//Se realiza la función de apagar,que recibe como parametros
//los luces que queremos apagar  
void apagar(int led, int led_dos)
{
  Serial.println("Apago led");
  digitalWrite(led, LOW);
  digitalWrite(led_dos, LOW);
}

//Se hace una funcion donde se junten tanto la funcion de prender
// y apagar las luces. Recibe como parametros las luces que
//queremos prender.
void encender_apagar_semaforo(int led, int led_dos, int tiempo)
{
  Serial.println("Sucuencia");
  encender(led, led_dos, tiempo);
  apagar(led, led_dos);
}

//Se reliza la funcion de repeticion del buzzer mediante un 
//siclo for para que suene mientras las luces rojas esten
//prendidas
void prenderBuzzer(){
    for(int i = 0; i<10;i++){
  	 tone(BUZZER, 10, 1000);
  	 delay(500);
  	 digitalWrite(BUZZER,LOW);
  }
}
