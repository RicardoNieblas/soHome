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

Automated house management systems are becoming increasingly popular, with many companies offering their own solutions. However, these systems can be expensive, require a lot of additional hardware, and are often limited to the products of a single company.

In this project, we propose an alternative to these systems, with the main goal in mind to make it as easy to use as possible, as well as providing security for our users. Our system will consist of a local machine, which means that there will be no need for an internet connection. Additionally, our system will be open source, which means that users will be able to modify it to their liking, as well as being able to add new features to it.

We have plans for the future to keep adding new features to our system, to solidify our project as a product that everybody can use, and to provide all documentation necessary to get the system up and running.

### **Hardware requirements**

We will provide purchase links to all these components if you intend to follow along with our project. Please do keep in mind this was developed in Mexico, so these links will be for Mexican stores. If you are from another country, you will have to look for these components in your local stores.

| Component                                                                        | Quantity | Characteristics | Component |
|:---------------------------------------------------------------------------------| :- | :- | :- |
| [STM32 F767ZI](https://www.st.com/en/evaluation-tools/nucleo-f767zi.html)        | 1 | <li> Powerful STM microcontroller <li> Versatile development board for embedded projects <li> Supports various input/output options <li> Integrated debugging and programming tools | (pending image) |
| [Movement sensor (PIR)](https://www.steren.com.mx/sensor-de-movimiento-pir.html) | 2 | <li> 4m detection distance <li> Simple or continuous pulse <li> Adjustable delay  | (pending image) |
| [Buzzer]()       | 2 |  | (pending image) |

### **Hardware schematic**



### **Hardware layout**



### **STM32 CubeMX parameters**



### **Software components**

<!-- template example

- Setting up the pins
- Creating the message queue
- Reading from C4014BE Parallel input / serial output shift register
- Writing to SN54HC595 Serial input / parallel output shift register

-->

### **Components**

#### **Shift Register 7495**

Tutorial from [Arduino Docs](https://docs.arduino.cc/tutorials/communication/guide-to-shift-out?queryID=b098cb175fcc8c0ed12b788bb6785914#shifting-out--the-595-chip)

- Serial In / Parallel Out
- It's used to expand output capabilities
- Connections
  - DS (pin 14) to pin 11 (blue)
  - SH_CP (pin 11) to pin 12 (yellow)
  - ST_CP (pin 12) to pin 8 (green)
- Sample code: count from 0 to 255
```
// pin connected to ST_CP of 74HC595
int latchPin = 8;

// pin connected to SH_CP of 74HC595
int clockPin = 12;

// pin connected to DS of 74HC595
int dataPin = 11;

void setup()
{
  // set pins to output so you can control the shift register
  pinMode(latchPin, OUTPUT);
  pinMode(clockPin, OUTPUT);
  pinMode(dataPin, OUTPUT);
}

void loop()
{
  // count from 0 to 255 and display the number on the LEDs
  for (int numberToDisplay = 0; numberToDisplay < 256; numberToDisplay++)
  {
    // take the latchPin low so the LEDs don't change while you're sending in bits:
    digitalWrite(latchPin, LOW);
    // shift out the bits:
    shiftOut(dataPin, clockPin, MSBFIRST, numberToDisplay);
    // take the latch pin high so the LEDs will light up:
    digitalWrite(latchPin, HIGH);
    // pause before next value:
    delay(500);
  }
}
```

**Translating to STM32 F767ZI**

```
void ShiftRegisterTask(void *pvParameters) {
    // Initialize your GPIO pins (dataPin, clockPin, and latchPin) here.

    while (1) {
        // Assuming MSBFIRST
        for (int i = 7; i >= 0; i--) {
            // Shift out the data one bit at a time
            uint8_t bit = (numberToDisplay >> i) & 0x01;

            // Write the bit to dataPin
            HAL_GPIO_WritePin(GPIOx, dataPin, bit);

            // Pulse the clock pin
            HAL_GPIO_WritePin(GPIOx, clockPin, GPIO_PIN_SET);
            HAL_GPIO_WritePin(GPIOx, clockPin, GPIO_PIN_RESET);
        }

        // Pulse the latch pin to update the shift register's output
        HAL_GPIO_WritePin(GPIOx, latchPin, GPIO_PIN_SET);
        HAL_GPIO_WritePin(GPIOx, latchPin, GPIO_PIN_RESET);

        // Do any RTOS-specific task handling or delay as needed.
        vTaskDelay(pdMS_TO_TICKS(100)); // Example: Delay for 100 ms
    }
}

int main() {
    // Initialize your STM32 peripherals, FreeRTOS, and tasks here.

    // Create the ShiftRegisterTask
    xTaskCreate(ShiftRegisterTask, "ShiftRegisterTask", configMINIMAL_STACK_SIZE, NULL, tskIDLE_PRIORITY + 1, NULL);

    // Start the FreeRTOS scheduler
    vTaskStartScheduler();

    // You should not reach here
    while (1);
}

```

MSBFIRST and LSBFIRST are bit order options commonly used when shifting data out to shift registers:

- MSBFIRST (Most Significant Bit First): In this bit order, the most significant bit (the leftmost bit) is shifted out first, followed by the less significant bits.
- LSBFIRST (Least Significant Bit First): In this bit order, the least significant bit (the rightmost bit) is shifted out first.

These term is also usually referred to as Little Endian and Big Endian.

#### **Shift Register 7495**

**Sample code**

```
void PIRSensorTask(void *pvParameters) {
    // Initialize your GPIO pin for the PIR sensor input
    GPIO_InitTypeDef GPIO_InitStruct;

    __HAL_RCC_GPIOx_CLK_ENABLE(); // Replace x with the appropriate GPIO port
    GPIO_InitStruct.Pin = GPIO_PIN_x; // Replace x with the specific GPIO pin
    GPIO_InitStruct.Mode = GPIO_MODE_INPUT;
    GPIO_InitStruct.Pull = GPIO_NOPULL;
    HAL_GPIO_Init(GPIOx, &GPIO_InitStruct);

    while (1) {
        // Read the PIR sensor input
        uint8_t motionDetected = HAL_GPIO_ReadPin(GPIOx, GPIO_PIN_x); // Replace x with the specific GPIO pin

        if (motionDetected) {
            // Motion detected, take action (e.g., turn on a light, set a flag, etc.)
            // Add your code to perform the desired action here.
        }

        // Delay for a short interval to avoid rapid triggering
        vTaskDelay(pdMS_TO_TICKS(100)); // Example: Delay for 100 ms
    }
}

int main() {
    // Initialize your STM32 peripherals, FreeRTOS, and tasks here.

    // Create the PIRSensorTask
    xTaskCreate(PIRSensorTask, "PIRSensorTask", configMINIMAL_STACK_SIZE, NULL, tskIDLE_PRIORITY + 1, NULL);

    // Start the FreeRTOS scheduler
    vTaskStartScheduler();

    // You should not reach here
    while (1);
}

```
