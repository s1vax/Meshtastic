# 🌐 Meshtastic Technology --> How it works? What we use? How do we start?
# 📡 Introduction to Meshtastic

<p align="center">
   
<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/a6218dca-af3a-496f-8577-7fef0b3c06f1" />

</p>

  [![Meshtastic](https://img.shields.io/badge/Meshtastic_Website-00750B?style=for-the-badge)](https://meshtastic.org/) 
  [![Meshtastic ARG](https://img.shields.io/badge/Meshtastic_Argentina-1489A6?style=for-the-badge)](https://mesharg.com.ar/) 



## Welcome to this guide about ***Meshtastic***. This repository aims to explain the fundamentals of this decentralized communication technology and document the configuration of specific nodes.

<br>

### 🗃️ Repository Structure
```
🌐 Meshtastic
├── 🔎 ¿What is Meshtastic? 
│
│
├── 🎯 ¿What is it used for?
│
│
├── ⚙️ ¿How it works?
│    ├── 📡 LoRa technology
│    │
│    └── 📡 Mesh Topology
│
│
├── 🎨 ¿What types of Meshtastic nodes exist?
│    ├── - Infrastructure Nodes (Fixed)
│    │
│    ├── - Personal or Mobile Nodes
│    │
│    └── - Specialized Nodes (Telemetry and Tracking)
│
│
├── 👾 ¿Wanna play? --> A mini cybersecurity (OSINT) game for Meshtastic
│    └── A small OSINT challenge in Spanish related to Meshtastic 
│        (you don't need a node to do it, just internet and lots of enthusiasm!)
│
│
├── 🚀 ¿How can we start? --> General steps to start using Meshtastic
│    ├── - Get the Hardware
│    │
│    ├── - Flash the Firmware
│    │
│    ├── - Use the Meshtastic App´s
│    │
│    └── - Pair and Configure
│
│
├── 🛠️ Hardware and Specific Configurations
│    ├── 🔹 Heltec T114 v2 (with screen)
│    │
│    ├── 🔹 Seed Studio Xiao nrf52840
│    │
│    └── 🔹 Other Meshtastic models
│
│
├── 🧊 3D cases (📌 in progress)
│
│
│
├── ⚖️ Disclaimer
│
└── I hope you found it useful and entertaining. If so, leave a star ⭐ Best wishes and much success!
```

<br>

## 🔎 ¿What is Meshtastic?

***Meshtastic*** is an open-source project that allows you to create a decentralized mesh network using ***LoRa*** (Long Range) technology. 

Unlike traditional communications that rely on cell towers or central Wi-Fi routers, Meshtastic allows devices to communicate directly with each other. It's like having a private, encrypted text messaging network that operates completely independently, without needing the internet or carrier subscriptions.

<br>

## 🎯 ¿What is it used for?

The flexibility of not depending on external infrastructure makes Meshtastic ideal for multiple scenarios:

* **Off-Grid Communications:** Maintain contact in areas without cell phone coverage (mountains, rural areas or isolated routes).

* **Security and Privacy:** Featuring AES256 encryption, it is used by communities and groups that require secure and auditable communication channels.

* **Emergency Cases:** Rapid deployment of communication networks after natural disasters where traditional infrastructure has collapsed.

* **Events and Coordination:** Keeping a team connected at festivals, conferences, or large venues.

* **RF experimentation:** Telemetry tests, antenna range and network topologies in unlicensed bands (such as 915 MHz or 433 MHz, depending on the region).

<br>

## ⚙️ ¿How it works?

The system is based on two fundamental pillars:

📡  **LoRa technology:** It uses long-range, low-power radio frequency modulation. This allows small data packets (such as text or GPS coordinates) to be sent several kilometers away using small batteries.

- `Frequencies`: Meshtastic uses ISM (Industrial, Scientific, and Medical) license-free bands. These vary by region to comply with local laws:
    - North America: 915 MHz
    - Europe: 868 MHz
    - Asia/Oceania/Others: Often 433 MHz or 923 MHz.
- `Power Consumption`: Extremely low. Most devices (like the Heltec V3 or T-Beam) consume between 20mA and 100mA while active. On a standard 3000mAh 18650 battery, a device can last anywhere from 24 hours to several days depending on screen usage and sleep settings.
- `Distances`: 
    - Urban: ≈ 1–5 km (due to buildings/interference).
    - Rural/Line of Sight: ≈ 10–30 km.
    - Record-breaking: With clear line of sight (mountain top to mountain top), distances can exceed ≈ 100+ km.
    
<br>

📡  **Mesh Topology:** Here's the magic. Each device (node) in the network not only sends and receives its own messages, but also acts as a repeater for the others. If Node A wants to talk to Node C, but they are far apart, the message can hop through Node B, which is in between. The more nodes there are, the more robust and extensive the network becomes.

- `Meshtastic Maps`: These are web-based platforms (like MeshMap or En some regions, MQTT-linked maps) that show the location of "public" nodes. If your device has GPS and you opt-in to sharing, your node will appear on a global map, helping others see the network's coverage in their area. Some maps are:
     - Liam Cottle: https://meshtastic.liamcottle.net/
     - MeshMap: https://meshmap.net/
- `MQTT` (Message Queuing Telemetry Transport): This is a bridge between the radio world and the internet. If one node in a mesh is connected to a phone with internet or a Wi-Fi gateway, it can push the local mesh traffic to an MQTT Broker. As result, you can talk to a mesh network in another city or country as if they were right next to you, effectively linking "islands" of radio users together via the web.

<br>

## 🎨 ¿What types of Meshtastic nodes exist?
- ***Infrastructure Nodes (Fixed)***: They are designed to be located in strategic points, generally at height and with a constant source of energy (either from the electrical grid or with a solar panel system and large batteries).
   - `Router`: It is the backbone of the network. Its primary purpose is to receive and retransmit messages to expand coverage. It is designed to be always on, does not enter deep sleep mode, and is visible in the users' node list.
   - `Repeater`:It performs the same infrastructure function as the router (retransmitting packets), but it is "invisible." It does not transmit its own information (NodeInfo) to the network, which prevents saturating users' contact lists and saves bandwidth.

   <br>
   
- ***Personal or Mobile Nodes***: These are the nodes that users carry with them, usually connected to a cell phone via Bluetooth. Power management is critical here.
   - `Client`: This is the default role when you flash a board. It's designed to be actively used by a single person. It routes messages from other nodes to help the network, but enters sleep mode to conserve battery power when not in use.
   - `ClientMute`: It works the same as the Client, but it doesn't act as a repeater. It only sends and receives user messages. It's ideal when you need to maximize battery life or when you're in an area with many nodes and relaying all the traffic would quickly drain your power.
   - `Router & Client`: It's a combination. It functions like a router (it doesn't sleep, it prioritizes traffic), but it also assumes there's a user actively connected to it sending messages. It requires a good power supply.
   - `ClientHidden`: Think of it as a stealth version of the regular Client. It behaves almost the same in terms of sending and receiving your messages, but it tries to stay invisible to the rest of the mesh.It does not advertise itself loudly and avoids being listed or easily discovered by other nodes.

   <br>
   
- ***Specialized Nodes (Telemetry and Tracking)***: They are designed for very specific tasks, generally "headless" (without a screen or user constantly interacting).
   - `Tracker`: Optimized for geolocation. Its job is to wake up, obtain a GPS position, transmit it to the network with priority, and then go back to sleep. Useful for tracking vehicles, pets, or, for example, fast-moving objects such as rockets or weather balloons.
   - `Sensor`: It is used for nodes that are connected to external hardware modules (temperature, humidity, pressure sensors, etc.). It wakes up, takes the telemetry reading, transmits it via LoRa, and returns to a very low-power mode.
   - `TAK`: A very specific role for nodes that are used in conjunction with the ATAK (Android Team Awareness Kit) application, optimizing traffic and routing for the needs of that platform.

<br>

## 👾 ¿Wanna play? --> A mini cybersecurity (OSINT) game for Meshtastic 
Here's a challenge I created for the first Hack the Box Meetup hosted by Ekogroup San Luis, where we tackled OSINT challenges. This particular challenge is related to Meshtastic!

In short, what is OSINT? --> Open Source Intelligence (OSINT) is the legal collection, analysis, and processing of publicly available information to transform it into useful knowledge. This methodology encompasses data from the internet, social media, public records, and news outlets to investigate individuals, companies, or security threats.

¿En que consiste este mini-desafio? Te pondras en el lugar de un agente de OSINT y deberas de encontrar, mediante cualquier herramienta o sitio que se te ocurra que este en internet (y sea legal obvio), 2 dispositivos Meshtastic que estan siendo usados por un grupo cibercriminal llamado FSociety (si, Mr. Robot referencia) para comunicarse entre si, y orquestar ataques a bases de datos en ciertos puntos de Argentina y Uruguay.

***NOTE***: The challenge is in Spanish, but you can translate it and complete it without needing a Meshtastic node. All you need is a device you can use to access the form and a strong desire to have fun.!

👉 https://forms.gle/bTwt6tVbDUNSLwcEA


<br>

## 🚀 ¿How can we start? --> General steps to start using Meshtastic

Getting started with Meshtastic is accessible and requires few components. In short, the steps to begin using any Meshtastic device are as follows:

1.  ***Get the Hardware:*** You need a development board that integrates a microcontroller (such as an ESP32 or nRF52) and a LoRa radio chip.
2.  ***Flash the Firmware:*** ⚠️ ***IMPORTANT*** ⚠️ Before powering the board, we must connect an antenna, either the one that comes on the package or another one. Once this is secured, we proceed to connect the board to the computer and install the official Meshtastic firmware using their web flasher (https://flasher.meshtastic.org/).
3.  ***Use the Meshtastic App´s:*** Install the Meshtastic app on your smartphone (iOS or Android), or visit the Meshtastic setup website for PC (https://client.meshtastic.org).
4.  ***Pair and Configure:*** Connect your Meshtastic device to your phone or your PC via Bluetooth, Network or Serial. From the app/website, you can configure your region (legal frequency), set a username, as others settings that we are going to look up, and then, we can start sending messages to the mesh network.

<br>

## 🛠️ Hardware and Specific Configurations

In the following sections, we will delve into two specific mesh device models, the Heltec T114 v2 and the Seed Xiao nrf52840, detailing their features, advantages, connection diagrams, flashing, and configurations. They will be configured as Personal or Mobile Nodes, with the aim of verifying their functionality and establishing initial communication.

***NOTE:*** This configuration is based on Argentina; if you are from another country, you will probably have to make certain adjustments (mainly in the LoRa configuration section).

### 🔹 Heltec T114 v2 (with screen)

<p align="center">
<img width="214" height="99" alt="image" src="https://github.com/user-attachments/assets/8528d90b-ed64-4ae9-bb28-11259c6f82cb" />
</p>


### 🛒 Things we need

- A `PC` for the firmware flashing & for power
- The `Heltec t114 v2 (with screen)` module
- `Phone` or `PC` for connectivity & configuration (GPS, MQTT, Channels, etc.)
- `Micro USB cable`

<br>

### ❓ How do we configure it?

- 👉 First, we can get this mesh device in these following pages (from Argentina):
   - Starware (model without GPS plate) --> https://tienda.starware.com.ar/producto/placa-desarrollo-lora-bt-gps-heltec-mesh-node-t114-nrf52840sx1262-v20-pantalla/
   - Starware (model with GPS plate) --> https://tienda.starware.com.ar/producto/kit-desarrollo-lora-bt-gps-heltec-antena-mesh-node-t114-nrf52840sx1262-v2/
   - Mercado Libre (international) (model with 3D Case but without GPS plate) --> https://www.mercadolibre.com.ar/meshtastic-tracker-t114-v2-nordic-nrf52840-sx1262-lorawa/p/MLA2068680206#polycard_client=search-desktop&search_layout=grid&position=26&type=product&tracking_id=304d39fc-bcfe-4be4-abb9-f76de48062d1&wid=MLA3055433870&sid=search
   
- 📻 Once the board has been acquired, we will perform the initialization steps:
   - ⚠️ ***IMPORTANT*** ⚠️ Before powering the board via the USB-C port, we must connect an antenna (either the one it comes with or any other we have) to its LoRa port. Once this is done, we connect it to our PC (for power and flashing) via the USB 2.0 ports [USB 3.0 ports are not recommended for connecting the board due to interference].
   - As the next step, we will flash the board using its web flasher (https://flasher.meshtastic.org/). However, unlike the Meshtastic board described below (the Xiao nRF52840 Seed), the Heltec is not flashed directly from the website; there is one less step. The flashing steps are as follows:
          
        --> We open the web flasher, and go to the section of `Select Target Device`
               <p align="center">
          <img width="1902" height="836" alt="image" src="https://github.com/user-attachments/assets/f29672f0-f267-45ff-8dba-a8be2c8c7d83" />
          </p>
        --> We select or search for our plate, in this case the `Heltec t114 v2 NRF52840 (with screen)`:
      <p align="center">
     <img width="1828" height="930" alt="image" src="https://github.com/user-attachments/assets/e46cfed5-cdd8-4d65-805c-01bb57e27aed" />
     </p>
     
        --> Next, in the `Firmware` section, we must select the version to download. It is recommended to choose a `Beta` version, as these are the most stable.
              <p align="center">
        <img width="1828" height="925" alt="image" src="https://github.com/user-attachments/assets/0df711dc-945d-4329-8937-ae3ef16620d7" />
     </p>
     
        --> Once you've selected the firmware version, click `Flash`, and a pop-up window will appear detailing all the features of that version. Click `Continue`.
      <p align="center">
        <img width="1349" height="757" alt="image" src="https://github.com/user-attachments/assets/bdae9d50-a56a-4796-a8e6-b53f659a9639" />
           </p>

        --> Following the previous step, another pop-up window will appear. Click directly on `Download UF2`:
      <p align="center">
        <img width="1200" height="700" alt="image" src="https://github.com/user-attachments/assets/1bc2a852-022c-410f-8626-694ff326b40b" />
           </p>

        --> What will happen is that a file will be downloaded. You will need to copy this file to the folder created by the Meshtastic device when you connect it to your PC (it appears as a disk). It's normal for this to take a little while and for the board to restart. 

      <br>
      <br>
         
        And that's it! ✅ Your Meshtastic board is now flashed and ready to use and configure.

      <br>

   - ***Optional step [Once the board has been flashed, it can be disconnected from the PC]***  
   - After that, to obtain the Meshtastic configuration software, we will download the Meshtastic app from the Play Store on our mobile phone, or we can directly access it from our PC at: https://client.meshtastic.org
   - If we choose to configure the board via cell phone, we turn on our phone's Bluetooth (there are also options via USB cable and internet on the phone). If we selected PC, we can simply configure it using a USB cable (on a PC, it can also be done via Bluetooth or HTTP).
     
     --> Connections type on cell phone (Bluetooth, Network & Serial)
     
        <p align="center">
        <img width="314" height="51" alt="572789225-ec389f05-ea8f-4707-bf0c-ec3644b65645(2)" src="https://github.com/user-attachments/assets/d6ac35a9-93d3-4c31-9e4d-95d99729f183" />
        </p>  
        
     --> Connections type on PC (HTTP, Bluetooth & Serial)

      <p align="center">
        <img width="484" height="92" alt="571588472-e44b108b-ee8f-4a3c-bdcd-740c9b57c742(2)" src="https://github.com/user-attachments/assets/41406ee1-292e-4e23-92cb-e795a250769e" />
        </p>  
      
   - If you disconnected the board after flashing, in the *Optional Step*, you must power it again using the USB-C cable (you can power it this time through the USB 2.0 ports of your PC as at the beginning or through a portable battery, or something that provides 5V).
    
   - Open the Meshtastic app (on your phone) and your device should appear in the `Connection` section, ready to connect via Bluetooth (or other options); it usually has a name like *"Meshtastic_XXXX"*. On a PC, go to `Add connection` (select the method you want to use to connect the device), and then click `Connect`.

     --> On cell phone:
     
<p align="center">
   <img width="314" height="588" alt="image" src="https://github.com/user-attachments/assets/ec389f05-ea8f-4707-bf0c-ec3644b65645" />
</p>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; --> On PC:

<br>
<br>
     
<p align="center">
   <img width="615" height="225" alt="image" src="https://github.com/user-attachments/assets/07d156f6-f08c-4a0a-86a7-2cd91423eb0c" />
</p>
<br>
<br>
<br>
   
- 💽 Board settings ***(important for proper operation)***

Now in this section we'll see how to get the node working. It's important to note that this is a basic configuration, not the final one; its sole purpose is to establish initial communication between the nodes and verify their functionality. This configuration will vary depending on our needs and objectives regarding the Mestatastic node—that is, what we want to do with it.

Once we're connected to the device using any Meshtastic app, we'll first go to the section of `Settings`, and to begin with, we will go to the option of `LoRa`.

<br>
<br>

 🔸 ***Settings: Radio Configuration: LoRa***
   - Within `LoRa`, we will go to the `Options` subsection and verify that:
      - `Region` is set to: Australia / Brazil / New Zealand
      - `Use Presets` is set to enabled/on
      - `Presets` is set to: LONG_FAST
   
   - Next, we continue with the following subsection of `Advanced`. Here we will activate the following:
       - `Ok to MQTT`
       - `Transmit Enabled`
   - In the same section (⚠️ for now, due to the current development of the san luis [Argentina] community in meshtastic) we will put the following settings: (but if you are from another city/province/country with a higher number of nodes and activity, it is recommended to place fewer hops)
       - `Number of Hops`: 7
       - `Frecuency Slot`: 20
   - Even within that section, we will activate `RX Boosted Gain`
   - And finally, you should see the following configuration at the end of this sub-section:
       - `Frequency Override`: 919.875
       - `Transmit Power`: 27

<br>
<br>

 🔸 ***Settings: Radio Configuration: Channels***
   - First, (only from our cell phone, in the Meshtastic app) we will go to the channel settings and tap where it says `LongFast`. A new window will open and we must have the following configured (this is due to the map I am using which I will explain below in the `MQTT` settings section):
      - `Uplink enabled` activated
      - `Downlink enabled` deactivated
      - `Position enabled` activated
      - `Precise location` deactivated
      - And the distance bar should be set to: 1194 ft

   - ***Current Mestastic channels in Argentina (Secondary channels)*** 
   
     - In this section we will also add the channels for Argentina (means through which communication with other mesh nodes/devices is possible)

     - You can open the following link by tapping it directly on your mobile phone, or on a PC, where you must paste the link into the Meshtastic website https://client.meshtastic.org (the image below explains how), and this will automatically add the argentinian mesh communication channels (all of them) to the Meshtastic app or website:

         https://meshtastic.org/e/?add=true#CgkSAQEoATABOgAKNBIgaB3K7ZIciBKq49nxn5gVmPQEtbTUVZOHKxuCaCKaHtAaCkJhaXJlc01lc2goATABOgAKNRIgyVyN1359YQb0S1LW2cslgMrXHbTkHnR1TSHYDa7VCCsaC01lbmRvemFNZXNoKAEwAToACjoSIJLLPuDDIXPbp2rlPIum4sdC7f6ZI1jL9TyBa9Hx_IOfGgtSb3NhcmlvTWVzaCUDAAAAKAEwAToACjASIMPZ0wFE2KdnhaOysgn6OWuNmEjOHsH61fz0qMXI6wDyGgZFUk1lc2goATABOgAKMxIgAe6IxXali8k08O27Gl04A_2yzvTj9XVnb-r0ZnpLRpkaCVBBVEFHT05JQSgBMAE6AAoxEiAHuNgMktbL1NKdqNYj_IAkRMsFyM3ZE1dRTiNLh5HImhoHTlFObWVzaCgBMAE6ABIWCAEY-gEgCygFOAZAB0gBUB5oAcAGAQ

     - If you don't want them all added at the same time, and only want to add one or a couple, you can add the following PSKs for the channels you want:

| Channel | PSK | Region |
|--------|-----------|--------|
| BairesMesh | aB3K7ZIciBKq49nxn5gVmPQEtbTUVZOHKxuCaCKaHtA= | CABA & AMBA 
| RosarioMesh | kss+4MMhc9unauU8i6bix0Lt/pkjWMv1PIFr0fH8g58= | Rosario 
| NQNmesh | B7jYDJLWy9TSnajWI/yAJETLBcjN2RNXUU4jS4eRyJo= | Neuquén
| CordobaMesh |  CoRd0B4lHaBoN6OWT0u2EvNX9Jci7gsIiIJtD30BCCw= | Córdoba
| ERMesh | w9nTAUTYp2eFo7KyCfo5a42YSM4ewfrV/PSoxcjrAPI= | Entre Ríos
| MendozaMesh | yVyN1359YQb0S1LW2cslgMrXHbTkHnR1TSHYDa7VCCs= | Mendoza

<br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--> If you don't know how to copy and use the link above on your PC on the Meshtastic website, you must click on the sections of the site in the numerical order shown in the following image:
     
<p align="center">
<img width="950" height="550" alt="image" src="https://github.com/user-attachments/assets/b9ec420b-03cc-49b4-b522-d11317fd558d" />
</p>

<br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--> After that, on PC, the channels should look like this:

<p align="center">
<img width="950" height="600" alt="image" src="https://github.com/user-attachments/assets/52f54a89-1c09-4a23-a894-3580ce11e61d" />
</p>

<br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--> On mobile, they should look like this:

<p align="center">
<img width="300" height="600" alt="WhatsApp Image 2026-05-01 at 21 10 53" src="https://github.com/user-attachments/assets/2dc884c5-0c9e-4ffb-92c1-2b6d11d9b2f1" />
</p>

<p align="center">
<img width="300" height="600" alt="WhatsApp Image 2026-05-01 at 21 10 32" src="https://github.com/user-attachments/assets/80559d45-c3be-4995-b35d-b94f832d6e91" />
</p>


<br>
<br>

 🔸 ***Settings: Device Configuration: User***
   - Here you can configure your device name and view your `NODE ID`, as well as 2 other options (not recommended).

<br>
<br>

 🔸 ***Settings: Device Configuration: Device***
   - In this section we must have the following. In the sub-section of `Options`, we seek that:: 
      - `Device Role` is set to: CLIENT
      - `Rebroadcast Mode` is set to: ALL
      - Y `Node info Broadcast Interval` is set to: 3 hours
   
   - Moving on to the next subsection, we'll go to `Hardware`. Here we can configure it to our liking.
      - I personally have activated: `Tiple Click Ad Hoc Ping` & `Led Heartbeat`
      - In `Time Zone` should be: GMT3

<br>
<br>

 🔸 ***Settings: Device Configuration: Position***
   - We move on to the section of `Position`. 
   - In the sub-section of `Position Packet` we verify that: 
      - `Broadcast Interval` is set to: 15 minutes
      - `Smart Position` is set to activated
      - `Smart Interval` is set to: 30 seconds
      - Y `Smart Distance` is set to: 100
   
   - Moving on to the next subsection, we have `Device GPS` where we look for:
      - `Fixed Position` is set to disabled
      - `GPS Mode (Physical Hardware)` is set to: ENABLED
      - `GPS Polling Interval` is set to: 8 seconds

   - Continuing, we move on to the sub-section `Position Flags` where we will need to have:
      - `Position Flags` in: 811

   - And finally, in the last subsection of `Advanced Device GPS`, we need to make sure all pins are at 0.

<br>
<br>
   
 🔹 ***We will omit some sections since the objective of this repository is not to go into depth, but to allow the use and access of Mestatastic devices, that is, to test an initial communication and its operation***

 <br>
 <br>

  🔸 ***Settings: Module Configuration: MQTT***
  
   - Here we begin with the sub-section of `MQTT Config` where we should have:
       - `MQTT enabled` activated
       - `Address`, `Username` y `Password`. These form the ID of the map server we want to join, that is, where we want our node to appear. We can only make our node appear on one Meshtastic map, out of the many created by the community. For example, I recommend these ones:

           <p align="center">
           <img width="400" height="300" alt="WhatsApp Image 2026-05-01 at 22 02 29" src="https://github.com/user-attachments/assets/ff036fab-0aab-46e9-b9fe-f95e073111b9" />
           </p>
       
       - `Encryption enabled` activated (It will depend on the pre-set configurations of the map we want to connect to.)
       - `JSON output enabled` disabled (It will depend on the pre-set configurations of the map we want to connect to.)
       - `TLS enabled` It will be enabled by default given our configuration
       - `Root topic` in: msh/ANZ
       - And `Proxy to client enabled` activated
       
   - Next, we have the following subsection of `Map reporting`, where we are looking for:
       - `Map reporting` activated
       - The `I agree` part, activated
       - Then, on the distance bar given in miles, we leave it at: 1.8 mi
       - And finally, we leave `Map reporting interval (seconds)` in: 1 hour

<br>
<br>

***And that's it, we can now connect and send messages to the Mehtastic network ✅***
       


<br>

### ⚡Advantages
- Comes with built-in screen
- Comes with antenna
- It comes with soldering pins
- It comes with power cables for batteries (portable)
- It comes with an specific input for a GPS module (it doesn´t include a GPS module)
- Medium/small hardware size
- Peripheral customization (high)
- USB-C power input
- Solar & Battery voltage inputs

<br>

### 📈 ¿What new features can we add?

- ***GPS Module:*** Meshtastic devices allow you to use your connected devices (cell phone or PC) as GPS. However, it's also possible to apply their own geolocation system so they don't depend on another device when being made "portable". That's why a GPS module can be added to identify their coordinates and other data. In the case of the Heltec t114 v2, it comes with an 8-pin connector specifically for GPS/GNSS modules (such as the L76K GNSS).

- ***Energy Systems:*** 
   - `Solar Panels + Battery`: A 5V to 6V panel (max 1W-2W) can be connected directly to the 1.25mm, 2-pin solar connector. No external charge controller is required. Additionally, a LiPo/Li-ion battery is needed for energy storage; this Heltec model also includes a 1.25mm, 2-pin battery connector for this purpose.

     📌 ***Solar Panel Connection diagram (in progress)***
   
   - `LiPo/Li-ion Batteries`: It supports 3.7V cells. It is possible to scale from the standard 800-1100mAh to 18650 or 21700 cells of 5000mAh for extended runtime.
   
        - `Protection Circuit (PCM/BMS) for LiPo Batteries` (In some cases): Many LiPo batteries come "bare." They need a small circuit board at the tip with the DW01 and 8205A chips.
Function: Cuts off power if the voltage drops below 2.4V (preventing the battery from permanently failing) or if there is a short circuit.

        - `NTC Thermistor` (Optional but recommended): If the node will be in the sun (inside a box or structure), the heat can be dangerous. Some chargers have a "TEMP" pin that, when connected to a thermistor attached to the battery, stops charging if the temperature exceeds 45°C - 50°C.
        
        - `JST-PH Connectors` (2.0mm) o `SH` (1.25mm): Ensure the polarity is correct. Important note: The red/black wire standard on Chinese batteries is sometimes reversed compared to what Heltec or Seeed boards require. Measure with a multimeter before plugging in.
   
- ***I2C Sensors:***
   - `BME280 / BME680`: It measures temperature, humidity, atmospheric pressure, and (in the case of the 680) air quality. It is ideal for remote weather stations.
   - `INA219`: Useful if you plan to monitor voltage and current consumption, especially in solar installations.
   - `SHT31`: A high-precision alternative for temperature and humidity.
   
- ***RF Upgrades (Antennas & Connectors):***
The factory-installed "spring" antenna is limited. To improve range:
   - `Pigtail IPEX (U.FL) a SMA`: It allows the use of higher gain external antennas.
   - `Dipole or Fiberglass Antennas`: If the node will be fixed (Router), a 3dBi to 5dBi antenna optimized for the frequency of your area (typically 915MHz in Argentina) will make a noticeable difference in the coverage radius.
   
- ***User Interface and Alerts:***
   - `Passive Buzzer`: A buzzer can be configured to receive audible alerts when a message arrives or a new node joins the network.
   - `Additional Buttons`: Although it has two physical buttons, other GPIO pins can be mapped for navigation functions on the 1.14" TFT screen.
   
<br>
<br>
<br>
<br>
<br>
<br>

### 🔹 Seeed Studio XIAO nRF52840 Kit

<p align="center">
<img width="150" height="200" alt="image" src="https://github.com/user-attachments/assets/3354f50d-0bc4-4644-bf62-ac7d54137ba6" />
</p>

### 🛒 Things we need

- A `PC` for the firmware flashing & for power
- The `Xiao nrf52840 Kit` module
- `Phone` or `PC` for connectivity & configuration (GPS, MQTT, Channels, etc.)
- `Micro USB cable`

<br>

### ❓ How do we configure it?

- 👉 First, we can get this mesh device in this following page (from Argentina):
   - Mercado Libre --> https://www.mercadolibre.com.ar/xiao-nrf52840--wiosx1262-kit-meshtastic-blelora-862930-m/up/MLAU3394520637#polycard_client=search-desktop&search_layout=grid&position=1&type=product&float_highlight=repurchase&tracking_id=3a7aa470-9531-405d-8084-412034cb75f7&wid=MLA1519008445&sid=search
   
- 📻 Once the board has been acquired, we will perform the initialization steps:
   - ⚠️ ***IMPORTANT*** ⚠️ Before powering the board via the USB-C port, we must connect an antenna (either the one it comes with or any other we have) to its LoRa port. Once this is done, we connect it to our PC (for power and flashing) via the USB 2.0 ports [USB 3.0 ports are not recommended for connecting the board due to interference].
   - As a next step, we proceed to flash the board using its web flasher (https://flasher.meshtastic.org/). The flashing steps are as follows:
     
        --> We open the web flasher, and go to the `Select Target Device` section.
          <p align="center">
          <img width="1902" height="836" alt="image" src="https://github.com/user-attachments/assets/f29672f0-f267-45ff-8dba-a8be2c8c7d83" />
          </p>
        --> We select or search for our board, in this case the `Seed Xiao nrf52840 Kit`:
           <p align="center">
           <img width="1901" height="896" alt="image" src="https://github.com/user-attachments/assets/23da2f63-b9a1-472c-8a28-32e6508b90d4" />
           </p>
        --> Next, in the `Firmware` section, we must select the version to download. It is recommended to choose a `Beta` version, as these are the most stable.
           <p align="center">
           <img width="1600" height="820" alt="image" src="https://github.com/user-attachments/assets/b208a8be-7708-401a-8fe0-17b497d2f034" />
           </p>
        --> Once you've selected the firmware version, click `Flash`, and a pop-up window will appear detailing all the features of that version. Click `Continue`.
           <p align="center">
           <img width="1677" height="753" alt="image" src="https://github.com/user-attachments/assets/fbbf21ac-f5b2-4396-a7e5-1df12ac60add" />
           </p>
        --> Next, we'll see another pop-up window. What we need to do is put the board into DFU mode. To do this, click where it says `Enter DFU Mode`, and a list of USB ports with connected devices will open in your browser. You'll need to locate your mesh board (by noting which COM port on your computer it's connected to), click on it, and then click `Connect`.
           <p align="center">
           <img width="900" height="600" alt="image" src="https://github.com/user-attachments/assets/745bc626-58d5-471b-8b8d-a894ed58c822" />
           </p>

        <p align="center">
       <img width="1598" height="837" alt="image" src="https://github.com/user-attachments/assets/07a5120c-c9c3-4f54-8823-1dcb32fe30dd" />
           </p>
           
        --> Once the correct COM port has been selected, click on `Download UF2`:
          <p align="center">
         <img width="1570" height="872" alt="image" src="https://github.com/user-attachments/assets/998a0114-7e0a-4791-bbb7-626decdafb11" />
           </p>
           
        --> Finally, once this is done, a file will be downloaded. Copy this file to the folder created by the Meshtastic device when you connect it to your PC (it appears as a disk). It's normal for the transfer to take a little while and for the board to restart.

      <br>
      <br>
         
        And that's it! ✅ Your Meshtastic board is now flashed and ready to use and configure.

      <br>

   - ***Optional step [Once the board has been flashed, it can be disconnected from the PC]***    
   - After that, to obtain the Meshtastic configuration software, we will download the Meshtastic app from the Play Store on our mobile phone, or we can directly access it from our PC at: https://client.meshtastic.org
   - If we choose to configure the board via cell phone, we turn on our phone's Bluetooth (there are also other configuration options such as USB cable and internet access on the phone). If we selected PC, we can simply configure it using a USB cable (it can also be done via Bluetooth or HTTP on a PC).
     
     --> Connections type on cell phone  (Bluetooth, Network & Serial)
        <p align="center">
        <img width="314" height="51" alt="572789225-ec389f05-ea8f-4707-bf0c-ec3644b65645(2)" src="https://github.com/user-attachments/assets/f8f4a5dc-28ad-420c-a987-fc675efa0827" />
        </p>  
     
     --> Connections type on PC (HTTP, Bluetooth & Serial)
        <p align="center">
        <img width="484" height="92" alt="571588472-e44b108b-ee8f-4a3c-bdcd-740c9b57c742(2)" src="https://github.com/user-attachments/assets/f8514d62-85b7-4f7e-93c8-93c133294fd8" />
        </p>  
   - If you disconnected the board after flashing, in the *Optional Step*, you must power it again using the USB-C cable (you can power it this time through the USB 2.0 ports of your PC as at the beginning or through a portable battery, or something that provides 5V).
    
   - Open the Meshtastic app (on your phone) and your device should appear in the `Connection` section, ready to connect via Bluetooth (or other options); it usually has a name like *"Meshtastic_XXXX"*. On a PC, go to `Add connection` (select the method you want to use to connect the device), and then click `Connect`.
   
     --> On cell phone:
     
<p align="center">
  <img width="314" height="588" alt="image" src="https://github.com/user-attachments/assets/ec389f05-ea8f-4707-bf0c-ec3644b65645" />
</p>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; --> On PC:

<br>
<br>
     
<p align="center">
   <img width="615" height="225" alt="image" src="https://github.com/user-attachments/assets/07d156f6-f08c-4a0a-86a7-2cd91423eb0c" />
</p>

<br>
<br>
<br>
   
- 💽 Board settings ***(important for proper operation)***
   - This section is the same as the one above, for the Heltec t114 v2 mesh device. Therefore, if you are in Argentina, you should follow the same settings mentioned previously.
   [🔹 Heltec T114 v2 (with screen)](https://github.com/s1vax/Meshtastic/tree/main?tab=readme-ov-file#-heltec-t114-v2-with-screen) (in the `Board settings` section)

<br>

### ⚡Advantages
- Very small hardware size
- Comes with antenna
- Peripheral customization (high)
- Built-in (detachable) LoRa module
- USB-C power input
- Lower power consumption

<br>

### 📈 ¿What new features can we add?
- ***XIAO Expansion Board:***
It's a key component for adding peripherals without soldering.:
    - `OLED Screen (0.96")`: An OLED screen can be added to the Xiao nrf52840 board without the need for a Xiao Expansion Board, but it should be noted that it already comes with an integrated socket to connect an SSD1306 screen, essential for viewing messages and node status.
    - `RTC (Real Time Clock)`: It includes a PCF8563 chip that allows it to maintain the exact time even if the device restarts or loses connection.
    - `MicroSD Slot`: Essential if you plan to do Data Logging (recording GPS positions or sensor readings during a journey or flight).
    
- ***GPS Module:*** Meshtastic devices allow you to use your connected devices (cell phone or PC) as GPS. However, it's also possible to apply their own geolocation system so they don't depend on another device when being made "portable". Therefore, a `GPS module` can be added to identify their coordinates and other data. In the case of the `Seed Studio Xiao nrf52840 Kit`, it requires a Grove GPS module (`Grove - GPS Air530Z`, high precision and low power consumption, ideal for the node to transmit its location) or soldering to UART pins (TX/RX), for example to the `L76K GNSS`.

- ***Energy Systems:***
    - `Solar panels + batteries`: For these microcontrollers, a 5V to 6V panel is ideal. Between 1W and 2W is sufficient to keep an nRF52840 node powered on 24/7. The panel can be monocrystalline (rigid) or PET/ETFE (flexible for aerodynamics or low weight). This requires a `Solar Charge Controller (IC)`, as the panel cannot be connected directly to the battery; a chip is needed to manage the charging protocol.
Recommended: CN3065. It is the standard for "mini" solar systems because it handles solar current fluctuations much better than a common TP4056.

       A `Schottky diode` (such as a 1N5817) would also be needed. This is placed between the panel and the charger. It prevents "reverse current," meaning the battery would try to "charge" the solar panel at night, which would drain it.

       And also, `electrolytic capacitors`. Placing one (100µF or 470µF) at the solar charger's input helps stabilize the voltage when fast-moving clouds pass by.

        <p align="center">
       <img width="1280" height="720" alt="Conexion de baterias en parte trasera" src="https://github.com/user-attachments/assets/f408ce6e-bf67-434a-84ff-1ad43b9bb5af" />
       </p>
       
    - `LiPo/Li-ion Batteries`: For batteries, the main requirement is that they be 1S (single cell) with a nominal voltage of 3.7V. Capacity: From 400mAh (flight/compact) to 5000mAh (fixed/station).

        - `Protection Circuit (PCM/BMS) for LiPo batteries` (in some cases): Many LiPo batteries come "bare." They need a small circuit board at the tip with the DW01 and 8205A chips.
Function: Cuts off power if the voltage drops below 2.4V (preventing the battery from permanently failing) or if there is a short circuit.

        - `NTC Thermistor` (Optional but recommended): If the node will be in the sun (inside a box or structure), the heat can be dangerous. Some chargers have a "TEMP" pin that, when connected to a thermistor attached to the battery, stops charging if the temperature exceeds 45°C - 50°C.
        
        - `JST-PH Connectors` (2.0mm) o `SH` (1.25mm): Ensure the polarity is correct. Important note: The red/black wire standard on Chinese batteries is sometimes reversed compared to what Heltec or Seeed boards require. Measure with a multimeter before plugging in.
    
- ***Grove Sensors (Plug & Play):***
The Seeed ecosystem uses the Grove standard. With dedicated connectors at the base, the following can be added:
    - `Barometer/Altimeter (BMP280 / MS5607)`: Crucial for accurately measuring altitude if the node is going to be in vertical motion or in applications where atmospheric pressure is a key data point.
    - `Accelerometer/Gyroscope (ICM20689)`: If you use the "Sense" version of the XIAO, it already has one built-in, but an external one with a higher range (such as an ADXL345) is useful for measuring strong impacts or vibrations.
    
- ***RF Upgrades (Antennas and Connectors):***
Since it does not have a built-in long-range antenna, the use of a U.FL to SMA pigtail is mandatory for connection:
    - `Cloverleaf antennas`: If the node is going to be rotating or constantly changing orientation, these antennas minimize signal loss due to polarization.
    - `Spring antennas`: To keep the size as small as possible in wearable devices.
    - `Gsm Gprs Modem Antenna 2dbi U.fl Sma Cable 15cm`
    
- ***User Interface and Alerts:***
   - `Passive Buzzer`: A buzzer can be configured to receive audible alerts when a message arrives or a new node joins the network.
   - `Additional Buttons`: Other GPIO pins can be mapped for on-screen navigation functions.

<br>
<br>
<br>
<br>
<br>
<br>

### 🔹 Other Meshtastic models
<p align="center">
<img width="210" height="210" alt="MeetUps" src="https://github.com/user-attachments/assets/de9f078d-02fb-4260-952c-880a839094af" />
</p>

<br>

👉 ***You can see more Meshtastic-compatible devices (like the ones below) at:*** https://meshtastic.org/docs/hardware/devices/

<br>

- `Heltec WiFi LoRa 32 (V3)`
   - Processor: ESP32-S3.
   - Screen: integrated 0.96-inch OLED.
   - Characteristics: Includes LiPo battery charging and Wi-Fi/Bluetooth.
   - Weak point: Moderate energy consumption (not the best for small batteries).

<br>

- `Lilygo T-Beam (V1.1 / V1.2)`
The "classic" all-in-one that defined the beginnings of the network.
   - Processor: ESP32.
   - GPS: Integrated Neo-6M or Neo-M8N module.
   - Power: It includes an 18650 battery socket on the back.
   - Characteristics: Very robust and easy to carry in a backpack without complex external boxes.
   
<br>

- `LILYGO® T-Lora Pager`
   - MCU
      - ESP32-S3 (WiFi & Bluetooth 5 LE)
   - LoRa Transceiver
      - Semtech LR1121
   - QWERTY keyboard
   - AI support IMU (BHI260AP)
   - 2.33-inch long screen (222 x 480 resolution)
   - U-blox GPS module (MIA-M10Q)
   - RFID/NFC + RTC circuitry
   - TI Power Management Monitoring Chipset
   - ES8311 (microphone/speaker/headphone jack) Encoder + Keypad

<br>

- `LILYGO® T-Deck`
   - MCU
      - ESP32-S3FN16R8 (WiFi & Bluetooth 5 LE)
      - ESP32-C3 (For keyboard only)
   - LoRa Transceiver
      - Semtech SX1262
   - LILYGO® backlit T-Keyboard
   - Trackball
   - 2.8 inch ST7789 SPI Interface IPS LCD (Resolution: 320 x 240)
   - I2S Speaker/Microphone

<br>

- `RAKwireless WisBlock (RAK4631)`
Considered the "gold standard" for serious nodes and solar stations.
- Processor: nRF52840 (Ultra low consumption).
   - Modularity: "LEGO" type design; you can add weather sensors, GPS or screens using modules.
   - Characteristics: It consumes a fraction of the energy of the ESP32 models.

<br>

- `Lilygo T-Echo`
   - Processor: nRF52840.
   - Screen: 1.54-inch E-Ink (Electronic Ink), visible in sunlight.
   - Characteristics: Includes protective case, GPS and factory internal battery.

<br>

- `Station G1 (Nano G1 Explorer)`
   - Processor: ESP32.
   - Case: Robust aluminum alloy.
   - Characteristics: SMA connector for external high-gain antenna and front USB-C port.

<br>
<br>
<br>
<br>
<br>
<br>

## 🧊 3D cases (📌 in progress)
<br>
<br>
<br>
<br>
<br>
<br>

## ⚖️ Disclaimer
I am not responsible for any issues with the distributors of the links shared in this repository. Open and use them at your own risk. 

I only share the links that I have used under my own responsibility and supervision during the execution of projects with Meshtastic.

<br>

### I hope you found it useful and entertaining. If so, leave a star ⭐ Best wishes and much success!
