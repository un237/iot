#include "ESP8266WiFi.h"
#include "DHT.h"
#define DHTTYPE DHT22
const char* ssid = "Bhavani";
const char* password = "Bhavani1234@";
WiFiServer wifiServer(9000);
DHT dht(D4, DHT22);

void setup() {
Serial.begin(115200);
delay(1000);
WiFi.begin(ssid, password);
while (WiFi.status() != WL_CONNECTED) {
delay(1000);
Serial.println("Connecting..");
}
Serial.print("Connected to WiFi. IP:");
Serial.println(WiFi.localIP());
wifiServer.begin();
dht.begin();

}

void loop() {
WiFiClient client = wifiServer.available();
if (client) {
while (client.connected()) {
while (client.available()>0) {
float t = dht.readTemperature();
float h = dht.readHumidity();
client.println("humidity :");
client.println("temperature :");
client.println(h);
Serial.println(h);
client.println(t);
Serial.println(t);
delay(2000);
}
}
client.stop();
Serial.println("Client disconnected");
}
}
