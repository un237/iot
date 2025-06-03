#include <DHT.h>
#include<ESP8266WiFi.h>
String apiKey = "Read API Key";
const char *ssid = "Kunal";
const char *pass = "12345678";
const char* server = "api.thingspeak.com";
#define DHTPIN D4
DHT dht(DHTPIN,DHT11);
WiFiClient client;
void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
  delay(1000);
  dht.begin();
  Serial.println("Connecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid,pass);
  while(WiFi.status() != WL_CONNECTED){
    delay(500);
    Serial.print(".");
  }
  Serial.println("");
  Serial.println("WiFi connected");
}

void loop() {
  // put your main code here, to run repeatedly:
  float h = dht.readHumidity();
  float t = dht.readTemperature();
  if(isnan(h) || isnan(t)){
    Serial.println("Failed to read from DHT sensor!");
    return;
  }
  if (client.connect(server,80))
{                      
  String postStr = apiKey;
  postStr +="&field1=";
  postStr += String(h);
  postStr +="&field2=";
  postStr += String(t);
  postStr += "\r\n\r\n";
  client.print("X-THINGSPEAKAPIKEY: "+apiKey+"\n");
  client.print("Content-Length: ");
  client.print(postStr.length());
  client.print("\n\n");
  client.print(postStr);
  Serial.print("Temperature: ");
  Serial.print(t);
  Serial.print(" degrees Celcius, Humidity: ");
  Serial.print(h);
  Serial.println("%. Send to Thingspeak.");
}
  client.stop();
  Serial.println("Waiting...");
  delay(1000);
}
