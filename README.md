A simple python script to read temperatures from Omron D6T thermal MEMS sensor

This script reads temperatures from D6T 44L sensor with 16 pixels, but can easily be modified for other sensor models. By the way, no error checks in this script...

Tested on Raspberry 3 B+ with Python 3.9. 

The official Omron D6T user manual can be found here: https://omronfs.omron.com/en_US/ecb/products/pdf/en_D6T_users_manual.pdf

Pigpio module needs to be started in boot, e.g. with this:
`sudo systemctl enable pigpiod`

If more I2C-buses are needed, edit `boot/config.txt` with these changes:

```
#Uncomment some or all of these to enable the optional hardware interfaces
dtparam=i2c_arm=on
#dtparam=i2s=on
#dtparam=spi=on

#Open other i2c bus(es) and change delay (thus affecting baudrate)
dtoverlay=i2c-gpio,bus=4,i2c_gpio_delay_us=4,i2c_gpio_sda=17,i2c_gpio_scl=27
dtoverlay=i2c-gpio,bus=3,i2c_gpio_delay_us=4,i2c_gpio_sda=5,i2c_gpio_scl=6
```
Notice that the baudrate must be slowed down a bit, e.g.: `us=4`

To check that the sensor is detected:
`sudo i2cdetect -y [port number]`

Remember to use a level shifter when connecting D6T (5V) to Raspberry (pin voltage 3.3V). Otherwise the I2C communication won't work.   

Thanks to Greg Griffes (https://forums.raspberrypi.com/viewtopic.php?t=96752) and avninja (https://github.com/avninja/omrond6t/blob/master/omrond6t.py) for their code!
