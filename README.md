maxcul-communication
======================

Describes the communication between MAX! devices and an CUL-Stick

Writing this down has helped me a lot in understanding the MAXcul protocol.
Maybe it helps someone else too.

Important sources of information were:

* github repository max-cube-protocol from Bouni https://github.com/Bouni/max-cube-protocol. 
    This is an explanation of the MAX! Cube-LAN-Gateway protocol.
    This gave me the idea to publish my accumulated knowledge about the communication between MAX! devices and an CUL-Stick also on github.

* ioBroker-adapter iobroker.maxcul. https://github.com/ioBroker/ioBroker.maxcul

* FHEM wiki. https://wiki.fhem.de/wiki/MAX

* culfw command refence. http://culfw.de/commandref.html

* MAX! Home automation by Dmitry A. Kazakov. http://www.dmitry-kazakov.de/ada/max_home_automation.htm

* and of course try and error

My experimental setup includes the following devices:

* 1 x DIY nanoCul with firmware culfw V1.67. https://wiki.fhem.de/wiki/Selbstbau_CUL
* 8 x MAX! Heating Thermostat basic (BC-RT-TRX-CyN)
* 12 x MAX! Shutter Contact (BC-SC-Rd-WM-2)
* 1 x MAX! Push Button (BC-PB-2-WM-RE)
* 1 x Raspberry Pi 3 with Raspbian-Jessie 2017-07-05 and automation platform ioBroker. https://www.iobroker.net/

I do not have a Wall Thermostat or a Cube-LAN-Gateway, therefore the communication with these devices is unfortunately missing.

You will find ??? beneath the explanations which were unclear to me or where approval was not sure for me.

If you want to contribute, pull requests are welcome!

