#include <SoftwareSerial.h>
#include <LiquidCrystal.h> //library for LCD
#include <DHT.h>
SoftwareSerial mySerial(1, 0);// RX=1 and TX=0
// initialize the library with the numbers of the interface pins 
LiquidCrystal lcd(11, 10, 9, 8, 5, 4); 
// defines pins numbers
#define DHT11_Pin 13
DHT dht(DHT11_Pin,DHT11);
const int MoistureSensorPin=A0;
int WaterPump=6;
int Moisture;
int Temp;
int Humid;

void setup() {
  // put your setup code here, to run once:
  mySerial.begin(9600);// Setting the baud rate of GSM Module 
  Serial.begin(9600);// Setting the baud rate of Serial Monitor (Arduino)
  delay(100);
  lcd.begin(20, 4); // set up the LCD's number of columns and rows:
  dht.begin();
  lcd.setCursor(0,0); // set the cursor position:
  lcd.print("  DESIGNED BY PLT    ");
  //lcd.setCursor(0,2);
  //lcd.print(" IRRIGATION FARMING ");
  pinMode(MoistureSensorPin, INPUT);
  pinMode(WaterPump, OUTPUT);
  pinMode(DHT11_Pin,INPUT);
}

void loop() 
{
  // put your main code here, to run repeatedly:
  
 //if (mySerial.available()>0)
   //Serial.write(mySerial.read());
  
  DHTSensor();
  MoistureSensor();

  if (Moisture<=50 && Temp>=30 && Humid<=60)
  {
   SendMessage1();
   delay(100);
   //ReceiveMessage();
  }
  else
  {
   SendMessage2();
   delay(100);
  }
}

void SendMessage1()
{
  mySerial.println("AT+CMGF=1");    //Sets the GSM Module in Text Mode
  delay(1000);  // Delay of 1000 milli seconds or 1 second
  mySerial.println("AT+CMGS=\"+254701344802\"\r"); // Replace with mobile number
  delay(1000);
  // Prints Message on the serial (Virtual Phone)
  Serial.print("Soil Moisture: "); 
  Serial.print(Moisture);
  Serial.println("%   "); 
  Serial.print("Temperature: ");
  Serial.print(Temp);
  Serial.println("C");
  Serial.print("Humidity: ");
  Serial.print(Humid);
  Serial.println("%");
  //mySerial.println("The farm is running dry!!!");// The SMS text you want to send
  Serial.println("Dear Farmer,your farm condition is not good!!");// The SMS text you want to send
  Serial.println("Please, send letter 'S' to turn ON the water pump.");
  //digitalWrite(WaterPump, HIGH);
  delay(1000);
  digitalWrite(WaterPump, HIGH);
  Serial.println("Water Pump turned ON!!"); 
  mySerial.println("AT+CNMI=2,2,0,0,0");//recive SMS
  delay(1000);
  if (Serial.available()>0)
  switch(Serial.read())
  {
    case 's':
      digitalWrite(WaterPump, HIGH);
      //SendMessage2();
      break;
    case 'n':
      digitalWrite(WaterPump, LOW);
      //break;
  }
  mySerial.println((char)26);// ASCII code of CTRL+Z
  delay(1000);
}

void SendMessage2()
{
  mySerial.println("AT+CMGF=1");    //Sets the GSM Module in Text Mode
  delay(1000);  // Delay of 1000 milli seconds or 1 second
  mySerial.println("AT+CMGS=\"+254701344802\"\r"); // Replace with mobile number
  delay(1000);
  // Prints Message on the serial (Virtual Phone)
  Serial.print("Soil Moisture: "); 
  Serial.print(Moisture);
  Serial.println("%   "); 
  Serial.print("Temperature: ");
  Serial.print(Temp);
  Serial.println("C");
  Serial.print("Humidity: ");
  Serial.print(Humid);
  Serial.println("%");
  //mySerial.println("The farm is running dry!!!");// The SMS text you want to send
  Serial.println("Dear Farmer,your farm condition is okay!!");// The SMS text you want to send
  Serial.println("No water is needed, thank you.");
  digitalWrite(WaterPump, LOW);
  Serial.println("Water Pump turned OFF!!");
  delay(100);
  mySerial.println((char)26);// ASCII code of CTRL+Z
  delay(1000);
}

void DHTSensor()
{
  float Temperature=dht.readTemperature();
  float Humidity=dht.readHumidity();
  Temp=Temperature;
  Humid=Humidity;
  lcd.setCursor(0,2);
  lcd.print("Temperature: ");
  lcd.print(Temp);
  lcd.print("C");
  lcd.setCursor(0,3);
  lcd.print("Humidity: ");
  lcd.print(Humid);
  lcd.print("%");
  delay(1000);
}

void MoistureSensor()
{
  int Val = analogRead(MoistureSensorPin);
    // Prints Message on the LCD
  Moisture = map(Val,0,1023,0,100);
  lcd.setCursor(0,1); 
  lcd.print("Soil Moisture: "); 
  lcd.print(Moisture);
  lcd.print("%   "); 
  delay(1000);
}
/*void ReceiveMessage()
{
  mySerial.println("AT+CNMI=2,2,0,0,0");//recive SMS
  delay(1000);
  if (Serial.available()>0)
  switch(Serial.read())
  {
    case 's':
      digitalWrite(WaterPump, HIGH);
      //SendMessage2();
      break;
    case 'n':
      digitalWrite(WaterPump, LOW);
      //break;
  }
}*/

    /*if (Serial.available()>0)
  switch(Serial.read())
  {
    case 's':
      analogWrite(WaterPump, HIGH);
      SendMessage2();
      break;
    //case 'I':
      //analogWrite(WaterPump, LOW);
      //break;
  }
  }
  else
  {
    analogWrite(WaterPump, LOW);
    SendMessage3();
  }

}
void ReciveMessage()
{
  mySerial.println("AT+CNMI=2,2,0,0,0");//recive SMS
  delay(1000);
}
void SendMessage1()
{
  mySerial.println("AT+CMGF=1");    //Sets the GSM Module in Text Mode
  delay(1000);  // Delay of 1000 milli seconds or 1 second
  mySerial.println("AT+CMGS=\"+254701344802\"\r"); // Replace with mobile number
  delay(1000);
  //mySerial.println("The farm is running dry!!!");// The SMS text you want to send
  Serial.println("The farm is running dry!!!");// The SMS text you want to send
  delay(100);
  mySerial.println((char)26);// ASCII code of CTRL+Z
  delay(1000);
}
void SendMessage2()
{
  mySerial.println("AT+CMGF=1");    //Sets the GSM Module in Text Mode
  delay(1000);  // Delay of 1000 milli seconds or 1 second
  mySerial.println("AT+CMGS=\"+254701344802\"\r"); // Replace with mobile number
  delay(1000);
  mySerial.println("The water pump is running!!!");// The SMS text you want to send
  delay(100);
  mySerial.println((char)26);// ASCII code of CTRL+Z
  delay(1000);
}
void SendMessage3()
{
  mySerial.println("AT+CMGF=1");    //Sets the GSM Module in Text Mode
  delay(1000);  // Delay of 1000 milli seconds or 1 second
  mySerial.println("AT+CMGS=\"+254701344802\"\r"); // Replace with mobile number
  delay(1000);
  mySerial.println("The water pump has stopped!!!");// The SMS text you want to send
  delay(100);
  mySerial.println((char)26);// ASCII code of CTRL+Z
  delay(1000);
}
*/
