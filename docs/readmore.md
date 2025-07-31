<b>More about using this setup</b>

<b>Buying the PUSR-DR134 :</b>
  * It seems there are different versions of the DR134 for sale.
  * Some may not have the <b>"Edge computing"</b>  capabilities necessary for this solution.
  * <b>Buy at the PUSER store on Alie , with description "Edge Computing MQTT" </b>
  * This setup uses firmware version 4304

Currently there is no comparable device with wifi. 

If no fixed LAN is available (no router nearby ?) you could use a ethernet powerline adapter.

<b>Setting up the Marstek Venus V2 wit CT003 :</b>
  * Doesn't work with my new KPN Box 12 router. 
  * Very strong Wifi signal is needed, 3 - 4 meters in between with a wall already gives problems.
  * A very nearby (25 cm) old WIFI 4 dedicated router works well in my case.
  * The Venus battery and CT003 create their own subnet.

<b>No RS485 cable ?</b>
  * At the dutch Tweakers forum for setting up the Marstek for use with HA there is more information available about building the cable.
  * thanx to : [superduper1969](https://github.com/Superduper1969)

<b>Known issues</b>
 * The <b>SOC</b> value is not very reliable. When analysing data of SOC and actual usage in Domoticz (!) it seems that when a nearly full or empty shown SOC the battery still goes on for hours ...
 * In my case <b>history</b> in the app got scrambled up and is not shown anymore. I believe this is because when using the Modbus connection there is no data of usage send to the cloud.

<b>Current status (31.07.2025)</b>
  * Venus firmware version : V153
  * CT003 : V117
  * App version : V1.6.45

I run : Anti-reverse current method (NOM)
  * This works well, during stable useage there is less than 10 watts used or returned per hour.
  * For a whole day less than 500 watts up/down.
  * Info retrieved from an external P1 device

