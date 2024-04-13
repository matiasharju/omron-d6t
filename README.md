# omron-d6t

Reads temperatures from an Omron D6T 44L sensor (16 pixels).

[Add a link to the Omron manual]

Pigpio module needs to be started in boot with this:
`sudo systemctl enable pigpiod`

If more I2C-buses are needed, edit `boot/config.txt` with these changes:

```
#Uncomment some or all of these to enable the optional hardware interfaces
dtparam=i2c_arm=on
#dtparam=i2s=on
#dtparam=spi=on

#open other i2c bus(es), change delay (thus affecting baudrate)
dtoverlay=i2c-gpio,bus=4,i2c_gpio_delay_us=4,i2c_gpio_sda=17,i2c_gpio_scl=27
dtoverlay=i2c-gpio,bus=3,i2c_gpio_delay_us=4,i2c_gpio_sda=5,i2c_gpio_scl=6
```
Notice that the baudrate must be slowed down a bit, e.g.: `us=4`

Connect the sensor to the right I2C connectors and check that it is detecetd:
`sudo i2cdetect -y [port number]`
