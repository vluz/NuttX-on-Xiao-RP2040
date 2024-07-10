# NuttX on Xiao RP2040

This repo contains updated instructions on how to compile and install      
Apache NuttX real-time operating system into a Seeed Studio Xiao RP2040       
on Debian 12.6 with serial over USB.       

## Links

Apache NuttX      
https://nuttx.apache.org/docs/latest/index.html       
https://github.com/apache/nuttx

Seeed Studio Xiao RP2040       
https://www.seeedstudio.com/XIAO-RP2040-v1-0-p-5026.html      
https://wiki.seeedstudio.com/XIAO-RP2040/

Mauser product link (Portugal)      
https://mauser.pt/catalog/product_info.php?products_id=095-0493

## Install

Modified from https://nuttx.apache.org/docs/latest/platforms/arm/rp2040/boards/seeed-xiao-rp2040/index.html

### 0. Get dependencies
   
  `sudo apt-get install kconfig-frontends g++-arm-linux-gnueabi g++-arm-linux-gnueabihf`

### 1. Download Raspberry Pi Pico SDK and update submodule cyw43-driver

  `git clone -b 1.4.0 https://github.com/raspberrypi/pico-sdk.git`
  
  `cd pico-sdk`
  
  `git submodule update --init --recursive lib/cyw43-driver`

### 2. Set PICO_SDK_PATH environment variable

  `export PICO_SDK_PATH=<absolute_path_to_pico-sdk_directory>`

### 3. Configure and build NuttX

  `git clone https://github.com/apache/nuttx.git nuttx`
  
  `git clone https://github.com/apache/nuttx-apps.git apps`
  
  `cd nuttx`
  
  `make distclean`
  
  `./tools/configure.sh seeed-xiao-rp2040:usbnsh`
  
  `make V=1`

  _Alternatively you can download the `nuttx.uf2` from this repo._

### 4. Connect Seeed Studio Xiao RP2040 board to USB port while pressing BOOTSEL button.
   The board will be detected as USB Mass Storage Device.      
   Then copy `nuttx.uf2` into the device.

### 5. To access the console, open a terminal app and connect to the board com port at:      
   115200 bits per second      
   8 data bits      
   No parity      
   1 stop bit     
   No flow control      

   If no `nsh>` prompt, press enter and you should get a prompt

   Try `uname -a`

   ```
   nsh> uname -a
   NuttX 12.5.1 881f749777 Jul 10 2024 19:03:48 arm seeed-xiao-rp2040
   ```

  You now have a functional NuttX installed on your Xiao RP2040

  Enter `help` for help

  
  ## Happy Hacking!

