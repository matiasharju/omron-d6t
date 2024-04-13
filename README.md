A simple python script to read temperatures from Omron D6T thermal MEMS sensor

This script reads temperatures from D6T 44L sensor with 16 pixels, but can easily be modified for other sensor models. By the way, no error checks in this script...

Tested on Raspberry 3 B+ with Python 3.9. 

The official Omron D6T user manual can be found here: https://omronfs.omron.com/en_US/ecb/products/pdf/en_D6T_users_manual.pdf

Pigpio module needs to be started in boot, e.g. with this:
`sudo systemctl enable pigpiod`

I think the I2C bus baudrate must be slowed down a bit for the sensor to work nicely. I have done that to the two extra I2C buses I've created for my sensors. That was done by editing `boot/config.txt` and 
- uncommenting `dtparam=i2c_arm=on`
- adding the extra buses with
```
dtoverlay=i2c-gpio,bus=4,i2c_gpio_delay_us=4,i2c_gpio_sda=17,i2c_gpio_scl=27
dtoverlay=i2c-gpio,bus=3,i2c_gpio_delay_us=4,i2c_gpio_sda=5,i2c_gpio_scl=6
```

To check that sensor is detected in the right bus and verify the sensor's address:
`sudo i2cdetect -y [port number]`

Remember to use a level shifter when connecting a D6T sensor (5V) to Raspberry (pin voltage 3.3V). Otherwise the I2C communication won't work.   

Thanks to Greg Griffes (https://forums.raspberrypi.com/viewtopic.php?t=96752) for his code I've recycled.
