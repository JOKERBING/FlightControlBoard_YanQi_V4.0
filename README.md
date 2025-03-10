# YanQi Flight Control Board V4.0

**3 x IMU & Baro & 4 x ESC small size PX4 for MAV research.**

<div align=center><img src="Pictures/20250310.png" width="800"></div>

## Physical

- Mounting: 20 x 35 mm, Φ 2 mm
- Dimensions: 24 x 39 x 6 mm
- Weight: 4.9 g

## Specifications

- MCU: STM32H743VIH6, 480MHz, 2MB Flash
- IMU: BMI088 + BMI088 + ICM42688P
- Baro: BMP388
- ESC: 4 x Bluejay
- MicroSD Card Slot
- 7 x UART
- 4 x PWM (DShot)
- 1 x External I2C
- 1 x External SPI
- 1 x SRGBLED neopixel
- 1 x SWD
- 2 x ADC (Battery Voltage, Current)
- 2 x AUX
- USB Type-C
- BEC 9V 3A output
- BEC 5V 3A output

## UART Mapping

<style>

.center
{
  width: auto;
  display: table;
  margin-left: auto;
  margin-right: auto;
}

</style>

<div class="center">

| UART   | TTY | SerialName | Suggest Funcion | DMA |
| :----: | :-: | :--------: | :-------------: | :-: |
| USART1 | /dev/ttyS0 | GPS1 |                       | OFF |
| USART2 | /dev/ttyS1 | GPS2 | WIFI module (ESP8266) | ON  |
| USART3 | /dev/ttyS2 | TEL1 |         DEBUG         | OFF |
| UART4  | /dev/ttyS3 | TEL2 |      Offboard PC      | ON  |
| UART5  | /dev/ttyS4 |  RC  |  Receiver BlackSheep  | ON  |
| USART6 | /dev/ttyS5 | TEL3 |                       | OFF |
| UART7  | /dev/ttyS6 | TEL4 | Optical Flow (MTF-01) | ON  |

</div>

## Debug Port

USART3 RX and TX are configured for use as the **System Console**.

## Getting Start

### Compile Locally

Follow the PX4 standard approach.

#### Bootloader:

```shell
make UCAS_YanQiH7_bootloader
```

#### Firmware:

```shell
make UCAS_YanQiH7_default
```

### Burn Bootloader & Firmware

#### Bootloader:

**Method 1：**

 To enter DFU mode, pull up BOOT0 while connecting the USB cable to your computer.

```shell
make UCAS_YanQiH7_bootloader upload
```

**Method 2：**

 To enter DFU mode, pull up BOOT0 while connecting the USB cable to your computer.

```shell
dfu-util -a 0 --dfuse-address 0x08000000 -D ./build/UCAS_YanQiH7_bootloader/UCAS_YanQiH7_bootloader.bin
```

If the burning tool is not installed, install the dfu util burning toolkit first.

```
sudo apt install dfu-util
```

#### Firmware:

**Method 1：**

```shell
make UCAS_YanQiH7_default upload
```

Connect the flight controller directly to your computer via USB.

The firmware will then proceed through a number of upgrade steps (downloading new firmware, erasing old firmware etc.). Each step is printed to the screen.

Once the firmware has completed loading, the device/vehicle will reboot and reconnect.

**Method 2：**

Start QGroundControl and connect the vehicle.

Select **"Q" icon** > **Vehicle Setup** > **Firmware** (sidebar) to open Firmware Setup.

Connect the flight controller directly to your computer via USB.

Check **Advanced settings** and select the version from the dropdown list.

Select the **Custom Firmware file...** option to install the custom firmware for the flight controller (autodetected).

Click the **OK** button to start the update.

The firmware will then proceed through a number of upgrade steps (downloading new firmware, erasing old firmware etc.). Each step is printed to the screen and overall progress is displayed on a progress bar.

Once the firmware has completed loading, the device/vehicle will reboot and reconnect.

## Setting Up PX4 Configuration Settings

### Power

### MAVLink

### Receiver



## TODO

- [ ]  stable SRGBLED driver based on srgbled_dma
