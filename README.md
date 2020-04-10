# BassOwl-Lite - HiFi Stereo Bluetooth Speaker
Make your own battery-powered Bluetooth speaker with HiFi sound!

![BassOwl-Lite](https://pcbwayfile.s3-us-west-2.amazonaws.com/project/20/04/09/1954334358834.jpeg)

During my years at NXP in the Voice & Audio solution department, I had the chance to put my hands on a nice amplifier, with excellent specs and little price: TFA9879. One of my colleagues was going to leave in few months, so I decided to make a special present for him, a personalized home-made Bluetooth speaker, good-looking and battery powered... that amplifier was perfect for that scope!

BassOwl-Lite is a PCB featuring following main components with their main functionalities:
* 2x TFA9879: I2S ClassD amplifier with DSP
  * Drive 4Ohm or 8Ohm loudspeakers with up to 2.5W RMS each 
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

More details for programming LPC micro-controller and CSR Bluetooth module will follow soon
