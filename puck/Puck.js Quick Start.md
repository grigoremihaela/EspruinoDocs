<!--- Copyright (c) 2016 Gordon Williams, Pur3 Ltd. See the file LICENSE for copying permission. -->
Getting Started with Puck.js
============================

* KEYWORDS: Puck.js,Quick Start,Getting Started,Web Bluetooth,BLE
* USES: Puck.js,Web Bluetooth

First, peel the silicone cover off your Puck.js and tip the circuit board out. On the back you'll find a platic tab in the battery that you need to pull out to power up your Puck.

Next, re-assemble. To make sure the button can click you need to put the battery facing down, with the silver shield facing towards the 'shelf' in the case.

Once you've got power on your Puck.js it'll start doing two things:

* Advertising itself on Bluetooth Low Energy
* Acting as an NFC tag that will redirect you to the Puck.js website

If you have an NFC phone, make sure NFC is on, and then move Puck.js near the NFC receiver on it. A Web page should open that will direct you to some examples.

Otherwise, you'll need to go straight to the Puck.js website - [https://puck-js.com/go](https://puck-js.com/go)


Using Puck.js
--------------

By default, Puck.js appears as a Bluetooth Low Energy device with a serial port. When you connect to this serial port you get full command-line access to the Espruno Javascript interpreter built into it.

To get started you have two options:

* Use the Espruino IDE or command-line tools to write code to Puck.js
* Send individual JavaScript commands to Puck.js without programming it


Using the Espruino IDE
----------------------

### With Web Bluetooth

<script><!--
  document.write("<p><b>Note:</b> Web Bluetooth is  <b>" +
    (navigator.bluetooth?'already enabled':'currently disabled')+
    "</b> on this computer.</p>");
--></script>

If your computer supports it, Web Bluetooth is the easiest way to get started with Puck.js.

You'll need:

* A Mac OS, Android, Chromebook or Linux computer (Windows should be supported in Q1 2017)
* The [Google Chrome](https://www.google.com/chrome/browser/desktop/) web browser
* If you have Linux you need `Bluez` newer than `5.40` - you can check by typing `bluetoothd --version`

First, you need to enable Web Bluetooth support:

* Type `chrome://flags` in the address bar
* You need to enable `Experimental Web Platform Features` (`chrome://flags/#enable-experimental-web-platform-features`) in Chrome 56 or later, or `Web Bluetooth` (`chrome://flags/#enable-web-bluetooth`) in Chrome 55 or earlier. For Chrome 56 and later on MacOS and Chromebook, there is no option available and Web Bluetooth is enabled by default.
* Restart your browser

Now:

* Go to the [Puck.js site](https://puck-js.com/go) and click the Web IDE option.
* Click the orange icon in the Top Left
* You should be shown a list of devices - click on `Puck.js ABCD` (where `ABCD` is the last 4 digits of your Puck's address)
* Wait a few seconds - you should now be connected!


### With an application

On some platforms (Windows, or Linux with older `Bluez`) Web Bluetooth isn't supported.

On these you'll need to install a native application. We've packaged up the Web IDE in builds for Windows, Linux, and Mac OS that you can download from the Espruino site.


### Via a Raspberry Pi

To be added soon...


### By wired connection

In the worst case, you don't have any computers that allow you to communicate using Bluetooth Low Energy.

But all is not lost! You can buy a USB-TTL converter, and can connect directly to your Puck.js.

Connect as follows:

| Puck.js  | USB->TTL converter |
|----------|--------------------|
| GND      | GND                |
| D28      | RX ( -> PC )       |
| D29      | TX ( <- PC )       |
| 3V       | 3.3v (Optional - to run without a battery) |

You can now use the normal Espruino Web IDE, or a serial terminal application at 9600 baud.


Command-Line
------------

You can use the Espruno command-line app. It works under [Node.js](https://nodejs.org/en/), so you'll need to:

* Install [Node](https://nodejs.org/en/)
* In a command prompt, type `npm install -g espruino`
* When that completes, you can type `espruino --help` for help
* To connect, try `espruino --list` to list devices, then copy your device's MAC address and type `espruino -p aa:bb:cc:dd:ee` to connect.


Sending Individual Commands
---------------------------

### Using Adafruit 'Bluefruit LE' app

* Start the app
* Choose the Puck.js device you want to communicate with and click `Connect`
* Click `UART`
* When connected you're ready to enter some commands - see `Commands` below

### `nRF UART` app

* Start the app
* Tap `Connect` and choose your Puck.js device
* Type commands into the console - see `Commands` below.

**Note:** In this app, you need to manually press the `Enter` key *before* sending a line

### A Website

You can use Web Bluetooth on your own website to control Puck.js devices, as long as you have a compatible browser.

While you can use Web Bluetooth directly, we've provided a helpful library. Just include
`<script src="https://puck-js.com/puck.js"></script>` in your website (served off `HTTPS`)
and you can easily execute commands just by running JS code like:

```
Puck.write('LED1.set();\n');
```

We've got [a proper tutorial on it here](/Puck.js Web Bluetooth)

### Your own app

You can make your own application to control Espruino for whatever platform you need.

For the simplest control, add you need to do is connect to the Puck.js bluetooth device and connect to the characteristic with ID `6e400002b5a3f393e0a9e50e24dcca9e`. You can then write repeatedly to it to send commands to Espruino.

### Commands...

type in `LED1.set()` and click send
* The red LED should light up.
* You can now type `LED1.reset()` to turn it off. `LED2` and `LED3` work too
* Note that responses are also being sent back. You can type in `BTN.read()` and `false` will be returned - it'll be `true` if the button is pressed
