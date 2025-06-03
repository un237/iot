#include<DHT.h>
#include <ESP8266WiFi.h>
String apiKey = "HWQYJKR1L1FMH189";     //paste your write api key from thingspeak
const char *ssid =  "nigga";     // enter your wifi hotspot name
const char *pass =  "Jyothika"; // enter hotspot pass
const char* server = "api.thingspeak.com";
#define DHTPIN D4
DHT dht(DHTPIN,DHT11);
WiFiClient client;

void setup() 
{
Serial.begin(115200);
delay(1000);
dht.begin();
Serial.println("Connecting to ");
Serial.println(ssid);
WiFi.begin(ssid, pass);
while (WiFi.status() != WL_CONNECTED)
{
delay(2000);
Serial.print(".");
}
Serial.println("   ");
Serial.println("WiFi connected");
}
void loop(){
  float h =dht.readHumidity();
  float t =dht.readTemperature();
  if(isnan(h)||isnan(t)){
    Serial.println("Failed to read from DHT sensor!");
    return;
  }
  
if (client.connect(server,80))   
{
String postStr = apiKey;
postStr +="&field1=";
postStr +=String(t);
postStr +="&field2=";
postStr +=String(h);

postStr += "\r\n\r\n";

client.print("POST /update HTTP/1.1\n");
client.print("Host: api.thingspeak.com\n");
client.print("Connection: close\n");
client.print("X-THINGSPEAKAPIKEY: "+apiKey+"\n");
client.print("Content-Type: application/x-www-form-urlencoded\n");
client.print("Content-Length: ");
client.print(postStr.length());
client.print("\n\n");
client.print(postStr);
Serial.print("Temp: ");
Serial.print(t);
Serial.print(" degrees Celcius , Humidity: ");
Serial.print(h);
Serial.println("%. Send to ThingSpeak,");
client.stop();

Serial.println("Waiting...");

delay(1000);
}
}
