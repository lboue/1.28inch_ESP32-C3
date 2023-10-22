# 1.28inch_ESP32-C3
1.28inch_ESP32-C3

## Hardware
ESP32 LVGL for Arduino Development Board 1.28 Inch 240*240 IPS Smart Display Screen LCD TFT Module WiFi & Bluetooth with Touch
* main control is a Single Core MCU, ESP32-C3-MINI-1U 
* integrated WI-FI and Bluetooth functions, the main
* frequency can reach 160MHz, 400KB SRAM, 384KB ROM,
* Flash size is 4MB
* display resolution is 240*240 IPS display
* capacitive touch.
* includes LCD display screen, backlight control circuit,IO port interface, this module supports development in arduino IDE, ESP IDE, Micropython and Mixly

![image](https://github.com/lboue/1.28inch_ESP32-C3/assets/938089/67d7e8a0-ca0c-4d22-9aca-f573492b956b)


* Brand: [Shenzhen Jingcai Intelligent Co., Ltd](https://www.displaysmodule.com)
* Specs: [1.28 Inch ESP32 Black shell CTP Display Module 240x240 Tft Lcd Screen Module LVGL Development Board](https://www.displaysmodule.com/sale-37538321-1-28-inch-esp32-black-shell-ctp-display-module-240x240-tft-lcd-screen-module-lvgl-development-board.html)
 * Store
   * [Aliexpress](https://www.aliexpress.com/item/1005005561489118.html)

## Demo
https://www.displaysmodule.com/video/ecerplay.html

## Source code
Source code archive 1.28inch_ESP32-2432S032.zip can be found [here](http://pan.jczn1688.com/1/ESP32%20module): 

## Dump

```
python esptool.py -b 115200 --port COM21 read_flash 0x00000 0x400000 flash_4M.bin
```



## ESPHome

```
pip install esphomeflasher
esphomeflasher your_esphome_firmware.bin --bootloader bootloader_qio_80m.bin
```


ESP32 firmware is split into 4 different files. When these files are installed using the command-line tool esptool, it will patch flash frequency, flash size and flash mode to match the target device. ESP Web Tools is not able to do this on the fly, so you will need to use esptool to create the single binary file and use that with ESP Web Tools.

Create a single binary using esptool with the following command:

```
esptool --chip esp32 merge_bin \
  -o merged-firmware.bin \
  --flash_mode dio \
  --flash_freq 40m \
  --flash_size 4MB \
  0x1000 bootloader.bin \
  0x8000 partitions.bin \
  0xe000 boot.bin \
  0x10000 your_app.bin
```
If your memory type is opi_opi or opi_qspi, set your flash mode to be dout. Else, if your flash mode is qio or qout, override your flash mode to be dio.



https://github.com/espressif/arduino-esp32/blob/b588aff6d6edfdc764c2d687a3f1b7242e96b176/tools/sdk/bin/bootloader_qio_80m.bin
