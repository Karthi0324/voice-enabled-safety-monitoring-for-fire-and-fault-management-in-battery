
//USER NAME : atvproject24@gmail.com
//PASSWORD: iotproject2024

#define BLYNK_TEMPLATE_ID "TMPL31YeurSPY"
#define BLYNK_TEMPLATE_NAME "EV Battery Monitoring"
#define BLYNK_AUTH_TOKEN "LPo7I5nWze6f-Ci1XHXt-v_gBpK9H-KE"

/* Comment this out to disable prints and save space */
#define BLYNK_PRINT Serial


#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>

// Your WiFi credentials.
// Set password to "" for open networks.
char ssid[] = "projectiot";
char pass[] = "1234567890";

#define VPIN_1    V0  // BV
#define VPIN_2    V1  // BP
#define VPIN_3    V3  // Temp
#define VPIN_4    V4  // Temp_Status
#define VPIN_5    V2  // Flame_Status



BLYNK_CONNECTED()
{ 

  Blynk.syncVirtual(V0);  
  Blynk.syncVirtual(V1);  
  Blynk.syncVirtual(V2);  
  Blynk.syncVirtual(V3);  
  Blynk.syncVirtual(V4);   
  
}
void setup()
{
  // Debug console
  Serial.begin(9600);
  delay(100);
  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);
}

void loop()
{
  Blynk.run();
  if (Serial.available()>0) 
  {
  char a=Serial.read();

if(a=='a')
{  
    float B=Serial.parseFloat(); 
    Blynk.virtualWrite(VPIN_1,B);//BV
}
  
  
 if(a=='b')
{  
    int P=Serial.parseInt(); 
    Blynk.virtualWrite(VPIN_2,P);//BP
}

if(a=='T')
{  
    int V=Serial.parseInt(); 
    Blynk.virtualWrite(VPIN_3,V);//Temp
}


if(a=='S')
{  
    int s=Serial.parseInt(); 
    Blynk.virtualWrite(VPIN_4,s);//temp status
}


if(a=='d')
{  
    int w=Serial.parseInt(); 
    Blynk.virtualWrite(VPIN_5,w);//fire status
}






}  
}