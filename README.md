#include &lt;ESP8266WiFi.h&gt;
#include &lt;WiFiClient.h&gt;
#include &lt;ThingSpeak.h&gt;
const char* ssid = "Wifi Adı ";
const char* password = " Wifi Şifresi Yazılıyor ";
int val;
int tempPin = A0;

WiFiClient client;
unsigned long myChannelNumber = 345148;
const char * myWriteAPIKey = "Thingspeak API Kodu Yazılıyor ";
void setup() {
Serial.begin(115200);
delay(10);

WiFi.begin(ssid, password);
// Connect to WiFi network
ThingSpeak.begin(client);
}

void loop() {
val = analogRead(tempPin);
float mv = ( val/1024.0)*5000;
float cel = mv/10;
Serial.print("TEMPRATURE = ");
Serial.print(cel);
Serial.print("*C");
Serial.println();
delay(1000);
ThingSpeak.writeField(myChannelNumber, 1,cel, myWriteAPIKey);

delay(100); }
