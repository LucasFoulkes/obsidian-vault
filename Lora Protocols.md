1. **LoRaWAN:** The most widely used LPWAN protocol for long-range, low-power IoT deployments, designed for large-scale network management.
2. **Custom Point-to-Point/Star Protocols:** Simple, lightweight protocols designed for direct communication between LoRa devices without complex network stacks.
3. **LoRa Mesh Networks:**
   - **Meshtastic:** An open-source, long-range mesh network protocol built on LoRa, useful for off-grid communication and situations without internet access.
   - **LoRaMesher:** A mesh networking library for LoRa, enabling multi-hop communication in decentralized IoT networks.
4. **TinyLoRa:** A minimalistic library for LoRa communication, optimized for low-power microcontrollers and sending small data packets.
5. **Sigfox:** A proprietary LPWAN technology that provides global coverage and ultra-low power communication, used as an alternative to LoRaWAN.
6. **NB-IoT (Narrowband IoT):** A cellular-based LPWAN technology offering long-range, low-power communication via existing telecom infrastructure.
7. **LTE-M:** A cellular IoT protocol providing higher data rates and lower latency than NB-IoT, useful for real-time IoT applications.
8. **RadioHead:** A versatile library that supports a range of wireless communication methods, including LoRa, enabling custom protocols for point-to-point, star, and mesh configurations.
9. **MQTT over LoRa:** A lightweight messaging protocol implemented over LoRa for publish-subscribe communication, often used in IoT.
10. **SimpleLoRa:** A basic LoRa library for point-to-point or star network communication, allowing for easy setup without complex overhead.
11. **SimpleLoRa (Arduino-Based):** A straightforward LoRa communication library designed for Arduino platforms, focusing on basic IoT tasks.
12. **ChirpStack (formerly LoRaServer):** An open-source LoRaWAN network server stack that can be used to manage LoRaWAN networks, providing support for end-to-end encryption and scalable IoT deployments.
13. **The Things Network (TTN):** An open, global LoRaWAN network that allows users to connect their LoRa devices to a cloud-based LoRaWAN backend, providing a collaborative IoT network for developers.
14. **LoRaP2P (Point-to-Point LoRa Communication):** A simple mode of communication using the basic LoRa modulation without LoRaWAN, suitable for direct communication between devices, often used in smaller projects.
15. **Arduino-LoRa Library:** A library specifically designed for Arduino projects, enabling communication over LoRa with easy-to-use functions for basic LoRa communication.
16. **Libelium LoRa Stack:** A proprietary stack developed by Libelium for its Waspmote platform, providing LoRa-based communication with extended range and reliability for industrial IoT deployments.
17. **OpenLoRa:** An open-source alternative protocol stack to LoRaWAN, designed to allow developers to implement custom IoT solutions using LoRa modulation without relying on LoRaWAN’s constraints.
18. **Contiki-NG with LoRa Support:** A popular IoT operating system that includes support for LoRa communication, enabling developers to build low-power, long-range IoT applications.

### Additional Information:
- **ChirpStack** and **The Things Network (TTN)** are particularly useful for those looking to create scalable LoRaWAN networks with backend support, while **LoRa Mesh Networks** (Meshtastic, LoRaMesher) are ideal for off-grid or distributed communication where gateways or infrastructure are unavailable.
- **RadioHead** and **SimpleLoRa** are popular in DIY and smaller IoT projects due to their simplicity and flexibility in creating custom LoRa-based communication solutions.
