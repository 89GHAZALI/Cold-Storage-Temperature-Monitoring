## Proposal
## COLD STORAGE TEMPERATURE MONITORING


Description: Malaysia is one of the biggest bird nest supplier and swiftlet farming, as well as its neighbouring country, Indonesia. One of the pioneers of Raw Unclean Edible Bird Nest (RUC EBN) exporting is MBN Enterprise. It is considered a primary processing unit for bird nests, which they mainly doing the initial cleaning of bird nest, such as grading, cleaning, drying and undergoes heating treatment before it is packaged and exported. In between the processes, the bird nests must be stored in a chiller room, to maintain the quality of the bird nests as well as to prevent yeast and mould or microbial growth.

All the cold room must follow the GMP/HACCP protocol on food products, which the temperature of the chiller room must be 0-4degC. The chiller room never turned off as the production goes all around the year. Even though it was maintained regularly, sometimes the temperature can be over the limit. On some cases, when production people want to bring in and out of the goods from the chiller room, the temperature might rise to 15-25 degC. If it was for a short time, it can be negotiable, but sometimes the production worker does not close the chiller room properly. There are also cases of customers complaining there are microbial growth on the bird nests. The biggest problem is that, HACCP protocol requires scheduled monitoring of the chiller room temperature, even if it during the non-working time (night, weekend and public holiday). To solve the issue and guarantee that the company follows the procedure, a smart monitoring system is needed to control and feedback the temperature of the chiller room.

Basic overview of how the smart monitoring system work:
1. All time monitoring the temperature of all 4-chiller room.
2. The sensor is connected to the internet, which send the data to the cloud.
3. As long as the users have the software and are connected to the internet, the users can monitor the temperature of the chiller room everywhere, even at home.
4. When the temperature is over the limit for a period of time, the users will get a notification to alarm them so that they can check if anything wrong happened to the chiller room (eg: compressor problem, sensor problem)

Internet of things technology is adopted in every field. Our proposed Smart cold storage and inventory monitoring system uses sensor-based IoT technology to offer remote monitoring and tracking the produce. Our paper proposed methodology is early warning alerts and notifications in critical conditions. It enables end-end visibility and accountability across the entire product value chain.This project continuously monitors the temperature in the cold storage facility with the help of LM35 temperature sensor. The operator sets a predefined threshold temperature value for the storage unit. The current values are displayed on the monitor with the help of Ubuntu software. If the threshold temperature is crossed, an SMS alert is sent to the operator along with the value of the current temperature reading of the storage unit. Also, visual and auditory cues are sent to the people nearby via lighting of an LED and the buzzing sound from the buzzer.

## Problem Statement


Several research and technology challenges need to addressed towards the implementation of IoT applications as well as the potential realization of horizontal IoT platforms. The most important challenges, based on our findings, are listed below.

1) Technological Interoperability: Interoperability is significantly more challenging for the IoT as it is not (only) about connecting people with people, but about a seamless interaction between devices and people with devices. These devices can differ regarding their technological capabilities.

2) Semantic Interoperability: For full interoperability, it is necessary that the devices interpret the shared information correctly and act accordingly, which is covered by the semantic aspect of interoperability usually referred to as Information Model. Hence, improvements have to be made regarding distributed ontologies, semantic web, or semantic device discovery.

3) Smart Things: Ultra low power circuits and devices capable of tolerating harsh environments have to be developed. Moreover, parallel processing in low power multi-processor systems, adaptation, autonomous behavior while guaranteeing trust, privacy and security, as well as battery, energy harvesting and storage technologies are among the core challenges regarding the devices in the IoT.



## System Architecture

System Architecture
![IoT Diagram vpd (1)](https://user-images.githubusercontent.com/95857649/204152137-a34c5a76-a1e9-4dc4-880c-9cb1c1814eea.jpg)










## Sensor

With the aid of a temperature sensor, this project continuously monitors the temperature in a cold storage for every 10 second. The threshold value is 5degreeCelcius. An LED is illuminated and a buzzer sounds to inform persons in the area if the temperature in the cold storage exceeds 5degC. The user is also alerted and informed of the current temperature through an (SMS or mobile app).
The sensor use in this project is DHT11 sensor which determine the temperature before communicating it to the ESP8266 Wifi with microcontroller module. 

List of Hardware component for sensor circuit:
WIFI ESP8266 With arduino, Jumper wires, LED, DHT11, 10k ohm resistor

updated : coding arduino 
https://randomnerdtutorials.com/complete-guide-for-dht11dht22-humidity-and-temperature-sensor-with-arduino/
https://randomnerdtutorials.com/esp8266-dht11dht22-temperature-and-humidity-web-server-with-arduino-ide/

Python coding for temperature sensor (link for web: https://randomnerdtutorials.com/esp32-esp8266-dht11-dht22-micropython-temperature-humidity-sensor/)
another link: https://www.instructables.com/Interface-DHT11-Using-Arduino/

SENSOR CODING (26/1/2023)

// Import required libraries
#include <Arduino.h>
#include <ESP8266WiFi.h>
#include <Hash.h>
#include <ESPAsyncTCP.h>
#include <ESPAsyncWebServer.h>
#include <Adafruit_Sensor.h>
#include <DHT.h>

// Replace with your network credentials
const char* ssid = "REPLACE_WITH_YOUR_SSID";
const char* password = "REPLACE_WITH_YOUR_PASSWORD";

#define DHTPIN 5     // Digital pin connected to the DHT sensor

// Uncomment the type of sensor in use:
#define DHTTYPE    DHT11     // DHT 11
//#define DHTTYPE    DHT22     // DHT 22 (AM2302)
//#define DHTTYPE    DHT21     // DHT 21 (AM2301)

DHT dht(DHTPIN, DHTTYPE);

// Create AsyncWebServer object on port 80
AsyncWebServer server(80);

// current temperature & humidity, updated in loop()
float t = 0.0;
float h = 0.0;

// Generally, you should use "unsigned long" for variables that hold time
// The value will quickly become too large for an int to store
unsigned long previousMillis = 0;    // will store last time DHT was updated

// Updates DHT readings every 10 seconds
const long interval = 10000;  

const char index_html[] PROGMEM = R"rawliteral(
<!DOCTYPE HTML><html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.7.2/css/all.css" integrity="sha384-fnmOCqbTlWIlj8LyTjo7mOUStjsKC4pOpQbqyi7RrhN7udi9RwhKkMHpvLbHG9Sr" crossorigin="anonymous">
  <style>
    html {
     font-family: Arial;
     display: inline-block;
     margin: 0px auto;
     text-align: center;
    }
    h2 { font-size: 3.0rem; }
    p { font-size: 3.0rem; }
    .units { font-size: 1.2rem; }
    .dht-labels{
      font-size: 1.5rem;
      vertical-align:middle;
      padding-bottom: 15px;
    }
  </style>
</head>
<body>
  <h2>ESP8266 DHT Server</h2>
  <p>
    <i class="fa-solid fa-temperature-half">" style="color:#059e8a;"></i> 
    <span class="dht-labels">Temperature</span> 
    <span id="temperature">%TEMPERATURE%</span>
    <sup class="units">&deg;C</sup>
  </p>
  <p>
    <i class="fa-solid fa-temperature-half" style="color:#00add6;"></i> 
    <span class="dht-labels">Humidity</span>
    <span id="humidity">%HUMIDITY%</span>
    <sup class="units">%</sup>
  </p>
</body>
<script>
setInterval(function ( ) {
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("temperature").innerHTML = this.responseText;
    }
  };
  xhttp.open("GET", "/temperature", true);
  xhttp.send();
}, 10000 ) ;

setInterval(function ( ) {
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("humidity").innerHTML = this.responseText;
    }
  };
  xhttp.open("GET", "/humidity", true);
  xhttp.send();
}, 10000 ) ;

</script>
</html>)rawliteral";

// Replaces placeholder with DHT values
String processor(const String& var){
  //Serial.println(var);
  if(var == "TEMPERATURE"){
    return String(t);
  }
  else if(var == "HUMIDITY"){
    return String(h);
  }
  return String();
}

void setup(){
  // Serial port for debugging purposes
  Serial.begin(115200);
  dht.begin();
  
  // Connect to Wi-Fi
  WiFi.begin(ssid, password);
  Serial.println("Connecting to WiFi");
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println(".");
  }

  // Print ESP8266 Local IP Address
  Serial.println(WiFi.localIP());

  // Route for root / web page
  server.on("/", HTTP_GET, [](AsyncWebServerRequest *request){
    request->send_P(200, "text/html", index_html, processor);
  });
  server.on("/temperature", HTTP_GET, [](AsyncWebServerRequest *request){
    request->send_P(200, "text/plain", String(t).c_str());
  });
  server.on("/humidity", HTTP_GET, [](AsyncWebServerRequest *request){
    request->send_P(200, "text/plain", String(h).c_str());
  });

  // Start server
  server.begin();
}
 
void loop(){  
  unsigned long currentMillis = millis();
  if (currentMillis - previousMillis >= interval) {
    // save the last time you updated the DHT values
    previousMillis = currentMillis;
    // Read temperature as Celsius (the default)
    float newT = dht.readTemperature();
    // Read temperature as Fahrenheit (isFahrenheit = true)
    //float newT = dht.readTemperature(true);
    // if temperature read failed, don't change t value
    if (isnan(newT)) {
      Serial.println("Failed to read from DHT sensor!");
    }
    else {
      t = newT;
      Serial.println(t);
    }
    // Read Humidity
    float newH = dht.readHumidity();
    // if humidity read failed, don't change h value 
    if (isnan(newH)) {
      Serial.println("Failed to read from DHT sensor!");
    }
    else {
      h = newH;
      Serial.println(h);
    }
  }
}

//There is a dht module that comes with the MicroPython firmware by default. So, it is easy to get temperature and humidity.

1. Importing the dht and machine modules
import dht
from machine import Pin

2. Create a dht object that refers to the sensor’s data pin, in this case it’s GPIO 14:

sensor = dht.DHT11(Pin(14))
#sensor = dht.DHT22(Pin(14))

3. Measure and read the sensor values

sensor.measure() 
sensor.temperature()
sensor.humidity()

## Cloud Platform

Deployment is a critical stage in web development. It is at this point that the application is tested in an environment where the user will be using it. Any sensitive information should be packaged in a manner that does not compromise the app.
This is just a draft for the final project, we decided to present this project as a web application (project from stage 1), particularly with the [Django framework](https://www.djangoproject.com/). And the data is private and secure as it is hosted in [pythonanywhere](https://www.pythonanywhere.com/).
#### The web-application can be accessed from [here](http://chadli.pythonanywhere.com/)
#### Screenshots
##### Homepage

![homepage capture](https://user-images.githubusercontent.com/110521665/204136430-8809cef7-0729-4058-84f4-1db16c79f93b.JPG)

## LINK: [Demo for the setup of cloud platform](https://drive.google.com/file/d/1gA54EYpU97CedSw01ERy1OGtU6efNLnq/view?usp=sharing)

## Built With

* Django2.2.4
* Python3.8
* Html
* Css



## Dashboard

An Internet of Things (IoT) dashboard is the user interface that is contained within an Internet of Things (IoT) platform. It gives users the ability to monitor and interact with connected devices through the use of graphs, charts, and other tools and UI components. Dashboards provide the user with the ability to handle every aspect of their connected devices and gain perspective on their surroundings through the visualisation of their device data.

Microsoft Visual Studio are used in this project to design the dashboard of the system.

![Design](https://user-images.githubusercontent.com/117091911/204157865-47dea09c-5281-4cac-8377-3d9a991f8391.JPG)

