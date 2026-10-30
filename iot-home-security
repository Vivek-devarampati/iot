#include <WiFi.h>
#include <PubSubClient.h>
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";
const char* mqtt_server = "broker.hivemq.com";
int pirPin = 13;
int ledPin = 2;
WiFiClient espClient;
PubSubClient client(espClient);
void setup() {
  Serial.begin(115200);
  pinMode(pirPin, INPUT);
  pinMode(ledPin, OUTPUT);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) { delay(500); }
  client.setServer(mqtt_server, 1883);
}
void loop() {
  if (!client.connected()) { client.connect("ESP32Client"); }
  client.loop();
  if (digitalRead(pirPin) == HIGH) {
    client.publish("home/security", "MOTION_DETECTED");
    delay(5000);
  }
  delay(1000);
}
