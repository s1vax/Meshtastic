# 🌐 Meshtastic Technology --> How it works? What we use? How do we start?
# 📡 Introduction to Meshtastic

<p align="center">
   
<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/a6218dca-af3a-496f-8577-7fef0b3c06f1" />

</p>

  [![Meshtastic](https://img.shields.io/badge/Meshtastic_Website-00750B?style=for-the-badge)](https://meshtastic.org/) 



## Welcome to this guide about ***Meshtastic***. This repository aims to explain the fundamentals of this decentralized communication technology and document the configuration of specific nodes.

---

### 🙌 Pueden traducir este y los demas repositorios, con el traductor de google de su navegador web o con alguna otra extensión 🙌

---

## 🔎 ¿What is Meshtastic?

***Meshtastic*** is an open-source project that allows you to create a decentralized mesh network using ***LoRa*** (Long Range) technology. 

Unlike traditional communications that rely on cell towers or central Wi-Fi routers, Meshtastic allows devices to communicate directly with each other. It's like having a private, encrypted text messaging network that operates completely independently, without needing the internet or carrier subscriptions.

## 🎯 ¿What is it used for?

The flexibility of not depending on external infrastructure makes Meshtastic ideal for multiple scenarios:

* **Off-Grid Communications:** Maintain contact in areas without cell phone coverage (mountains, rural areas or isolated routes).
* **Security and Privacy:** Featuring AES256 encryption, it is used by communities and groups that require secure and auditable communication channels.
* **Emergency Cases:** Rapid deployment of communication networks after natural disasters where traditional infrastructure has collapsed.
* **Events and Coordination:** Keeping a team connected at festivals, conferences, or large venues.
* **RF experimentation:** Telemetry tests, antenna range and network topologies in unlicensed bands (such as 915 MHz or 433 MHz, depending on the region).

## ⚙️ ¿How it works?

The system is based on two fundamental pillars:

📡  **LoRa technology:** It uses long-range, low-power radio frequency modulation. This allows small data packets (such as text or GPS coordinates) to be sent several kilometers away using small batteries.

- *Frequencies*:
- *Power Consumption*:
- *Distances*:

📡  **Mesh Topology:** Here's the magic. Each device (node) in the network not only sends and receives its own messages, but also acts as a repeater for the others. If Node A wants to talk to Node C, but they are far apart, the message can hop through Node B, which is in between. The more nodes there are, the more robust and extensive the network becomes.

- *Meshtastic Maps & MQTT*:

## 🚀 ¿How can we start? --> General Steps

Getting started with Meshtastic is accessible and requires few components. In short, the steps to begin using any Meshtastic device are as follows:

1.  ***Get the Hardware:*** You need a development board that integrates a microcontroller (such as an ESP32 or nRF52) and a LoRa radio chip.
2.  ***Flash the Firmware:*** ⚠️ ***IMPORTANT*** ⚠️ Before powering the board, we must connect an antenna, either the one that comes on the package or another one. Once this is secured, we proceed to connect the board to the computer and install the official Meshtastic firmware using their web flasher (https://flasher.meshtastic.org/).
3.  ***Use the Meshtastic App´s:*** Install the Meshtastic app on your smartphone (iOS or Android), or visit the Meshtastic setup website for PC (https://client.meshtastic.org).
4.  ***Pair and Configure:*** Connect your Meshtastic device to your phone or your PC via Bluetooth, Network or Serial. From the app/website, you can configure your region (legal frequency), set a username, as others settings that we are going to look up, and then, we can start sending messages to the mesh network.

---

## 🛠️ Hardware and Specific Configurations

In the following sections, we will delve deeper into the configuration and optimization of 2 specific mesh device models, the Heltec T114 v2 and the Seed Xiao nrf52840, detailing their features, advantages, connection schemes, flashing and configurations.

### 🔹 Heltec T114 v2 (with screen)

<p align="center">
<img width="214" height="99" alt="image" src="https://github.com/user-attachments/assets/8528d90b-ed64-4ae9-bb28-11259c6f82cb" />
</p>


### 🛒 Things we need

- A `PC` for the firmware flashing & for power
- The `Heltec t114 v2 (with screen)` module
- `Phone` or `PC` for connectivity & configuration (GPS, MQTT, Channels, etc.)
- `Micro USB cable`
- ***[Optional]*** For power we can use a `Lipo Battery`

<br>

### ❓ How do we configure it?

- 👉 First, we can get this mesh device in these following pages (from Argentina):
   - Starware (model without GPS plate) --> https://tienda.starware.com.ar/producto/placa-desarrollo-lora-bt-gps-heltec-mesh-node-t114-nrf52840sx1262-v20-pantalla/
   - Starware (model with GPS plate) --> https://tienda.starware.com.ar/producto/kit-desarrollo-lora-bt-gps-heltec-antena-mesh-node-t114-nrf52840sx1262-v2/
   - Mercado Libre (international) (model with 3D Case but without GPS plate) --> https://www.mercadolibre.com.ar/meshtastic-tracker-t114-v2-nordic-nrf52840-sx1262-lorawa/p/MLA2068680206#polycard_client=search-desktop&search_layout=grid&position=26&type=product&tracking_id=304d39fc-bcfe-4be4-abb9-f76de48062d1&wid=MLA3055433870&sid=search
   
- 📻 Once the board has been acquired, we will perform the initialization steps:
   - ⚠️ ***IMPORTANT*** ⚠️ Before powering the board via the USB-C port, we must connect an antenna (either the one it comes with or any other we have) to its LoRa port. Once this is done, we connect it to our PC (for power and flashing) via the USB 2.0 ports [USB 3.0 ports are not recommended for connecting the board due to interference].
   - As the next step, we will flash the board using its web flasher (https://flasher.meshtastic.org/). However, unlike the Meshtastic board described below (the Xiao nRF52840 Seed), this one is not flashed directly from the website; there is one less step. The flashing steps are as follows:
          
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

        --> What will happen is that a file will be downloaded. You will need to copy this file to the folder created by the Meshtastic device when you connect it to your PC (it appears as a disk). It's normal for this to take a little while and for the board to restart. And that's it! Your Meshtastic board is now flashed and ready to use and configure.

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
   
- 💽 Board settings ***(important for proper operation)***
   - Ahora en esta parte veremos como hacer funcionar el nodo. Una vez que estemos conectados con el dispositivo por medio de cualquier app de Meshtastic, en primer lugar vamos a ir al apartado de `Settings`, y entraremos a la opcion de `LoRa`. Aqui vamos a
   
   - ***Canales de meshtastic actuales de Argentina*** (el siguiente link lo pueden abrir desde su celular o en PC, pegar el link en el sitio web de Meshtastic (mas abajo en la imagen se explica como), y hara que se agreguen automaticamente los canales de comunicacion mesh en la app o web de Meshtastic):
https://meshtastic.org/e/?add=true#CgkSAQEoATABOgAKNBIgaB3K7ZIciBKq49nxn5gVmPQEtbTUVZOHKxuCaCKaHtAaCkJhaXJlc01lc2goATABOgAKNRIgyVyN1359YQb0S1LW2cslgMrXHbTkHnR1TSHYDa7VCCsaC01lbmRvemFNZXNoKAEwAToACjoSIJLLPuDDIXPbp2rlPIum4sdC7f6ZI1jL9TyBa9Hx_IOfGgtSb3NhcmlvTWVzaCUDAAAAKAEwAToACjASIMPZ0wFE2KdnhaOysgn6OWuNmEjOHsH61fz0qMXI6wDyGgZFUk1lc2goATABOgAKMxIgAe6IxXali8k08O27Gl04A_2yzvTj9XVnb-r0ZnpLRpkaCVBBVEFHT05JQSgBMAE6AAoxEiAHuNgMktbL1NKdqNYj_IAkRMsFyM3ZE1dRTiNLh5HImhoHTlFObWVzaCgBMAE6ABIWCAEY-gEgCygFOAZAB0gBUB5oAcAGAQ

     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--> Si no saben como copiar y usar el link anterior en su PC en la pagina web de Meshtastic, deben clickear en los apartados del sitio en el orden numerico establecido, mostrados en la siguiente imagen:
     
<p align="center">
<img width="859" height="550" alt="image" src="https://github.com/user-attachments/assets/b9ec420b-03cc-49b4-b522-d11317fd558d" />
</p>

### ⚡Advantages
- Comes with built-in screen
- Comes with antenna
- It comes with soldering pins
- It comes with power cables for batteries (portable)
- It comes with an specific input for a GPS module (it doesn´t include a GPS module)
- Medium/small hardware size
- Peripheral customization (high)
- USB-C power input

### 📈 ¿What new features can we add?


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
- ***[Optional]*** For power we can use a `Lipo Battery`

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
        <img width="1171" height="600" alt="image" src="https://github.com/user-attachments/assets/745bc626-58d5-471b-8b8d-a894ed58c822" />
           </p>

        <p align="center">
         <img width="1598" height="837" alt="image" src="https://github.com/user-attachments/assets/07a5120c-c9c3-4f54-8823-1dcb32fe30dd" />
           </p>
           
        --> Once the correct COM port has been selected, click on `Download UF2`:
          <p align="center">
         <img width="1570" height="872" alt="image" src="https://github.com/user-attachments/assets/998a0114-7e0a-4791-bbb7-626decdafb11" />
           </p>
        --> Finally, once this is done, a file will be downloaded. Copy this file to the folder created by the Meshtastic device when you connect it to your PC (it appears as a disk). It's normal for the transfer to take a little while and for the board to restart. And that's it! Your Meshtastic board is now flashed and ready to use and configure.

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
   
- 💽 Board settings ***(important for proper operation)***
   - This section is the same as the one above, for the Heltec t114 v2 mesh device. Therefore, if you are in Argentina, you should follow the same settings mentioned previously.
   [🔹 Heltec T114 v2 (with screen)](https://github.com/s1vax/Meshtastic/tree/main?tab=readme-ov-file#-heltec-t114-v2-with-screen) (in the `Board settings` section)


### ⚡Advantages
- Very small hardware size
- Comes with antenna
- Peripheral customization (high)
- Built-in (detachable) LoRa module
- USB-C power input

### 🎯 ¿What new features can we add?

<br>
<br>
<br>
<br>

### 🔹 Other Meshtastic models

<br>

### I hope you found it useful and entertaining. If so, leave a star ⭐ Best wishes and much success!
