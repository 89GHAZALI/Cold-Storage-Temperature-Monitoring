####**Proposal**

Description: Malaysia is one of the biggest bird nest supplier and swiftlet farming, as well as its neighbouring country, Indonesia. One of the pioneers of Raw Unclean Edible Bird Nest (RUC EBN) exporting is MBN Enterprise. It is considered a primary processing unit for bird nests, which they mainly doing the initial cleaning of bird nest, such as grading, cleaning, drying and undergoes heating treatment before it is packaged and exported. In between the processes, the bird nests must be stored in a chiller room, to maintain the quality of the bird nests as well as to prevent yeast and mould or microbial growth.

All the cold room must follow the GMP/HACCP protocol on food products, which the temperature of the chiller room must be 0-4degC. The chiller room never turned off as the production goes all around the year. Even though it was maintained regularly, sometimes the temperature can be over the limit. On some cases, when production people want to bring in and out of the goods from the chiller room, the temperature might rise to 15-25 degC. If it was for a short time, it can be negotiable, but sometimes the production worker does not close the chiller room properly. There are also cases of customers complaining there are microbial growth on the bird nests. The biggest problem is that, HACCP protocol requires scheduled monitoring of the chiller room temperature, even if it during the non-working time (night, weekend and public holiday). To solve the issue and guarantee that the company follows the procedure, a smart monitoring system is needed to control and feedback the temperature of the chiller room.

Basic overview of how the smart monitoring system work:
1. All time monitoring the temperature of all 4-chiller room.
2. The sensor is connected to the internet, which send the data to the cloud.
3. As long as the users have the software and are connected to the internet, the users can monitor the temperature of the chiller room everywhere, even at home.
4. When the temperature is over the limit for a period of time, the users will get a notification to alarm them so that they can check if anything wrong happened to the chiller room (eg: compressor problem, sensor problem)

Internet of things technology is adopted in every field. Our proposed Smart cold storage and inventory monitoring system uses sensor-based IoT technology to offer remote monitoring and tracking the produce. Our paper proposed methodology is early warning alerts and notifications in critical conditions. It enables end-end visibility and accountability across the entire product value chain.This project continuously monitors the temperature in the cold storage facility with the help of LM35 temperature sensor. The operator sets a predefined threshold temperature value for the storage unit. The current values are displayed on the monitor with the help of Ubuntu software. If the threshold temperature is crossed, an SMS alert is sent to the operator along with the value of the current temperature reading of the storage unit. Also, visual and auditory cues are sent to the people nearby via lighting of an LED and the buzzing sound from the buzzer.

####_Problem Statement_####

Several research and technology challenges need to addressed towards the implementation of IoT applications as well as the potential realization of horizontal IoT platforms. The most important challenges, based on our findings, are listed below.

1) Technological Interoperability: Interoperability is significantly more challenging for the IoT as it is not (only) about connecting people with people, but about a seamless interaction between devices and people with devices. These devices can differ regarding their technological capabilities.

2) Semantic Interoperability: For full interoperability, it is necessary that the devices interpret the shared information correctly and act accordingly, which is covered by the semantic aspect of interoperability usually referred to as Information Model. Hence, improvements have to be made regarding distributed ontologies, semantic web, or semantic device discovery.

3) Smart Things: Ultra low power circuits and devices capable of tolerating harsh environments have to be developed. Moreover, parallel processing in low power multi-processor systems, adaptation, autonomous behavior while guaranteeing trust, privacy and security, as well as battery, energy harvesting and storage technologies are among the core challenges regarding the devices in the IoT.



###_System Architecture_####
=======
System Architecture
![IoT Diagram vpd (1)](https://user-images.githubusercontent.com/95857649/204152137-a34c5a76-a1e9-4dc4-880c-9cb1c1814eea.jpg)










####_Sensor_####
=======

With the aid of a temperature sensor, this project continuously monitors the temperature in a cold storage for every 10 second. The threshold value is 5degreeCelcius. An LED is illuminated and a buzzer sounds to inform persons in the area if the temperature in the cold storage exceeds 5degC. The user is also alerted and informed of the current temperature through an (SMS or mobile app).
The sensor use in this project is LM35 sensor which determnine the temperature before communicating it to the Bolt WiFi module.
The Python programme determines whether the current temperature is below a predetermined threshold (link : https://www.hackster.io/ritwik-deo/temperature-monitoring-system-for-cold-storage-43f679)

List of Hardware component for sensor circuit:
Bread board, IoT Bolt WiFI Module, Jumper wires, LED, LM35 temperature sensor, buzzer, resistor and USB Cable

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



Dashboard-hanafi

##'/home/ghazali/Desktop/IoT Diagram.vpd (1).jpg'
