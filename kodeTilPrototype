//vi importerer CapacitiveSensor biblioteket skrevet av Paul Badger for implementasjon av //touch funksjonalitet

#include <CapacitiveSensor.h>
CapacitiveSensor button = CapacitiveSensor(4,2); 


//pinsene defineres som i kilden vår og i setup da vi syns det var mest lesbart (Aqib, 2018)
int red_light_pin= 9; 
int blue_light_pin = 10;
int green_light_pin = 11;

int readValue = 0;
boolean isTouched = false;
int threshold = 1000; //forteller arduino når den skal finne en puls
//et høyt tall reduserer sensitiviteten, men et mindre tall øker sensitiviteten til touch-funksjonen

//all lights turn off
void allLightsOff(){
      digitalWrite(red_light_pin, LOW);
      digitalWrite(blue_light_pin, LOW);
      digitalWrite(green_light_pin, LOW);
      delay(500); 
}

void setup() {
  pinMode(red_light_pin, OUTPUT);
  pinMode(green_light_pin, OUTPUT);
  pinMode(blue_light_pin, OUTPUT);
  Serial.begin(9600); // for visning av verdier i monitor
}


void loop() {
  long sensorValue = button.capacitiveSensor(100); //setter value for knappen basert på touch registrert
  
  Serial.println(sensorValue);
  
  Serial.println(isTouched); 

  //hvis value som blir registrert er større enn 1000, og hvis lampen er skrudd av, så vil lampen skru seg på fordi det betyr at bruker har touchet og ønsker å skru lampen på.
  if (sensorValue > threshold && isTouched == false){
    isTouched = true;
  }
  //hvis value som blir registrert er større enn 1000, og hvis lampen er på fra før av, så vil lampen skrur seg av fordi dette betyr at den var på og bruker forsøker å skru av lampen ved touch.
  else if(sensorValue > threshold && isTouched == true){
      isTouched = false;
      allLightsOff(); //alle LED-lys skal stoppe å lyse
  }

//koden under kjører dersom lampen er på, readValue leser verdi fra bryteren festet til potensiometeret (fra 0 til 1025) 
//og relevante lysfarger velges basert på brukers interaksjon med bryteren

  if (isTouched){
  readValue = analogRead(A0); //potensiometer 

    //hvis lyset slås på og value er mellom 0 og 203 inklusiv så skal det lyses hvitt 
    if (204 > readValue){
      digitalWrite(red_light_pin, HIGH);
      digitalWrite(blue_light_pin, HIGH);
      digitalWrite(green_light_pin, HIGH);
    }
    
    //hvis value er større enn 203, og mindre enn 410, så skal det lyses rødt
    if(203 < readValue && readValue < 410){
      digitalWrite(red_light_pin, HIGH);      
      digitalWrite(blue_light_pin, LOW);
      digitalWrite(green_light_pin, LOW);
      }
      
    //hvis value er større enn 409, og mindre enn 615, så skal det lyses gult
    if(409 < readValue && readValue < 615){
      digitalWrite(red_light_pin, HIGH);      
      digitalWrite(blue_light_pin, LOW);
      digitalWrite(green_light_pin, HIGH);
      }

    //hvis value er større enn 614, og mindre enn 820, så skal det lyses grønt
    if(614 < readValue && readValue < 820){
      digitalWrite(red_light_pin, LOW);      
      digitalWrite(blue_light_pin, LOW);
      digitalWrite(green_light_pin, HIGH);
      }

    //hvis value er større enn 819, og mindre enn 1025, så skal det lyses blått    
    if(819 < readValue && readValue < 1025){
      digitalWrite(red_light_pin, LOW);      
      digitalWrite(blue_light_pin, HIGH);
      digitalWrite(green_light_pin, LOW);
      }
    //legger inn delay for å sikre at bruker rekker å ta bort fingeren fra touchområdet
    delay(250);
  }
}
  

