# Domoticz-Marstek
Connecting Marstek Venus 5.12Kwh V2 (home battery) to Domoticz (home automation system) using PUSR-DR134.(fixed LAN, not Wifi)

<b>WARNING</b> : when using this solution with a 1 second reporting time you maybe lose the connection to the Marstek database, no data of useage will be shown in the app. 
It seems that setting te reporting time to 10 seconds you can still see data in the app.
But even if no data is stored you can still use the app to control the battery.

Forget a dedicated plugin, forget Node-Red, forget programming this is an easy to setup solution.

This is not a software solution but a device configuration of the Pusr-DR134 for use with the already avaiable general purpose plugin : <b>MqttMapper by FlyingDomotic</b>

<b>Prerequisites :</b>
  * Home battery Marstek Venus V2 running with modbus port and cable
  * Domoticz installed and running (basic knowledge is enough)
  * Domoticz Mqttmapper plugin installed  (https://github.com/FlyingDomotic/domoticz-mqttmapper-plugin)   
  * Mosquito (or other MQTT Broker) installed and running. Eventualy use a tool like MQTT Explorer to check.
  * PUSR-DR134 : "Lipstick" Size Serial Device Server for RS485 <b>(Light Edge version !)</b> buy for € 15 on the internet. (Firmware Version：V4304)

Toolpath :
  * <b>Hardware toolpath</b> : Marstek Venus V2 -> Modbuscable -> PUSR-DR134 -> LAN -> Computer
  * <b>Software toolpath</b> : (transparent :automatic polling of modbus on Marstek Venus V2) -> Lightedge on PUSR-DR134 -> MQTT Broker (Mosquito) -> MqttMapper -> Domoticz

<b>Result : </b>

<img width="497" height="413" alt="Domoticz-result" src="https://github.com/user-attachments/assets/84ad113f-1b7a-42d5-974f-11a1b812934b" />

<b>Setting up the Marstek Venus V2 modbus connection :</b>
  * Marstek delivers a RS485 cable with the battery.
  * If not , you have to build one yourself but that is not difficult.

<b>Connecting to PUSR-DR134</b>    
<img src="https://github.com/user-attachments/assets/f4eed6a8-ce7b-4c4f-8bcf-92a484edf0b6" width="200">

From the twisted (Marstek RS485) cable use :
  * Yellow to A,
  * Red to B ;
  * the Black cable connect to - (not GND : GND is not used)

From the cables connected together use : 
  * Black for + (5volts)
  * The red cable from this set is not used.
  * <b>Watch out , Your cable can be different , CHECK it with a voltmeter !!</b>

<b>Setting up PUSR-DR134</b>

When your PUSR-DR134 is connected through the modbus-cable to the Marstek battery it is powered and boots up.
If not booting (lights !) the power is not connected the right way.

Connect and configure your LAN setup with the <b>[Setup Software] EthernetTool V1.4.0(Edge computing) </b> available from the PUSR website.
When setup and visible in your LAN : connect to the websetuppage  of the device (http://ip.adres.of.device)

 * On page "Port parameter" set up workmode als : MQTT
 * On page " MQTT Gateway " setup your Mqtt broker connection details, select under Publish Config : Transparent Transmission and create a topic : <b>Marstek</b> (used in this config, or whatever you want, without slashes)
 * On page "EDGE Gateway" select working mode "Light Edge" and set "Merge Collect" and "Periodic Reporting" to "V" set "Reporting interval" to 1 second
 * On page "Ponit" (Point) import file <i>dr134.json</i>

The file 'dr134.json' sets the correct parameters for the registers to (automaticly) poll on the Marstek Venus, you can add and/or change.

After this you should see messages, to the topic Marstek ,from the DR134 in your MQTT Broker like this (Partial, could be more):

````
{
  "params": {
    "dir": "up",
    "id": "device_id_of_DR134",
    "r_data": [
     {
        "name": "batterySOC",
        "value": "82",
        "err": "0"
      },
      {
        "name": "ACpower",
        "value": "-252",
        "err": "0"
      }
    ]
  }
}
````

<b>Installing and setting up Mqttmapper plugin:</b>
  * If not already installed : install the MqttMapper plugin in Domoticz through the hardware panel (use the plugin setup methode).
  * Set up the connection parameters to connect to your MQTT Broker (IP, credentials etc).
  * download the file <i>MqttMapper.json</i> (or copy+paste lines into an existing) and put it in your Domoticz/plugins/MqttMapper directory
  * NOTE : The items in the published Mqtt message are not used by <i>parameter name</i> but by <i>item number</i> !! 
  * restart Domoticz.

After installing : 2 new devices should be found with ID <b>MPWR</b> (Power in Watts in or out) and <b>MSOC</b> (State of Charge). 

These devices can be incorporated as battery devices in the Energy Dashboard of Domoticz (as shown before) or used elsewhere

<b>Other possibilities and use your imagination :</b>
  * Marstek modbus registers are published, you can use these wisely. https://duravolt.nl/wp-content/uploads/Duravolt-Plug-in-Battery-Modbus.pdf
  * Can be used with other modbus devices.

<b>UPDATES</b>
|Date     | Comment |
|---------|---------|
|20250727 | adding total counters, temperature of device and feeding for P1 device to be used as Battery device.|
|         | 4 new devices are created in Domoticz. The P1/battery device has now the capability to show graphs of usage of the battery|

<b>Please let me know your solution based on this setup</b>



