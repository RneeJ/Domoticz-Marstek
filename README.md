# Domoticz-Marstek
Connecting Marstek Venus 5.12Kwh V2 (home battery) to Domoticz (home automation system) using PUSR-DR134.

Forget a dedicated plugin, forget Node-Red, forget programming this is an easy to setup solution.

This is not a software solution but a device configuration of the Pusr-DR134 for use with the already avaiable general purpose plugin : <b>MqttMapper by FlyingDomotic</b>

<b>Prerequisites :</b>
  * Home battery Marstek Venus V2 running with modbus port and cable
  * Domoticz installed and running (basic knowledge is enough)
  * Domoticz Mqttmapper plugin installed  (https://github.com/FlyingDomotic/domoticz-mqttmapper-plugin)   
  * Mosquito (or other MQTT Broker) installed and running. Eventualy use a tool like MQTT Explorer to check.
  * PUSR-DR134 : "Lipstick" Size Serial Device Server for RS485 <b>(Light Edge version !)</b> buy for € 15 on the internet.

<b>Hardware toolpath</b> : Marstek Venus V2 -> Modbuscable -> PUSR-DR134 -> LAN -> Computer
<b>Software toolpath</b> : (transparent :automatic polling of modbus on Marstek Venus V2) -> Lightedge on PUSR-DR134 -> MQTT Broker (Mosquito) -> MqttMapper -> Domoticz

Result : 
<img width="497" height="413" alt="Domoticz-result" src="https://github.com/user-attachments/assets/84ad113f-1b7a-42d5-974f-11a1b812934b" />

<b>Setting up the Marstek Venus V2 modbus connection :</b>
  * Marstek delivers a RS485 cable with the battery.
  * If not , you have to build one yourself but that is not difficult.

<b>Connecting to PUSR-DR134</b>    
<img src="https://github.com/user-attachments/assets/f4eed6a8-ce7b-4c4f-8bcf-92a484edf0b6" width="200">

From the twisted cables use :
  * Yellow to A,
  * Red to B ;
  * the Black cable connect to - (not GND)

From the cables connected together use the Black for + (5volts)
The red cable from this 3-set is not used.
<b>Watch out , Your cable can be different , CHECK it with a voltmeter !!</b>

<b>Installing and settingup Mqttmapper plugin:</b>
  * Install the MqttMapper plugin through the hardware panel.
  * Set up the connection parameters to connect to your MQTT Broker.    

<b>Setting up PUSR-DR134</b>

When your PUSR-DR134 is connected through the modbus-cable to the Marstek battery it is powered and boots up.

Connect and configure your LAN setup with the <b>[Setup Software] EthernetTool V1.4.0(Edge computing) </b> avaiable from the PUSR website.
When setup connect to the websetuppage  of the device (http://ip.adres.of.device)

 * On page "Portparameter" set up workmode als : MQTT
 * On page " MQTT Gateway " setup your Mqtt broker connection details, select under Publish Config : Transparent Transmission and create a topic : Marstek (or whatever but without slashes)
 * On page "EDGE Gateway" select working mode "Light Edge" and set "Merge Collect" and "Periodic Reporting" to "V" set "Reporting interval" to 1 second
 * On page "Ponit" (Point) import file 'drv134.json'

The file 'drv.json' set
