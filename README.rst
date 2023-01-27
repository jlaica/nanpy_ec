Nanpy
=====

|Travis| |Latest Version| |Supported Python versions| |Downloads|

Programa la tarjeta Arduino Uno con Python. http://pypi.python.org/pypi/nanpy


Overview
--------
Nanpy es una biblioteca que usa nuestra tarjeta arduino como esclavo y es controlado por un dispositivo maestro como una PC , una Raspberry , etc. donde ejecutamos nuestros scripts.

Nanpy ayuda a los programadores habituados a la programación de tarjetas arduino y de c++ a una introducción e implementación rápida y sencilla a la sintaxis de python usando los mismos circuitos que ya tenemos construidos sin necesidad de modificar nada en ellos. 

Manejando pines I/O
~~~~~~~~~~~~~~~~~~~~

::

    from nanpy import ArduinoApi

    a = ArduinoApi()
    a.pinMode(13, a.OUTPUT)
    a.digitalWrite(13, a.HIGH)

Nanpy es fácilmente extensible y teóricamente puede usar todas las bibliotecas, permitiéndole crear cuantos objetos desee. Soportamos OneWire, Lcd, Stepper, Servo, DallasTemperature y muchos más...

¡Intentemos probar nuestra pantalla LCD de 16x2 en los pines 7, 8, 9, 10, 11, 12 y mostrar su primer "Hola mundo"!

::

    from nanpy import Lcd

    lcd = Lcd([7, 8, 9, 10, 11, 12], [16, 2])
    lcd.printString('Hello World!')

Esto es realmente sencillo. 

Serial communication
~~~~~~~~~~~~~~~~~~~~

Nanpy puede detectar automáticamente el puerto serie en el cual se encuentra conectado nuestra tarjeta ó puede especificar el puerto serie que estamos usando:

::

    from nanpy import SerialManager
    connection = SerialManager(device='/dev/ttyACM1')

y úsalo con tus objetos

::

    from nanpy import ArduinoApi
    a = ArduinoApi(connection=connection)
    a.pinMode(13, a.OUTPUT)
    a.digitalWrite(13, a.HIGH)

Puede especificar cuántos objetos SerialManager desea y controlar más que una placa Arduino dentro del mismo script.

Construir firmware e instalar
-----------------------------

En primer lugar, debe compilar el firmware y cargarlo en su
arduino, para hacer eso debemos clonar el repositorio 'nanpy-firmware' dedse Github <https://github.com/nanpy/firmware>`__ o puede descargarlo desde
PyPi <https://pypi.python.org/pypi/nanpy>`__.

::

    git clone https://github.com/nanpy/nanpy-firmware.git
    cd nanpy-firmware
    ./configure.sh

| You can now edit Nanpy/cfg.h generated file to configure your Nanpy
  firmware, selecting the features you want to include and the baud
  rate.
 
| Ahora necesitamos editar el archivo Nanpy/cfg.h para configurar el firmware Nanpy, seleccionando las características que desea incluir y la tasa de       baudios.
  
| To build and install Nanpy firmware, copy Nanpy directory under your
  "sketchbook" directory, start your Arduino IDE, open Sketchbook ->
  Nanpy and click on "Upload".

To install Nanpy Python library on your master device just type:

::

    pip install nanpy

To uninstall::

    pip uninstall nanpy

To install the latest version from Github::

    pip install https://github.com/nanpy/nanpy/archive/master.zip


How to contribute
-----------------

Nanpy still needs a lot of work. You can contribute with patches
(bugfixing, improvements, adding support for a new library not included
in Nanpy yet, writing examples and so on), writing documentation,
reporting bugs, creating packages or simply spreading Nanpy through the
web if you like it :) If you have any doubt or problem, please contact
me at stagi.andrea@gmail.com

Do you want to support us with a coffee? We need a lot of caffeine to
code all night long! if you like this project and you want to support
us, `please donate using
Paypal <https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=TDTPP5JHVJK8J>`__

Bug reports
-----------

- try the blink.py example
- try to test the function without Nanpy, using only Arduino code. If the problem remains then it is not a Nanpy bug.
- enable logging: `import logging;logging.basicConfig(level=logging.DEBUG)`
- attach the log messages
- attach your program. The program should be as small as possible which demonstrates the bug.
- check cfg.h. All needed functions are enabled?
- Run `examples/firmware_check.py` to check cfg.h again. All needed functions are listed?
- attach your cfg.h
- describe your hardware

Supported hardware
------------------

board:
 - ATmega boards (ATtiny has not enough RAM)
 - ESP8266 (communication over serial or WiFi connection)

external hardware:
 - BMP180 Digital pressure sensor
 - AD9850 Direct Digital Synthesizer
 - TLC5947 LED Driver
 - DHT11, DHT22, DHT21, AM2301 humidity sensors
 - HD44780 LCD controller
 - PCF8574 8-Bit I/O Expander for I2C
 - X9C1xxx (xxx = 102,103,104,503) digital potentiometers
 - HC-SR04 (ultrasonic sensor)

internal hardware:
 - counter, frequency measurement
 - PWM (advanced PWM functions are hardcoded for Uno compatible boards)
 - ADC
 - I2C
 - read, write RAM
 - read, write EEPROM
 - read, write all registers
 - tone()


License
-------

This software is released under MIT License. Copyright (c) 2012-2016
Andrea Stagi stagi.andrea@gmail.com

.. |Travis| image:: http://img.shields.io/travis/nanpy/nanpy.svg
   :target: https://travis-ci.org/nanpy/nanpy/
.. |Latest Version| image:: https://img.shields.io/pypi/v/nanpy.svg
   :target: https://pypi.python.org/pypi/nanpy/
.. |Supported Python versions| image:: https://img.shields.io/badge/python-2.7%2C%203.3%2C%203.4%2C%203.5-blue.svg
   :target: https://pypi.python.org/pypi/nanpy/
.. |Downloads| image:: https://img.shields.io/pypi/dm/nanpy.svg
   :target: https://pypi.python.org/pypi/nanpy/
