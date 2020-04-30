# BassOwl-Lite - HiFi Stereo Bluetooth Speaker
### Make your own battery-powered Bluetooth speaker with HiFi sound!

#### Project description

![BassOwl-Lite](https://pcbwayfile.s3-us-west-2.amazonaws.com/project/20/04/09/1954334358834.jpeg)

During my years at NXP in the Voice & Audio solution department, I had the chance to put my hands on a nice amplifier, with excellent specs and little price: TFA9879. One of my colleagues was going to leave in few months, so I decided to make a special present for him, a personalized home-made Bluetooth speaker, good-looking and battery powered... that amplifier was perfect for that scope!

BassOwl-Lite is a PCB featuring following main components and their main functionalities:
* 2x TFA9879: I2S ClassD amplifier with DSP
  * Drive 4Ohm or 8Ohm loudspeakers with up to 2.5W RMS output power each 
* 1x BTM625: Bluetooth module with CSRA64215 chip from Qualcomm
  * Acquiring signal from the microphone
  * Driving LEDs
  * Handle user buttons (play/pause, next/vol+, prev/vol-)
  * Sending I2S digital audio stream to the TFA9879 amplifiers
* 1x LPC1343: Microcontroller with USB bootloader
  * Initialize TFA9879 amplifiers with I2C commands
  * Apply DSP settings for audio processing (equalizer, dinamic-range compressor, etc.)

BassOwl Lite requires a DC input voltage to work. It can provided from an AC/DC converter or from a battery.
Two different voltage inputs can be use for powering either from a 3.6V-5.5V source or from a 6V-9V source. Any input voltage above 5V will maximize the output power.

If a 3.7V LiPo battery is used (selecting a 3000mAh one music playback can last for several hours), it is recommended to add an additional module for charging the battery and providing 5.5V input to the BassOwl-Lite PCB.

![LiPo charging module with DC-DC converter](https://pcbwayfile.s3-us-west-2.amazonaws.com/project/20/04/09/2118250916703.png)

  
  
#### LPC micro-controller programming via USB bootloader

A compiled version of the LPC1343 code that initialize the TFA9879 amplifiers is included in the [repository](https://github.com/Darmur/bassowl-lite/tree/master/lpc-firmware). A BlinkLed compiled binary is also included, for testing purpose.

Source code and instructions for building and adapting the code will be provided later.

Flashing the compiled code in the LPC1343 is pretty easy:

1) Insert jumper on JP2 to enable bootloader mode
2) Connect to a PC with USB cable
3) Press reset button: the device will be recognised as an external drive with label "CRP DISABLD"
4) Delete the only file "firmware.bin" from the device
5) Copy/paste the provided firmware "BassOwl-Lite_FW_v0.1.3.bin" in the drive
6) Remove jumper from JP2
7) Press reset button

LED D5 should turn on if BassOwl released firmware is loaded properly.



#### Setting CSRA64215 for buttons, LEDs and microphone

[CSRA64215](https://www.tinyosshop.com/datasheet/CSRA64215%20QFN%20Data%20Sheet.pdf) can be updated via SPI interface using cheap (clone) programmers from Aliexpress or Ebay, I got mine for less than 15 USD.

Closing JP1 with a jumper will enable SPI mode for updating all available parameters, including GPIOs configuration, microphone gain and Bluetooth name. Yes, you can set the one you prefer, very effective for a personalised gift!

For programming CSRA64215 modules, a proprietary tool from CSR is needed: **CSRA64xxx and CSRA63xxx Tools v2**
If you have problems updating a module with ROM v15, please have a look to this thread on [diyaudio]
(https://www.diyaudio.com/forums/digital-source/323164-program-csra64215-rom-15-csra64xxx-v2.html)

In the [repository](https://github.com/Darmur/bassowl-lite/tree/master/bt-settings) it is included a configuration file for ROM V15 (any recent CSRA64215 has that version).
The configuration file will configure GPIOs to match buttons and LEDs assignment of BassOwl-Lite PCB. It will also set I2S properly and the gain of the microphone. Just load the file with CSRA64xxx and CSRA63xxx Tools v2 and write new settings on the device.

Don't forget to remove jumper from JP1 after setting up your module.
