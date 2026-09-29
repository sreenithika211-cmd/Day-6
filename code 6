#include "WiFi.h" 

#include <WiFiClient.h>
#include <WebServer.h>

WebServer server(80);

const int led=2;
const char MAIN_page[] PROGMEM = R"=====(
  <!DOCTYPE html>
  <html>
  <body>
  <center>
  <h1>Wi-Fi LED on off demo </h1><br>
  Click to turn <a href="ledon">LED ON</a><br>
  Click to turn <a href="ledoff">LED OFF</a><br>
  </center>
  </body>
  </html>
)=====";

void handleRoot(){
  String s = MAIN_page; //Read HTML contents
  server.send(200,"text/html",s); //send web page
}

void handleledon() {
  digitalWrite(led,LOW);
  server.send(200,"text/html","LED is ON");
}

void handleledoff() {
  digitalWrite(led,HIGH);
  server.send(200,"text/html","LED is OFF");
}

void setup(void) {
  
  pinMode(led,OUTPUT);
  digitalWrite(led, 0);
  Serial.begin(115200);
  WiFi.mode(WIFI_STA);
  WiFi.begin("Wokwi-GUEST","");
  
  Serial.println("");
  while(WiFi.status() != WL_CONNECTED){
    delay(500);
    Serial.print(".");
  }
  
  Serial.println("");
  Serial.print("WiFi Connected\n");
  Serial.print("IP address: ");
  Serial.println(WiFi.localIP());
  server.on("/",handleRoot);
  server.on("/ledon",handleledon);
  server.on("/ledoff",handleledoff);
  handleRoot();
  server.begin();
  Serial.println("HTTP server started");
}

void loop(void) {
  server.handleClient();
  delay(2);
}
