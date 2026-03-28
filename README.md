# 🌐 Meshtastic Technology --> How it works? What we use? How do we start?
# 📡 Introduction to Meshtastic

<p align="center">
   
![meshtastic-banner](https://github.com/user-attachments/assets/b67f0d6d-6899-40ca-84ea-4ff4b66120cf)
</p>

 [![Meshtastic](https://img.shields.io/badge/Meshtastic-00750B?style=for-the-badge)](https://meshtastic.org/)



Welcome to this guide about ***Meshtastic***. This repository aims to explain the fundamentals of this decentralized communication technology and document the configuration of specific nodes.
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

El sistema se basa en dos pilares fundamentales:

1.  **LoRa technology:** It uses long-range, low-power radio frequency modulation. This allows small data packets (such as text or GPS coordinates) to be sent several kilometers away using small batteries.
2.  **Mesh Topology:** Here's the magic. Each device (node) in the network not only sends and receives its own messages, but also acts as a repeater for the others. If Node A wants to talk to Node C, but they are far apart, the message can hop through Node B, which is in between. The more nodes there are, the more robust and extensive the network becomes.

## 🚀 ¿How can we start? --> General Steps

Empezar con Meshtastic es accesible y requiere pocos componentes. De forma breve, los pasos para empezar a involucrarte con algun dispositivo Meshtastic consisten en lo siguiente:

1.  ***Conseguir el Hardware:*** Necesitas una placa de desarrollo que integre un microcontrolador (como un ESP32 o nRF52) y un chip de radio LoRa. 
2.  ***Flashear el Firmware:*** ⚠️ ***IMPORTANTE*** ⚠️ Antes de alimentar la placa debemos conectarle alguna antena, ya sea la que trae por defecto u otra. Una vez asegurado esto, procedemos a conectar la placa a la computadora e instalar el firmware oficial de Meshtastic a través de su [flasheador web](https://flasher.meshtastic.org/).
3.  ***Descargar la App Meshtastic:*** Instalar la aplicación de Meshtastic en tu smartphone (iOS o Android) (ver para PC).
4.  ***Emparejar y Configurar:*** Conectar tu teléfono a la placa vía Bluetooth. Desde la app, puedes configurar tu región (frecuencia legal), establecer un nombre de usuario y empezar a enviar mensajes a la malla.

---

## 🛠️ Hardware y Configuraciones Específicas

En las siguientes secciones, profundizaremos en la configuración y optimización de 2 modelos específicos de dispositivos mesh, el Heltec T114 v2 y la Seed Xiao nrf52840, detallando sus características, ventajas, esquemas de conexión, flasheos y configuraciones.

### 🔹 Heltec T114 v2 (con pantalla)

<p align="center">
<img width="214" height="99" alt="image" src="https://github.com/user-attachments/assets/8528d90b-ed64-4ae9-bb28-11259c6f82cb" />
</p>

### ❓ Como la configuramos?

- 👉 En primer lugar, podemos conseguir esta placa de dos paginas principales (de Argentina):
   - Starware (modelo sin placa GPS) --> https://tienda.starware.com.ar/producto/placa-desarrollo-lora-bt-gps-heltec-mesh-node-t114-nrf52840sx1262-v20-pantalla/
   - Starware (modelo con placa GPS) --> https://tienda.starware.com.ar/producto/kit-desarrollo-lora-bt-gps-heltec-antena-mesh-node-t114-nrf52840sx1262-v2/
   - Mercado Libre (internacional) (modelo ya armado, con carcasa 3D, sin placa GPS) --> https://www.mercadolibre.com.ar/meshtastic-tracker-t114-v2-nordic-nrf52840-sx1262-lorawa/p/MLA2068680206#polycard_client=search-desktop&search_layout=grid&position=26&type=product&tracking_id=304d39fc-bcfe-4be4-abb9-f76de48062d1&wid=MLA3055433870&sid=search
   
- 📻 Una vez adquirida la placa, vamos a realizar los pasos de inicializacion:
   - ⚠️ ***IMPORTANTE*** ⚠️ Antes de alimentar la placa por medio del puerto USB-C, debemos conectar alguna antena (ya sea la que trae por default o cualquier otra que tengamos) a su puerto LoRa. Asegurado esto, la conectamos a nuestra PC (para alimentacion y flasheo) por medio de los puertos USB 2.0 [los puertos 3.0 no son recomendados para conectar la placa debido a la generacion de interferencias]
   - Como paso siguiente, procedemos a flashear la placa a traves de su [flasheador web](https://flasher.meshtastic.org/). Este paso consiste en lo siguiente:
          
        --> Abrimos el flasheador web, y nos vamos al apartado de `Select Target Device`

   - *Paso opcional [Una vez flasheada la placa, se la puede desconectar de la PC]*  
   - Luego de eso vamos a descargar la app de Meshtastic de la PlayStore en nuestro celular, o sino, ... (ver pagina o app para PC)
   - Encedemos el bluetooth de nuestro celular (ver como es para PC)
   - En caso de haber desconectado la placa luego del flasheo, en el *Paso Opcional*, la debemos de volver a alimentar mediante el cable USB-C (podemos alimentarla esta vez, por medio de los puertos USB de nuestra PC como al inicio, por medio de una bateria portatil, o por medio de algun puerto que nos brinde 3.3 V)
   - Abrimos la app de Meshtastic y nos deberia salir en el apartado de `Connection`, nuestro dispositivo para conectar via Bluetooth
   
- ⚙️ Configuraciones de la placa ***(importante para correcto funcionamiento)***
   - Ahora en esta parte veremos como hacer funcionar el dispositivo o "nodo". Una vez que estemos conectados con el dispotivo adquirido por medio de la app de Meshtastic, en primer lugar vamos a ir al apartado de `Settings`, y entraremos a la opcion de `LoRa`. Aqui vamos a

### ⚡Ventajas
  
<br>
<br>

### 🔹 Seeed Studio XIAO nRF52840 Kit

<p align="center">
<img width="150" height="200" alt="image" src="https://github.com/user-attachments/assets/3354f50d-0bc4-4644-bf62-ac7d54137ba6" />
</p>

### ❓ Como la configuramos?

- 👉 En primer lugar, podemos conseguir esta placa de dos paginas principales (de Argentina):
   - Mercado Libre --> https://www.mercadolibre.com.ar/xiao-nrf52840--wiosx1262-kit-meshtastic-blelora-862930-m/up/MLAU3394520637#polycard_client=search-desktop&search_layout=grid&position=1&type=product&float_highlight=repurchase&tracking_id=3a7aa470-9531-405d-8084-412034cb75f7&wid=MLA1519008445&sid=search
   
- 📻 Una vez adquirida la placa, vamos a realizar los pasos de inicializacion:
   - ⚠️ ***IMPORTANTE*** ⚠️ Antes de alimentar la placa por medio del puerto USB-C, debemos conectarle alguna antena (ya sea la que trae por default o cualquier otra que tengamos) a su puerto LoRa. Asegurado esto, la conectamos a nuestra PC (para alimentacion y flasheo) por medio de los puertos USB 2.0 [los puertos 3.0 no son recomendados para conectar la placa debido a la generacion de interferencias]
   - Como paso siguiente, procedemos a flashear la placa a traves de su [flasheador web](https://flasher.meshtastic.org/). Este paso consiste en lo siguiente:
     
        --> Abrimos el flasheador web, y nos vamos al apartado de `Select Target Device`
          <p align="center">
          <img width="1902" height="836" alt="image" src="https://github.com/user-attachments/assets/f29672f0-f267-45ff-8dba-a8be2c8c7d83" />
          </p>
        --> Seleccionamos o buscamos nuestra placa, en este caso la `Seed Xiao nrf52840 Kit`:
           <p align="center">
           <img width="1901" height="896" alt="image" src="https://github.com/user-attachments/assets/23da2f63-b9a1-472c-8a28-32e6508b90d4" />
           </p>
        --> Luego, en el apartado de `Firmware` debemos seleccionar la version del mismo a descargar. Es recomendado que se escoja una version `Beta` ya que son las mas estables:
           <p align="center">
           <img width="1600" height="820" alt="image" src="https://github.com/user-attachments/assets/b208a8be-7708-401a-8fe0-17b497d2f034" />
           </p>

   - *Paso opcional [Una vez flasheada la placa, se la puede desconectar de la PC]*    
   - Luego de eso vamos a descargar la app de Meshtastic de la PlayStore en nuestro celular, o sino, ... (ver pagina o app para PC)
   - Encedemos el bluetooth de nuestro celular (ver como es para PC)
   - En caso de haber desconectado la placa luego del flasheo, en el *Paso Opcional*, la debemos de volver a alimentar mediante el cable USB-C (podemos alimentarla esta vez, por medio de los puertos USB de nuestra PC como al inicio, por medio de una bateria portatil, o por medio de algun puerto que nos brinde 3.3 V)
   - Abrimos la app de Meshtastic y nos deberia salir en el apartado de `Connection`, nuestro dispositivo para conectar via Bluetooth. Generalmente sale con un nombre estilo: *"Meshtastic_XXXX"*
   
- ⚙️ Configuraciones de la placa y comunicacion ***(importante para correcto funcionamiento)***
   - Ahora en esta parte veremos como hacer funcionar el dispositivo o "nodo". Una vez que estemos conectados con el dispotivo adquirido por medio de la app de Meshtastic, en primer lugar vamos a ir al apartado de `Settings`, y entraremos a la opcion de `LoRa`. Aqui vamos a 

### ⚡Ventajas
