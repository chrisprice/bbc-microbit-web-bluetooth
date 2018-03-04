# bbc-microbit-web-bluetooth

Communicating between the [BBC micro:bit](https://lancaster-university.github.io/microbit-docs/ble/profile/) and the browser using [Web Bluetooth](https://developers.google.com/web/updates/2015/07/interact-with-ble-devices-on-the-web#read_a_bluetooth_characteristic). How hard can that be... 

No rambling introduction to this one, I'm going to jump straight into the details so you don't get tempted to skip ahead and skip important steps... Like I did...

## Just do it

**Even if you are running the default firmware or ultimately want to run your own firmware, follow this step!** Flashing the default firmware via USB has a [number of ~confusing and cryptic~ useful side-effects](#why-was-the-first-step-to-flash-the-default-firmware-onto-the-microbit-via-usb). Don't worry, we'll come back to running your own custom firmware once we've got a working connection.

First up, we're going to flash the default firmware onto the micro:bit via USB. Download the [default firmware](https://lancaster-university.github.io/microbit-docs/resources/BBC_MICROBIT_OOB_FINAL.zip) and unzip it. Connect your micro:bit via USB, find the mounted drive and drag the `BBC_MICROBIT_OOB_FINAL.hex` onto it. After restarting, your micro:bit screen will be alternating between a `←` and an `A`

* You've previously tried to pair (or successfully paired) your micro:bit with any bluetooth devices.
** If you have, follow the instructions below for flashing new firmware via USB (it clears any paired devices as far as the micro:bit is concerned).

## It still won't work

If you go to the device information example and click connect you should be presented with a popup listing the micro:bit

### FAQ

#### Why was the first step to flash the default firmware onto the micro:bit via USB?

Good question! Unfortunately there are a number of issues, each of which can cause communication problems. We needed to ensure -

* Bluetooth was enabled. 
  * The default firmware enables bluetooth. Custom firmware often does not e.g. [MakeCode](https://makecode.microbit.org/) does not include the bluetooth package by default.
  
* All bluetooth services were enabled. 
  * The default firmware's bluetooth profile contains all of the built-in services. Custom firmware often only contains a subset of these services e.g. [MakeCode](https://makecode.microbit.org/) only enables 3 services by default: Device Information Service, Event Service and DFU Control Service.

* Paired device information was in a known state. 
  * Flashing via USB clears all paired device information from the micro:bit. Mismatched pairing information can cause hard to debug issues. Additionally, there's a hard limit of 4 paired devices.

* Pairing Mode was enabled.
  * Whilst more typically symptomatic of bluetooth not being enabled, it is possible to disable this independently.

* `Just Works` Pairing was enabled.
  * As there are three different pairing modes available, this makes for simpler instructions. See [Is there an easier way?](#is-there-an-easier-way) for a description of the other modes.

#### Is there an easier way?

Kind of. There are 3 different pairing modes, each with their own advantages -

* `Just Works` Pairing
  * This is the mode used by the default firmware and its use is covered by the instructions above.
* Passkey Pairing
  * Similar to the above, the micro:bit screen shows a passcode which you must enter on the connecting device. This prevents a [MITM attack](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) but is probably unnecessary for hobby projects.
* No Pairing
  * During development you can disable the need to pair the devices. 
