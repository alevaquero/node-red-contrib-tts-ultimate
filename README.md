
![Sample Node](img/logo.png) 

[![NPM version][npm-version-image]][npm-url]
[![NPM downloads per month][npm-downloads-month-image]][npm-url]
[![NPM downloads total][npm-downloads-total-image]][npm-url]
[![MIT License][license-image]][license-url]
[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)
[![Donate via PayPal](https://img.shields.io/badge/Donate-PayPal-blue.svg?style=flat-square)](https://www.paypal.me/techtoday) 
[![Facebook][facebook-image]][facebook-url]

<img src='https://raw.githubusercontent.com/Supergiovane/node-red-contrib-tts-ultimate/master/img/main.png' width="80%">

<details><summary> VIEW SAMPLE CODE </summary>

> Adjust the nodes according to your setup

```js
[{"id":"569773ae.930abc","type":"inject","z":"344c547c.b230c4","name":"","topic":"","payload":"true","payloadType":"bool","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":230,"y":300,"wires":[["e066ce90.46f758"]]},{"id":"e066ce90.46f758","type":"function","z":"344c547c.b230c4","name":"Via function","func":"// The simplest way\nmsg.payload=\"Benvenuti,Wilkommen,Wellcome!\";\nreturn msg;\n","outputs":1,"noerr":0,"x":370,"y":300,"wires":[["3d9635bc.53c14a"]]},{"id":"c272b47c.41e238","type":"inject","z":"344c547c.b230c4","name":"","topic":"","payload":"true","payloadType":"bool","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":230,"y":340,"wires":[["2fcffdb7.1c76ea"]]},{"id":"2fcffdb7.1c76ea","type":"function","z":"344c547c.b230c4","name":"Set volume","func":"// Set the Volume\nmsg.volume=\"60\"; // If not set, will take the volume from setting page\nmsg.payload=\"Benvenuti,Wilkommen,Wellcome!\";\nreturn msg;\n\n","outputs":1,"noerr":0,"x":370,"y":340,"wires":[["3d9635bc.53c14a"]]},{"id":"2bd6fd7f.9b9ae2","type":"inject","z":"344c547c.b230c4","name":"","topic":"","payload":"true","payloadType":"bool","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":230,"y":380,"wires":[["aa3b6e42.669fc"]]},{"id":"aa3b6e42.669fc","type":"function","z":"344c547c.b230c4","name":"Array of messages","func":"// Create an array of messages\nvar aMessages=[];\n// Add random messages\naMessages.push({volume:\"50\",payload:\"Benvenuti.\"});\n// Wheater in Italy\naMessages.push({volume:\"40\",payload:\"http://media.ilmeteo.it/audio/2020-12-23.mp3\"});\n// Add random messages\naMessages.push({volume:\"30\",payload:\"Cambia la tua voce nei settaggi.\"});\nreturn [aMessages];\n","outputs":1,"noerr":0,"x":390,"y":380,"wires":[["3d9635bc.53c14a"]]},{"id":"3e0d9b5c.fe01b4","type":"inject","z":"344c547c.b230c4","name":"Hello World","topic":"","payload":"Ciao Mondo! Come stai?","payloadType":"str","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":250,"y":260,"wires":[["3d9635bc.53c14a"]]},{"id":"42e6fab4.e8d154","type":"comment","z":"344c547c.b230c4","name":"Play text on Sonos. Single player or Group of players","info":"","x":360,"y":220,"wires":[]},{"id":"3d9635bc.53c14a","type":"ttsultimate","z":"344c547c.b230c4","name":"","voice":"Brian","ssml":false,"sonosipaddress":"192.168.1.109","sonosvolume":"30","sonoshailing":"Hailing_Hailing.mp3","config":"557d8082.eb5a8","property":"payload","propertyType":{},"rules":[],"x":610,"y":260,"wires":[[]]},{"id":"557d8082.eb5a8","type":"ttsultimate-config","z":"","name":"googletranslate","noderedipaddress":"192.168.1.219","noderedport":"1980","purgediratrestart":"leave","ttsservice":"googletranslate"}]
```
</details>


## DESCRIPTION
This node transforms a text into a speech audio. You can hear the voice through Sonos.<br/>
Uses Amazon Polly and Google TTS voices (even without credentials nor registration), and you can use it with **your own audio file** as well and it can be used **totally offline** even without the use of TTS, without internet connection.<br/>
This is a major ***upgrade from the previously popular node SonosPollyTTS*** (SonosPollyTTS is not developed anymore).<br/>
**Node v.10.0.0 or newer is needed**.

[![Donate via PayPal](https://img.shields.io/badge/Donate-PayPal-blue.svg?style=flat-square)](https://www.paypal.me/techtoday)

## CHANGELOG
* See <a href="https://github.com/Supergiovane/node-red-contrib-tts-ultimate/blob/master/CHANGELOG.md">here the changelog</a>

## FEATURES
* **Amazon Voices, Gooogle Translate Voices and Google TTS Voices** are all supported, with all avaiables languages and genders.
* **Automatic grouping** is supported. You can group all players you want to play your announcements.
* **Automatic discovery** of your players.
* **Automatic resume of music** queue (including radio stations, but here, some users reports problem resuming ***radio stations*** and, because of lack of Sonos API documentation, the issue cannot currently be fixed), at exact track, at exact time.
* **TTS caching**. Amazon AWS and Google charges you if you use they tts service for a high rate of text to speech requests. TTS-Ultimate caches the TTS files. It downloads the TTS audio from Amazon or Google only once. The second time, the node will read it from the cache. The caches is resilient, that means it survives reboots and updates.
* **UPLOAD your own audio files**. You can upload your own audio files with OwnFile node.
* **Can work offline**. You can use your own audio files (with OwnFile node) to make the node works offline.
* Send a simple payload with the text you want to speech out. For example <code>node.send({payload:"Hello there!"});</code>.

>
> ***UPDATE PATH FROM SONOSPOLLYTTS TO TTS-ULTIMATE***
>
> Supergiovane takes care about your brain and your time.<br/>
> Install TTS-Ultimate. Both SonosPollyTTS and TTS-Ultimate can cohexist.<br/>
> Then just delete your old SonosPollyTTS nodes and replace it with TTS-Ultimate nodes.<br/>
> The cache will remain the same. Your own audio files and hailing files won't be touched. You'll find it again in TTS-Ultimate<br/>
> 

<br/>

>
> ***NOTE IF YOU CANNOT UPLOAD YOUR OWN FILES***
>
> If you're running node-red as "plugin" for homeassistant, redmatic etc...<br/>
> You may expect not to be able to upload your own files. Please check that the user running node-red, has premission **to write to the filesystem**.<br/>
> 

<br/><br/>

# TTS Service node
Here you can set all parameters you need. All nodes will refer to this config node, so you need to set it only once.<br/> 
IF YOU RUN NODE-RED BEHIND DOCKER OR SOMETHING ELSE, BE AWARE: <br/>
PORT USED BY THE NODE ARE 1980 (DEFAULT) AND 1400 (FOR SONOS DISCOVER). <br/>
PLEASE ALLOW MDNS AND UDP AS WELL

**TTS Service**<br/>
You can choose between Google (without credentials), Amazon AWS (Polly) or Google TTS (require credentials and registration to google) engines.<br/>
For Google TTS Engine, you can choose pitch and speed rate of the voice.
<br/>
<br/>

* **TTS Service using Google (without credentials)**<br/>
   This is the simplest way. Just select the voice and you're done. You don't need any credential and you don't even need to be registered to any google service. The voice list is more limited than other services, but it works without hassles.
   
<br/>

* **TTS Service using Amazon AWS (Polly)**<br/>
    > HOW-TO in Deutsch: for german users, there is a very helpful how-to, where you can learn how to use the node and how to register to Amazon AWS Polly as well: here: https://technikkram.net/blog/2020/09/26/sonos-sprachausgabe-mit-raspberry-pi-node-red-und-amazon-polly-fuer-homematic-oder-knx-systeme
   
   **AWS Access key**<br/>
   AWS access key credential
   <br/><br/>
   **AWS Secret key**<br/>
   AWS access Secret key. 
<br/>

* **TTS Service using Google TTS**<br/>
   For Google TTS Engine, you can choose pitch and speed rate of the voice.<br/>
   **Google credentials file path**<br/>
   Here you must select your credential file, previously downloaded from Google, [with these steps](https://www.npmjs.com/package/@google-cloud/text-to-speech):
   > [Select or create a Cloud Platform project](https://console.cloud.google.com/project)<br/>
   > [Enable billing for your project](https://support.google.com/cloud/answer/6293499#enable-billing)<br/>
   > [Enable the Google Cloud Text-to-Speech API](https://console.cloud.google.com/flows/enableapi?apiid=texttospeech.googleapis.com)<br/>
   

<br/>

**Node-Red IP**<br/>
set IP of your node-red machine. Sonos will connect to this address in order to play TTS. You can also write any value you want, for example 127.0.0.1 in this field (**don't leave this field blank in any case**), if you don't want to use Sonos as player. Please see below, the section **TTS-ULTIMATE NODE**, property **Player**.

**Host Port**<br/>
Sonos will connect to this port in order to play TTS. Default 1980. Choose a free port. Do not use 1880 or any other port already in use on your computer.

**TTS Cache**
<br/>
***Purge and delete the TTS cache folder at deploy or restart***<br/>
On each deploy or node-red restart, delete all tts files in the cache. This is useful not to run out of disk space, in case you've a lot of TTS speech files.
<br/>
***Leave the TTS cache folder untouched*** (suggested only if you have enough disk space)<br/>
Don't delete the files cached. Useful if you wish to keep the tts files, even in case of internet outages, node-red restart or reboots.
<br/> 
<br/>

# TTS-ULTIMATE NODE

**TTS Service**<br/>
Select the TTS SERVICE ENGINE NODE, as stated above.

**Voice**<br/>
Select your preferred voice. If you use Amazon, Polly voices will be displayed. If you use Google, google voices will be displayed. Google service without authentication, has a limited set of voices.

**Rate**<br/>
Only avaiable if you choose Google TTS Engine (with credentials). Specifies the speech speed (Between 0.25 and 4.0, default 1).

**Pitch**<br/>
Only avaiable if you choose Google TTS Engine (with credentials). Specifies the speech pitch (Between -20.0 and 20.0,  default 0).

**Hailing**<br/>
Before the first TTS message of the message queues, Sonos will play an "hailing" sound. You can select the hailing or totally disable it.

**Player**<br/>
Select the player. If you select not to use a player, the node will output a msg with an array of files, ready to be played by third party nodes.<br/>
In case you select ***No player, only output file name***, you'll get a message with an additional property *filesArray*, containing an array of all mp3 files ready to be played with third party nodes. Please see below the **OUTPUT MESSAGES FROM THE NODE** section.

**Volume** <br/>
Set the preferred TTS volume, from "0" to "100" (can be overridden by passing <code>msg.volume = "40";</code> to the node)

**Main Sonos Player** <br/>
Select your Sonos primary player. (It's strongly suggested to set a fixed IP for this player; you can reserve an IP using the DHCP Reservation function of your router/firewall's DHCP Server).<br/>
It's possibile to group players, so your announcement can be played on all selected players. For this to happen, you need to select your primary coordinator player. All other players will be then controlled by this coordinator.

**Additional Players** <br/>
Here you can add all additional players that will be grouped toghether to the *Main Sonos Player* coordinator group. You can add a player using the "ADD" button, below the list.


## INPUT MESSAGES TO THE NODE <br/>

**msg.volume**<br/>
Set the volume (values between "0" and "100" with quotes)</br>

**msg.nohailing**<br/>
Temporarely doesn't play the Hailing sound prior to the message (values "true" or "1" with quotes)</br>

**msg.payload** <br/>
The text to be spoken (for example msg.payload = "Hello World!";). You can also play an mp3 stored on an http server, by passing the URL to the payload ( <code>msg.payload = "http://www.myserver.com/alarm.mp3"</code>)</br>

**msg.sonoshailing**<br/>
Overrides the selected hailing and plays the filename you passed in. Please double check the spelling of the filename (must be the same as you can see in the dropdown list of your hailing files, in the ttsultimate config window) and do not include the <b>.mp3</b> extenson. For example *node.sonoshailing="ComputerCall"*<br/>

**msg.priority**<br/>
If set to <b>true</b>, the inbound flow message will cancel the current TTS queue, will stop the current phrase being spoken and the node will play this priority message.<br/>
If there are other priority messages in the queue, they will be retained and the inbound priority flow message is added to the queue.<br/>
If the inbound priority flow message is the first in the priority queue, the hailing is played first (if the hailing has been enabled or if the hailing has been overridden by *node.sonoshailing*)<br/>

**msg.stop**<br/>
If set to <b>true</b>, stops whatever is playing and clears the TTS queue.<br/>

*Examples*

```js
// Play a message
msg.payload = "Hello, the current temperature is 12°";
return msg;
```

```js
// Play a message, forcing no hailing
msg.nohailing = true;
msg.payload = "I won't disturb with my hailing, this time.";
return msg;
```

```js
// Play custom hailing and custom mp3 taken from anywhere
msg.sonoshailing = "IntruderAlert";
msg.payload = "http://192.125.22.44/intruderalarm.mp3";
return msg;
```

```js
// Play priority message
msg.priority = true;
msg.payload = "Warning. Intruder in the dinning room.";
return msg;
```

```js
// Stop whatever is playing
msg.stop = true;
return msg;
```

## OUTPUT MESSAGES FROM THE NODE

The node has two output pins. The first pin is to signal play status, the second one, is to signal an error.

**OUTPUT PIN 1**<br/>
Payload is ***true*** when the node has finished playing, ***false*** if the node is playing<br/>
In case you selected ***No player, only output file name.*** in the **Player** property, you'll get a message with an additional property *filesArray*, containing an array of all mp3 files ready to be played with third party nodes.<br/>
```js
{
   "payload":true,
   "filesArray":[
      {
         "file":"/Users/supergiovane/.node-red/sonospollyttsstorage/hailingpermanentfiles/Hailing_ComputerCall.mp3"
      },
      {
         "file":"/Users/supergiovane/.node-red/sonospollyttsstorage/ttsfiles/ille mi par esse deo videtur_pause_ ille si fas est superare divos_stop__it-IT.mp3"
      },
      {
         "file":"/Users/supergiovane/.node-red/sonospollyttsstorage/ttsfiles/Banana rama_it-IT.mp3"
      }
   ],
   "_msgid":"8b6b22a45dfd5236"
}
```

**OUTPUT PIN 2**<br/>
Payload is ***true*** when error occurs (for example, lost connection with Sonos Player), otherwise ***false***.<br/>

In this sample, you see the TTS-Ultimate node connected with two debug nodes, to catch the errors.

<img src='https://github.com/Supergiovane/node-red-contrib-tts-ultimate/raw/master/img/error.png' width="80%">

<br/>
<br/>

## CHANGE CONFIGURATION VIA MSG PROPERTY

You can change the configuration of tts-ultimate, *via msg.setConfig* property.<br/>
The property is a JSON object. 

<img src='https://github.com/Supergiovane/node-red-contrib-tts-ultimate/raw/master/img/setConfig.png' width="80%">

**msg.setConfig**<br/>
This is the property where you can set all the things. It must be an Object.

**setMainPlayerIP**<br/>
Sets the main player IP. This will also be the coordinator if you have a group of players

**setPlayerGroupArray**<br/>
Sets the array of players beloging to the group, if any.<br/>
If you have only one additional player, you need to ever put it into an array. See below.

```js
// Set player IP
var config= {
    setMainPlayerIP:"192.168.1.109"
};
msg.setConfig = config;
return msg;
```

```js
// Set player IP and additional players
var config= {
    setMainPlayerIP:"192.168.1.109",
    setPlayerGroupArray:[
        "192.168.1.110",
        "192.168.1.111",
        "192.168.1.112"
    ]
};
msg.setConfig = config;
return msg;
```

```js
// If you have only one additional player
var config= {
    setMainPlayerIP:"192.168.1.109",
    setPlayerGroupArray:["192.168.1.110"]
};
msg.setConfig = config;
return msg;
```

<br/>

<details><summary> VIEW SAMPLE CODE</summary>

> Adjust the nodes according to your setup

```js
[{"id":"4b4514d.047366c","type":"ttsultimate","z":"235d8e3d.a7583a","name":"","voice":"de-DE","ssml":false,"sonosipaddress":"192.168.1.109","sonosvolume":"5","sonoshailing":"0","config":"feee307e.54bca","property":"payload","propertyType":{},"rules":[],"x":430,"y":360,"wires":[["2b2d7556.251d0a"],["2978fe86.e680aa"]]},{"id":"2b2d7556.251d0a","type":"debug","z":"235d8e3d.a7583a","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","targetType":"full","statusVal":"","statusType":"auto","x":610,"y":340,"wires":[]},{"id":"2978fe86.e680aa","type":"debug","z":"235d8e3d.a7583a","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","targetType":"full","statusVal":"","statusType":"auto","x":610,"y":380,"wires":[]},{"id":"9d9e06be.09718","type":"function","z":"235d8e3d.a7583a","name":"Change Config","func":"// Set the main player IP and each IP belonging to the player's group\nvar config= {\n    setMainPlayerIP:\"192.168.1.109\",\n    setPlayerGroupArray:[\n        \"192.168.1.110\",\n        \"192.168.1.111\",\n        \"192.168.1.112\"\n    ]\n};\nmsg.setConfig = config;\nreturn msg;","outputs":1,"noerr":0,"initialize":"","finalize":"","x":260,"y":360,"wires":[["4b4514d.047366c"]]},{"id":"c3da8b3a.e8f2c8","type":"inject","z":"235d8e3d.a7583a","name":"","props":[{"p":"payload"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"Hello","payloadType":"str","x":110,"y":360,"wires":[["9d9e06be.09718"]]},{"id":"c55b7140.4a7cc8","type":"comment","z":"235d8e3d.a7583a","name":"Change the player and/or group of players via msg property.","info":"","x":270,"y":300,"wires":[]},{"id":"feee307e.54bca","type":"ttsultimate-config","name":"Config","noderedipaddress":"192.168.1.161","noderedport":"1980","purgediratrestart":"leave","ttsservice":"googletranslate"}]
```
</details>

<br/>
<br/>

# OWNFILE NODE CONFIGURATION

<img src='https://github.com/Supergiovane/node-red-contrib-tts-ultimate/raw/master/img/of.png' width="80%">

<br/>

<details><summary> VIEW SAMPLE CODE</summary>

> Adjust the nodes according to your setup

```js
[{"id":"db0ea33.f1186e","type":"ttsultimate","z":"c6efd2b6.ab02e8","name":"","voice":"en-AU-Standard-A#en-AU#FEMALE","ssml":false,"sonosipaddress":"192.168.1.109","sonosvolume":"25","sonoshailing":"Hailing_Hailing.mp3","config":"4f941d61.f52c4c","propertyType":{},"rules":[],"x":670,"y":240,"wires":[[]]},{"id":"c7fb2970.271978","type":"ownfile","z":"c6efd2b6.ab02e8","name":"","selectedFile":"OwnFile_Tur geoeffnet.mp3","x":490,"y":220,"wires":[["db0ea33.f1186e"]]},{"id":"fef80c5b.49f9e","type":"inject","z":"c6efd2b6.ab02e8","name":"","topic":"","payload":"true","payloadType":"bool","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":130,"y":220,"wires":[["c7fb2970.271978"]]},{"id":"807f0f6c.6d59c","type":"comment","z":"c6efd2b6.ab02e8","name":"You can upload your own voice messages and use it with ttsultimate","info":"","x":310,"y":180,"wires":[]},{"id":"536e58b3.bb8468","type":"ownfile","z":"c6efd2b6.ab02e8","name":"","selectedFile":"OwnFile_Tur geoeffnet.mp3","x":490,"y":260,"wires":[["db0ea33.f1186e"]]},{"id":"26c339f9.346fbe","type":"inject","z":"c6efd2b6.ab02e8","name":"","topic":"","payload":"true","payloadType":"bool","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":130,"y":260,"wires":[["25016441.6447bc"]]},{"id":"25016441.6447bc","type":"function","z":"c6efd2b6.ab02e8","name":"Dynamically Select file","func":"// Override the selected file.\nmsg.selectedFile=\"Porta aperta\"\nreturn msg;","outputs":1,"noerr":0,"x":300,"y":260,"wires":[["536e58b3.bb8468"]]},{"id":"4f941d61.f52c4c","type":"ttsultimate-config","z":"","name":"GoogleTTS","noderedipaddress":"192.168.1.219","noderedport":"1980","purgediratrestart":"leave","ttsservice":"googletts"}]
```
</details>

This node allow you to upload your custom message and play it via ttsultimate without the need of an internet connection. You can use it, for example, with your alarm panel, to annuce a zone breach, a doorbell or so.

**Name**<br/>
Node name

**File to be player** <br/>
Select a file to be played. You can upload one or multiple files at the same time via the "upload" button.

**Priority**<br/>
If set to <b>true</b>, the OwnFile message will cancel the current TTS queue, will stop the current phrase being spoken and the TTS-Ultimate node will play this priority message.<br/>
Please refer to *msg.priority* msg input property of TTS-Ultimate for info on how this message will be handled<br/>

## INPUT MESSAGE 

**msg.payload = true**<br/>
Begin play of the message <br/>

**msg.selectedFile = "Garage door open"** <br/>
Overrides the selected message and plays the filename you passed in. Please double check the spelling of the filename (must be the same as you can see in the dropdown list of your own files, in the node config window) and do not include the <b>.mp3</b> extenson.<br/>

**msg.priority**<br/>
If set to <b>true</b>, the OwnFile message will cancel the current TTS queue, will stop the current phrase being spoken and the TTS-Ultimate node will play this priority message.<br/>
Please refer to *msg.priority* msg input property of TTS-Ultimate for info on how this message will be handled<br/>


![Logo](https://raw.githubusercontent.com/Supergiovane/node-red-contrib-tts-ultimate/master/img/madeinitaly.png)
    
[license-image]: https://img.shields.io/badge/license-MIT-blue.svg
[license-url]: https://github.com/Supergiovane/node-red-contrib-tts-ultimate/master/LICENSE
[npm-url]: https://npmjs.org/package/node-red-contrib-tts-ultimate
[npm-version-image]: https://img.shields.io/npm/v/node-red-contrib-tts-ultimate.svg
[npm-downloads-month-image]: https://img.shields.io/npm/dm/node-red-contrib-tts-ultimate.svg
[npm-downloads-total-image]: https://img.shields.io/npm/dt/node-red-contrib-tts-ultimate.svg
[facebook-image]: https://img.shields.io/badge/Visit%20me-Facebook-blue
[facebook-url]: https://www.facebook.com/supergiovaneDev