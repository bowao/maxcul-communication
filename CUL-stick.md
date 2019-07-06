CUL
===

## REQUEST CUL VERSION

### Send to CUL:

	V
	|
	+---------------------------- Command V = Request CUL Firmware Version


### Response from CUL:

	V 1.67 nanoCUL868
	|||||||||||||||||
	+++++++++++++++++------------ CUL Firmware Version (string)

_______________________________________________________________________________________________________________________

## ENABLE RSSI

(RSSI = Received Signal Strength Indicator)

### Send to CUL:

	X20
	|||
	|++-------------------------- This is a one-byte hex value (bit 0 is the LSB bit) (see below)
	+---------------------------- Enable data reporting for SlowRF (i.e. 1kHz data rate)

Convert hex to bin

	20 = 00100000
	     ||||||||
	     |||||||+---------------- Report known messages (parity & checksum ok), with type prefix.
	     ||||||+----------------- Report each of the (repeated) packets of a message
	     |||||+------------------ Report detailed data, even with wrong parity / checksum.
	     ||||+------------------- Monitor mode: output an r on a risings edge and 'f' on a falling edge. 
	     ||||                     Output a '.' at the end of the message (no signal for 4msec).
	     |||+-------------------- Timing: in monitor mode output one additional byte of the internal 
	     |||                      microsecond timer, divided by 16. This is binary!
	     ||+--------------------- RSSI: report RSSI value as an additional HEX byte after digested data 
	     ||                       or as a separate byte if Bit 3 is set too. (Decoding see below)
	     |+---------------------- Report FHT protocol messages (ack, etc)
	     +----------------------- CUL/CUN: Report raw RSSI data (a==weak ... p==strong signal)
		                          CUR: Grafic representation: dark==weak ... light == stong signal 

Note:

* 00 disables radio reception, any other value initializes the radio chip and enables reception. 
* Default is 00: do not report anything, radio chip is uninitialized.
* Example: X01 (normal reporting, no RSSI) or X67 (debugging)
* If after X is nothing specified, report the current value and the available time for sending RF (in 10 ms units) (see REQUEST CREDITS)

#### Decoding RSSI hex-byte:

Convert RSSI hex in dec

RSSIdec between 0 and 124 ---> RSSIdec / 2 - 74

RSSIdec between 128 and 255 ---> ( RSSIdec - 254 ) / 2 - 74


### Response from CUL: 

**nothing**
_______________________________________________________________________________________________________________________

## REQUEST CREDITS:

### send to CUL:

	X
	|
	+---------------------------- If after X is nothing specified, report the current value and 
	                              the available time for sending RF (in 10 ms units)

### Response from CUL:

	20 900
	|| |||
	|| +++----------------------- Credits left: The available time for sending RF (in 10 ms units)
	++--------------------------- The current Value of X (see ENABLE RSSI)
_______________________________________________________________________________________________________________________

## ENABLE MORITZ (aka MAX!) MODE

### Send to CUL:

	Zr
	||
	++--------------------------- Enable MORITZ reception.

Note:
 
* Only MORITZ messages will be received in this mode. Data is reported in hex.
* If bit 4 was set in previous X cmd (i.e. X10) reported data is binary. 

#### Respond from CUL: 

**nothing**

_______________________________________________________________________________________________________________________

## ENABLE AUTO ACKNOWLEDGE
(See Push-Button and Shutter-Contact state messages)

### Send to CUL:

	Za
	||
	++--------------------------- Enabel Auto Acknowledge

Note:

* If Auto Acknowledge is not enabled, the Push-Button and the Shutter-Contact repeat their state-messages five times.
* This command is **not** specified in culfw reference: http://culfw.de/commandref.html



### Response from CUL: 

**nothing**

