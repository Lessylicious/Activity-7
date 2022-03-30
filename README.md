# Activity-7
/*Create an Automated Coooling System Device
that ables to control a cooling Fan. 
This device should have 3 LED lights to signify 
Temperature Levels

Red- Hot/High temperature,
Green- Room temperature/ Medium Temparature
Yello- Cold/ lower than room Temperature.

A buzzer will emits emergency Sound Signal 
if room teprature is below 27C or above 37C*/

//Lester P. Calub BSIT-2B

//Pin Setup
int celsius = 0;
int green = 2;
int yellow = 3;
int red = 4;
int buzzer = 5;
int fan = 6;
int sensorPin = A0;
int thresholdValue = 0;
void fanOn(){
	digitalWrite(fan, HIGH);
}
void fanOff(){
	digitalWrite(fan, LOW);
}
void setup()
{
  pinMode(sensorPin, INPUT);
  Serial.begin(9600);
  pinMode(green, OUTPUT);
  pinMode(yellow, OUTPUT);
  pinMode(red, OUTPUT);
  pinMode(fan, OUTPUT);
  pinMode(buzzer, OUTPUT);
}

void loop(){
	 int reading = analogRead(sensorPin);
   float voltage = reading * 5.0;
   voltage /= 1024.0;
   celsius = (voltage - 0.5) * 100 ;
   
   Serial.print("Surrounding temperature is ");
   Serial.print(celsius);
   Serial.println(" C ");
   
  
  //Red Light
   if (celsius > 37 ){
     digitalWrite(green,LOW);
      digitalWrite(yellow,LOW);
      digitalWrite(red,HIGH);
     digitalWrite(buzzer,HIGH);
     fanOn();
   }
  //Green Light
    if (celsius >27 && celsius <37 ){
     digitalWrite(green,HIGH);
      digitalWrite(yellow,LOW);
      digitalWrite(red,LOW);
      fanOff();
      digitalWrite(buzzer,LOW);
   }
  //Yellow Light
   if (celsius <27 ){
     digitalWrite(green,LOW);
      digitalWrite(yellow,HIGH);
      digitalWrite(red,LOW);
      fanOff();
     digitalWrite(buzzer,HIGH);
   }
  }
