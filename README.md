# RPI_LIRC_NodeJS-Project
This projects records the remote control command in order to bean them back from a local hardware set up on a RPI.

This setup can be accessed from anywhere via a Internet enable device

# Necessary hardware to run this project
  * Raspberry Pi board. This project was developed on a RPI-1B board.

  * Infra-Red sensor. (Emitter and receiver.)

  * Dongle wifi.

# Necessary software to run this project
  * LIRC library

  * NodeJS

  * lirc_web project

  * localtunnel or ngrok

# Where to find help for setting things up
Set up LIRC lib on RPI:
  * [Instructables](http://www.instructables.com/id/How-To-Useemulate-remotes-with-Arduino-and-Raspber/?ALLSTEPS)
  * [AlexBain](http://alexba.in/blog/2013/01/06/setting-up-lirc-on-the-raspberrypi/)

Set up NodeJs on RPI:
  * [Node-ARM](http://node-arm.herokuapp.com/)
  * [NodeJS](http://weworkweplay.com/play/raspberry-pi-nodejs/)

To wire the sensor to RPI and to test them:
  * [WireUP-IR](https://learn.adafruit.com/ir-sensor/testing-an-ir-sensor)
  * [Test-IR](http://randomtutor.blogspot.com.br/2013/01/web-based-ir-remote-on-raspberry-pi.html)

Set up dongle wifi to RPI:
  * [Ivan](http://ivanx.com/raspberrypi/raspberrypi_wifi.html)

Tunnel the local service to the world:
  * [HongKiat](http://www.hongkiat.com/blog/accessible-local-web-server/)
  * [LocalTunnel](https://github.com/localtunnel/localtunnel)

# What to do after following all the steps above?
### Move things around:
  * To `lirc_web/` folder:
    * Move the folders 'db/', 'views/' and the file 'app.js' to the folder 'lirc_web/'.
    * This will change the behaviour of the website where we can access the remote controls. Since our local server is going to be tunneled, it'll need a login area. It's NOT interesting the everyone with the link could access the devices in our house. It's better if ONLY people with username and password could to it.
    * To add a new user and password open the file 'users.js' under the folder 'db/'. Just follow the structure under 'var records'.
    * To test the web server type:
      * username: **batman**
      * password: **robin**
    * Another change is that we'll be using port 80, instead of 3000.

  * For LIRC lib
    * For a quick test of the functionalities of this project:
      * Move the file 'lircd.conf' in this repo to the directory ~/ (which is supposed do be pi/home/).
      After that type irsend list '' '' . You should see 'MasterControl'. This means you'll see the commands from this remote control on the website.

        **It's not a good idea to change 'lircd.conf' from it's original place. Believe me, I've tried.**

      * The folder `lircFiles/` contains handy scripts for automating the process of:
          - Recording a new command,
          - Deleting a command and
          - Renaming an existing command.

          **See instructions on how to use them bellow.**

  * After making these small changes you should be able to:
    - Use the built-in functions from LIRC lib.
    - Run a local web server with NodeJS. Using: `sudo node lirc_web/app.js`.
    - Tunnel the local web server to the world. Using: `lt -p 80 --subdomain your_subdomain`.
    - Use username and password to access the web server.
    - See the commands I recorded on the Internet.

### Add your own stuff:
You can use the built-in functions from LIRC lib, or my automated scripts. To begin using my scripts give them the right access using: `sudo chmod 777 recordIR renameIR deleteIR`.

  * Using the scripts:
    * recordIR:

      * This script uses `mode2` built-in function from LIRC to record the RAW data from a remote control. This is so, for some remote controls I tested had such a lengthy encoding that I had to use `mode2` function instead of `irrecord` function.

      * To use the script type: `./recordIR name_you_want_for_command`
      * After that just follow the instructions that will pop up. The expected result is `name_you_want_for_command recorded graciously.` That means you'll be set and able to see the new command when typing: `irsend list '' ''`.
      * If the result is `Couldn't record command.`, no data was acquired. You might want to try again.

    * deleteIR:
      * This script just manipulates the file where the commands are stored: `.allRawData`.

      * To use the script type: `./deleteIR name_of_command`. After that just follow the instructions that will pop up. The messages are self explanatory.

    * renameIR:
      * This script just manipulates the file where the commands are stored: `.allRawData`.

      * To use the script type: `./renameR name_of_command_stored new_name_of_command` After that just follow the instructions that will pop up. The messages are self explanatory.

  * After making these small changes you should be able to:
    - Record your own commands.
    - Remove my commands. Although I'd advise to use the command: `echo '' > lircFiles/.allRawData`. This command *erases* the content of the file where my commands **(and eventually yours)** are stored: `.allRawData`.
    - Delete your commands.
    - Rename your commands.

#### Attention: Every time you change the `lircd.conf` you must restart the `app.js` process. Then you will be able to see the changes on the web server.

### If you got here congratulations! Now you can control stuff over the Internet. You did that without adding any hardware to your devices.

# Disclaimer
  * By no means, this project is at a finished state. This project is intended to get your feet wet on RPI, LIRC, NodeJS and Tunneling.
  * It's also NOT bug free. You know...
  * Feel free to use the stuff here in your project as you see fit. Just remember to cite this repo.
  * And please, let me know of your projects that used this idea. I'd be glad to add your improvements to my project here.

# ---
#### `For God so loved the world that He gave his one and only Son, that whoever believes in Him shall not perish but have eternal life.`
#### `John 3.16`
