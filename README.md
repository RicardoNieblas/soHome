# **soHome**

| **Project name** | soHome  |
| :- | :- |
| **Authors** | 30841 - Orlando Kevin Gurrola <br> 34715 - Caitlin Murillo Denisse Espinoza <br> 34735 - Ricardo Nieblas Cabrera  |
| **Editor** | Dr. Adán Hirales Carbajal |
| **Last update** | Sep. 27th 2023 |

## **Index**

1. [Problem statement](#problem-statement)
2. [Hardware requirements](#hardware-requirements)
3. [Hardware schematic](#hardware-schematic)
4. [Hardware layout](#hardware-layout)
5. [STM32 CubeMX parameters](#stm32-cubemx-parameters)
6. [Software components](#software-components)

### **Problem statement**

In this day and age, an increasing amount of companies try to present their own solution for automated house management as the ideal solution. Systems such as Phillips Hue (house lighting) offer a wide amount of compatibility with other systems, but are often expensive and require a lot of additional hardware to work. Other systems, such as Google Home, offer a more complete solution, but are often limited to the products of a single company, and are often not compatible with other systems.

While it's easy to get lost in a sea of products designed for home management that apparently work with each other, it's often hard to get exactly what you're expecting from every single product, let alone have them working seamlessly with each other. Now, if you happen to be a user than can accomodate to the pros and cons of a certain ecosystem, there is always a concern regarding the security of your data, as well as the possibility of it being sold to third parties.

We want to propose an alternative to all automated house management systems, with the main goal in mind to make it as easy to use as possible, as well as providing security for our users. Since our project will consist of a local machine (for the sake of our class, a microcontroller), there will be no need for an internet connection, and therefore, no need to worry about our data being sold to third parties. Additionally, since our system will be open source, users will be able to modify it to their liking, as well as being able to add new features to it.

We have plans for the future to keep adding new features to our system, to solidify our project as a product everybody can use, and to provide all documentation necessary to get the system up an running.

### **Hardware requirements**

We will provide purchase links to all these components if you intend to follow along with our project. Please do keep in mind this was developed in Mexico, so these links will be for Mexican stores. If you are from another country, you will have to look for these components in your local stores.

| Component | Quantity | Characteristics | Component |
| :- | :- | :- | :- |
| [STM32 F767ZI](https://www.st.com/en/evaluation-tools/nucleo-f767zi.html) | 1 | <li> Powerful STM microcontroller <li> Versatile development board for embedded projects <li> Supports various input/output options <li> Integrated debugging and programming tools | (pending image) |
| [Dip switch (8-positions)](https://www.steren.com.mx/switch-deslizable-dip-switch-de-8-posiciones.html) | 1 | <li> Eight-position switch for binary configuration <li> Durable and reliable design <li> Ideal for setting hardware parameters <li> Suitable for PCB mounting | (pending image) |
| [Shift register (SN74HC595N)](https://www.steren.com.mx/circuito-integrado-shift-register.html) | 2 | <li> Serial-in, parallel-out shift register <li> 8-bit data storage and output <li> Cascadable for extended output capabilities <li> Commonly used for driving multiple LEDs or digital devices | (pending image) |
| [Movement sensor (PIR)](https://www.steren.com.mx/sensor-de-movimiento-pir.html) | 2 | <li> 4m detection distance <li> Simple or continuous pulse <li> Adjustable delay  | (pending image) |

### **Hardware schematic**

<!-- pending -->

### **Hardware layout**

<!-- pending -->

### **STM32 CubeMX parameters**

<!-- pending -->

### **Software components**

<!-- pending -->


<!-- template example

- Setting up the pins
- Creating the message queue
- Reading from C4014BE Parallel input / serial output shift register
- Writing to SN54HC595 Serial input / parallel output shift register

-->