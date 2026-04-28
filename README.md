# 🌐 Meshtastic Technology --> How it works? What we use? How do we start?
# 📡 Introduction to Meshtastic

<p align="center">
   
<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/a6218dca-af3a-496f-8577-7fef0b3c06f1" />

</p>

  [![Meshtastic](https://img.shields.io/badge/Meshtastic_Website-00750B?style=for-the-badge)](https://meshtastic.org/) 



## Welcome to this guide about ***Meshtastic***. This repository aims to explain the fundamentals of this decentralized communication technology and document the configuration of specific nodes.

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
- `MQQT` (Message Queuing Telemetry Transport): This is a bridge between the radio world and the internet. If one node in a mesh is connected to a phone with internet or a Wi-Fi gateway, it can push the local mesh traffic to an MQTT Broker. As result, you can talk to a mesh network in another city or country as if they were right next to you, effectively linking "islands" of radio users together via the web.

<br>

## 🚀 ¿How can we start? --> General Steps

Getting started with Meshtastic is accessible and requires few components. In short, the steps to begin using any Meshtastic device are as follows:

1.  ***Get the Hardware:*** You need a development board that integrates a microcontroller (such as an ESP32 or nRF52) and a LoRa radio chip.
2.  ***Flash the Firmware:*** ⚠️ ***IMPORTANT*** ⚠️ Before powering the board, we must connect an antenna, either the one that comes on the package or another one. Once this is secured, we proceed to connect the board to the computer and install the official Meshtastic firmware using their web flasher (https://flasher.meshtastic.org/).
3.  ***Use the Meshtastic App´s:*** Install the Meshtastic app on your smartphone (iOS or Android), or visit the Meshtastic setup website for PC (https://client.meshtastic.org).
4.  ***Pair and Configure:*** Connect your Meshtastic device to your phone or your PC via Bluetooth, Network or Serial. From the app/website, you can configure your region (legal frequency), set a username, as others settings that we are going to look up, and then, we can start sending messages to the mesh network.

<br>

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

     Solar Panel Connection diagram
   
   - `Baterías LiPo/Li-ion`: It supports 3.7V cells. It is possible to scale from the standard 800-1100mAh to 18650 or 21700 cells of 5000mAh for extended runtime.
   
        - `Circuito de Protección (PCM/BMS) para baterias LiPo` (In some cases): Many LiPo batteries come "bare." They need a small circuit board at the tip with the DW01 and 8205A chips.
Function: Cuts off power if the voltage drops below 2.4V (preventing the battery from permanently failing) or if there is a short circuit.

        - `Termistor NTC` (Optional but recommended): If the node will be in the sun (inside a box or structure), the heat can be dangerous. Some chargers have a "TEMP" pin that, when connected to a thermistor attached to the battery, stops charging if the temperature exceeds 45°C - 50°C.
        
        - `Conectores JST-PH` (2.0mm) o `SH` (1.25mm): Ensure the polarity is correct. Important note: The red/black wire standard on Chinese batteries is sometimes reversed compared to what Heltec or Seeed boards require. Measure with a multimeter before plugging in.
   
- ***Sensores via I2C:***
   - `BME280 / BME680`: It measures temperature, humidity, atmospheric pressure, and (in the case of the 680) air quality. It is ideal for remote weather stations.
   - `INA219`: Útil si planeas monitorear el voltaje y consumo de corriente, especialmente en instalaciones solares.
   - `SHT31`: Una alternativa de alta precisión para temperatura y humedad.
   
- ***Mejoras de RF (Antenas y Conectores):***
La antena de "resorte" que suele venir de fábrica es limitada. Para mejorar el alcance:
   - `Pigtail IPEX (U.FL) a SMA`: Permite usar antenas externas de mayor ganancia.
   - `Antenas Dipolo o Fibra de Vidrio`: Si el nodo será fijo (Router), una antena de 3dBi a 5dBi optimizada para la frecuencia de tu zona (típicamente 915MHz en Argentina) marcará una diferencia notable en el radio de cobertura.
   
- ***Interfaz de Usuario y Alertas:***
   - `Buzzer Pasivo`: Se puede configurar un buzzer para recibir alertas sonoras cuando llegue un mensaje o un nodo nuevo se una a la red.
   - `Botones Adicionales`: Aunque trae dos botones físicos, se puede mapear otros pines GPIO para funciones de navegación en la pantalla TFT de 1.14".

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
Es una pieza clave para agregar periféricos sin tener que soldar:
    - `Pantalla OLED (0.96")`: Una pantalla OLED se puede agregar a la placa Xiao nrf52840 sin la necesidad de una Xiao Expansion Board, pero cabe destacar que en esta ya viene con un zócalo integrado para conectar una pantalla SSD1306, fundamental para ver mensajes y estado del nodo.
    - `RTC (Reloj en Tiempo Real)`: Incluye un chip PCF8563 que permite mantener la hora exacta incluso si el dispositivo se reinicia o pierde conexión.
    - `Slot MicroSD`: Vital si planeas hacer Data Logging (registrar posiciones GPS o lecturas de sensores durante un trayecto o vuelo).
    
- ***GPS Module:*** En los dispositivos Meshtastic podemos utilizar como GPS a nuestros dispositivos conectados (celular o PC). Sin embargo, existe la posibilidad de aplcarles su propio sistema de geolocalizacion para que no dependan de otro dispositivo al momento de hacerlos "portables". Es por ello que se les puede agregar un `GPS Module` para identificar sus coordenadas y otros datos. En el caso de la `Seed Studio Xiao nrf52840 Kit` requiere un módulo Grove GPS (`Grove - GPS Air530Z`, de alta precisión y bajo consumo, ideal para que el nodo transmita su ubicación) o soldar a pines UART (TX/RX), por ejemplo al `L76K GNSS`.
- ***Sistemas de Energia:***
    - `Paneles solares + bateria`: Para estos microcontroladores, lo ideal es un panel de 5V a 6V. Entre 1W y 2W es suficiente para mantener un nodo nRF52840 encendido 24/7. Monocristalino (rígido) o Pet/ETFE (flexible para aerodinámica o bajo peso). Para esto requiere de un `Controlador de Carga Solar (IC)`, ya que no se puede conectar el panel directo a la batería, para esto se necesita un chip que gestione el protocolo de carga.
Recomendado: CN3065. Es el estándar para solar "mini" porque soporta las fluctuaciones de corriente del sol mucho mejor que un TP4056 común.

       Tambien se necesitaria un `Diodo Schottky` (como un 1N5817). Este se coloca entre el panel y el cargador. Evita el "flujo inverso", es decir, que la batería intente "alimentar" al panel solar durante la noche, lo cual la agotaría.

       Y ademas, `capacitores electrolíticos`. Se coloca uno (de 100µF o 470µF) en la entrada del cargador solar ayuda a estabilizar el voltaje cuando pasan nubes rápidas.

        <p align="center">
       <img width="1280" height="720" alt="Conexion de baterias en parte trasera" src="https://github.com/user-attachments/assets/f408ce6e-bf67-434a-84ff-1ad43b9bb5af" />
       </p>
       
    - `Baterías LiPo/Li-ion`: Para las baterías, el requerimiento principal es que sean 1S (una sola celda) con un voltaje nominal de 3.7V. Con capacidad: Desde 400mAh (vuelo/compacto) hasta 5000mAh (fijo/estación).

        - `Circuito de Protección (PCM/BMS) para baterias LiPo` (En algunos casos): Muchas LiPo vienen "desnudas". Se necesita que tengan una pequeña plaquita en la punta con los chips DW01 y 8205A.
             Función: Corta la energía si el voltaje baja de 2.4V (evita que la batería muera permanentemente) o si hay un cortocircuito.

        - `Termistor NTC` (Opcional pero recomendado): Si el nodo va a estar al sol (dentro de una caja o estructura), el calor puede ser peligroso. Algunos cargadores tienen un pin "TEMP" que, conectado a un termistor pegado a la batería, detiene la carga si la temperatura supera los 45°C - 50°C.

        - `Conectores JST-PH` (2.0mm) o `SH` (1.25mm): Asegurarse de que la polaridad sea la correcta. Dato vital: El estándar de cables rojo/negro en baterías chinas a veces viene invertido respecto a lo que esperan las placas Heltec o Seeed. Medir con multímetro antes de enchufar.
    
- ***Sensores Grove (Plug & Play):***
El ecosistema de Seeed utiliza el estándar Grove. Al tener conectores dedicados en la base, se pueden agregar:
    - `Barómetro/Altímetro (BMP280 / MS5607)`: Crucial para medir altitud con precisión si el nodo va a estar en movimiento vertical o en aplicaciones donde la presión atmosférica es un dato clave.
    - `Acelerómetro/Giroscopio (ICM20689)`: Si se usa la versión "Sense" del XIAO, ya viene uno integrado, pero uno externo de mayor rango (como un ADXL345) es útil para medir impactos o vibraciones fuertes.
- ***Mejoras de RF (Antenas y Conectores):***
Al no tener una antena integrada de gran alcance, el uso de un pigtail U.FL a SMA es obligatorio para conectar:
    - `Antenas Cloverleaf`: Si el nodo va a estar rotando o cambiando de orientación constantemente, estas antenas minimizan la pérdida de señal por polarización.
    - `Antenas de muelle (Spring)`: Para mantener el tamaño lo más pequeño posible en dispositivos "wearables" (portables).
    - `Antena Modem Gsm Gprs 2dbi U.fl Sma Cable 15cm`
- ***Interfaz de Usuario y Alertas:***
   - `Buzzer Pasivo`: Se puede configurar un buzzer para recibir alertas sonoras cuando llegue un mensaje o un nodo nuevo se una a la red.
   - `Botones Adicionales`: Se puede mapear otros pines GPIO para funciones de navegación en la pantalla.

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

👉 ***Pueden ver mas dispositivos compatibles con Meshtastic (como los de abajo) en:*** https://meshtastic.org/docs/hardware/devices/

<br>

- `Heltec WiFi LoRa 32 (V3)`
   - Procesador: ESP32-S3.
   - Pantalla: OLED de 0.96 pulgadas integrada.
   - Características: Incluye carga de batería LiPo y Wi-Fi/Bluetooth.
   - Punto débil: Consumo de energía moderado (no es el mejor para baterías pequeñas).

<br>

- `Lilygo T-Beam (V1.1 / V1.2)`
El "clásico" todo-en-uno que definió los inicios de la red.
   - Procesador: ESP32.
   - GPS: Módulo Neo-6M o Neo-M8N integrado.
   - Alimentación: Incluye un zócalo para batería 18650 en la parte posterior.
   - Características: Muy robusto y fácil de llevar en la mochila sin cajas externas complejas.

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
Considerado el "estándar de oro" para nodos serios y estaciones solares.
   - Procesador: nRF52840 (Ultra bajo consumo).
   - Modularidad: Diseño tipo "LEGO"; puedes añadir sensores de clima, GPS o pantallas mediante módulos.
   - Características: Consume una fracción de la energía de los modelos ESP32.

<br>

- `Lilygo T-Echo`
   - Procesador: nRF52840.
   - Pantalla: E-Ink (Tinta electrónica) de 1.54 pulgadas, visible bajo el sol.
   - Características: Incluye caja protectora, GPS y batería interna de fábrica.

<br>

- `Station G1 (Nano G1 Explorer)`
   - Procesador: ESP32.
   - Carcasa: Aleación de aluminio robusta.
   - Características: Conector SMA para antena externa de alta ganancia y puerto USB-C frontal.

<br>

## ⚖️ Disclaimer
No soy responsable de los links compartidos en este repositorio frente alguna problematica con los distribuidores de los mismos. Abrirlos y utilizarlos bajo su propio cuidado y responsabilidad. 

Solo comparto los links que yo he utilizado bajo mi propia responsabilidad y supervision durante la realizacion de proyectos con Meshtastic.

<br>

### I hope you found it useful and entertaining. If so, leave a star ⭐ Best wishes and much success!
