py-gaugette
===========

A library for interfacing with the ssd1306 oled with the raspberry pi.

Original author: [Guy Carpenter](https://github.com/guyc/py-gaugette)

Modifications were done to support the ssd1306 128x64.

Prerequisites
=============

### WiringPi and WiringPi2-Python

Modules that use GPIO require [wiringpi](https://projects.drogon.net/raspberry-pi/wiringpi/) and [WiringPi2-Python](https://github.com/WiringPi/WiringPi2-Python).

To install wiringpi:
```
git clone git://git.drogon.net/wiringPi
cd wiringPi
sudo ./build
```

To install wiringpi2-python:
```
git clone https://github.com/Gadgetoid/WiringPi2-Python.git
cd WiringPi2-Python/
sudo python setup.py install
cd ..
```

### py-spidev

gaugette.ssd1306 requires [spidev](https://github.com/doceme/py-spidev).

### gdata-python-client

gaugette.oauth2 requires [Google's gdata](http://code.google.com/p/gdata-python-client/).

SSD1306 OLED Usage
==================

```python
    import gaugette.ssd1306
    RESET_PIN = 15
    DC_PIN    = 16
    led = gaugette.ssd1306.SSD1306(reset_pin=RESET_PIN, dc_pin=DC_PIN)
    led.begin()
    led.clear_display()
    led.draw_text2(0,0,'Hello World',2)
    led.display()
```

SSD1306 Font Usage
==================

```python
    from gaugette.fonts import arial_16
    font = arial_16  # fonts are modules, does not need to be instantiated
    # draw_text3 returns the col position following the printed text.
    x = led.draw_text3(0,0,'Hello World',font)  

    # text_width returns the width of the string in pixels, useful for centering:
    text_width = led.text_width('Hello World',font)
    x = (128-text_width)/2
    led.draw_text3(x,0,'Hello World',font)
```

The fonts include the printable ASCII characters ('!' through '~') and because of the usefulness of the degree symbol '&deg;', it has been added as a non-standard character 127 (0x7F hex and 177 octal).  Use the degree symbol in a python literal like this: 
```python
textSize = led.draw_text3(0,0,'451\177F', font)
```

Discussion At
=============

[http://guy.carpenter.id.au/gaugette/](http://guy.carpenter.id.au/gaugette/)

Using This Module In Your Code
==============================

You can use this code by checking it out into your source directory as follows:

```
cd myApplication
git clone git://github.com/guyc/py-gaugette.git
ln -s py-gaugette/gaugette gaugette
```
The soft link is created so that the local directory `gaugette` will point to 
`py-gaugette/gaugette` which simplifies your import statements.

Alternatively if you want to install this module as a system-wide python module, you can
do so as follows:

```
cd myPythonStuff
git clone git://github.com/guyc/py-gaugette.git
cd py-gaugette
sudo python setup.py install
```
