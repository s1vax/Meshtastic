# Meshtastic Technology --> How it works? What we use? How do we start?
# 📡 Introducción a Meshtastic

[![Meshtastic](https://img.shields.io/badge/Meshtastic-C22500?style=for-the-badge&logo=maildotru)](https://meshtastic.org/)


Bienvenido a esta guía sobre **Meshtastic**. Este repositorio tiene como objetivo explicar los fundamentos de esta tecnología de comunicación descentralizada y documentar la configuración de nodos específicos.

---

## 🧐 ¿Qué es Meshtastic?

**Meshtastic** es un proyecto de código abierto (open-source) que permite crear una red de malla (mesh network) descentralizada utilizando tecnología **LoRa** (Long Range). 

A diferencia de las comunicaciones tradicionales que dependen de torres de telefonía celular o routers Wi-Fi centrales, Meshtastic permite que los dispositivos se comuniquen directamente entre sí. Es como tener una red de mensajería de texto privada y encriptada que funciona de forma completamente autónoma, sin necesidad de internet ni suscripciones a operadoras.

## 🎯 ¿Para qué se usa?

La flexibilidad de no depender de infraestructura externa hace que Meshtastic sea ideal para múltiples escenarios:

* **Comunicaciones Off-Grid:** Mantener el contacto en zonas sin cobertura celular (montañas, zonas rurales o rutas aisladas).
* **Seguridad y Privacidad:** Al contar con encriptación AES256, es utilizado por comunidades y grupos que requieren canales de comunicación seguros y auditables.
* **Casos de Emergencia:** Despliegue rápido de redes de comunicación tras desastres naturales donde la infraestructura tradicional ha caído.
* **Eventos y Coordinación:** Mantener a un equipo conectado en festivales, conferencias o grandes predios.
* **Experimentación RF:** Pruebas de telemetría, alcance de antenas y topologías de red en bandas de uso libre (como 915 MHz o 433 MHz, dependiendo de la región).

## ⚙️ ¿Cómo funciona?

El sistema se basa en dos pilares fundamentales:

1.  **Tecnología LoRa:** Utiliza modulación de radiofrecuencia de largo alcance y bajo consumo de energía. Esto permite enviar pequeños paquetes de datos (como texto o coordenadas GPS) a varios kilómetros de distancia utilizando baterías pequeñas.
2.  **Topología de Malla (Mesh):** Aquí está la magia. Cada dispositivo (nodo) en la red no solo envía y recibe sus propios mensajes, sino que actúa como un **repetidor** para los demás. Si el Nodo A quiere hablar con el Nodo C, pero están muy lejos, el mensaje puede saltar a través del Nodo B que está en el medio. Cuantos más nodos haya, más robusta y amplia se vuelve la red.

## 🚀 ¿Cómo podemos empezar?

Empezar con Meshtastic es accesible y requiere pocos componentes:

1.  **Conseguir el Hardware:** Necesitas una placa de desarrollo que integre un microcontrolador (como un ESP32 o nRF52) y un chip de radio LoRa. 
2.  **Flashear el Firmware:** Conectar la placa a la computadora e instalar el firmware oficial de Meshtastic a través de su [flasheador web](https://flasher.meshtastic.org/).
3.  **Descargar la App:** Instalar la aplicación de Meshtastic en tu smartphone (iOS o Android).
4.  **Emparejar y Configurar:** Conectar tu teléfono a la placa vía Bluetooth. Desde la app, puedes configurar tu región (frecuencia legal), establecer un nombre de usuario y empezar a enviar mensajes a la malla.

---

## 🛠️ Hardware y Configuraciones Específicas

En las siguientes secciones, profundizaremos en la configuración y optimización de dos modelos específicos, detallando sus características, ventajas y esquemas de conexión.

### 🔹 Heltec V3 / T114 v2
*(Próximamente: Descripción detallada, pinout y configuración de esta placa).*

### 🔹 Seeed Studio XIAO nRF52840
*(Próximamente: Descripción detallada, gestión de energía y configuración de esta placa).*
