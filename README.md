# RPI_LIRC_NodeJS-Project
This projects records the remote control command in order to bean them back from a local hardware set up on a RPI.

This setup can be accessed from anywhere via a Internet enable device

# Necessary hardware to run this project
1 - Raspberry Pi board. This project was developed on a RPI-1B board.

2 - Infra-Red sensor. (Emitter and receiver.)

3 - Dongle wifi.

# Necessary software to run this project
1 - LIRC library

2 - NodeJS

3 - lirc_web project

4 - localtunnel or ngrok

# Where to find help for setting up things
  Set up LIRC lib on RPI:

    1 - http://www.instructables.com/id/How-To-Useemulate-remotes-with-Arduino-and-Raspber/?ALLSTEPS

    2 - http://alexba.in/blog/2013/01/06/setting-up-lirc-on-the-raspberrypi/


  Set up NodeJs on RPI:

    1 - http://node-arm.herokuapp.com/

    2 - http://weworkweplay.com/play/raspberry-pi-nodejs/

  To wire the sensor to RPI and to test them:

    1 - https://learn.adafruit.com/ir-sensor/testing-an-ir-sensor

    2 - http://randomtutor.blogspot.com.br/2013/01/web-based-ir-remote-on-raspberry-pi.html

  Set up dongle wifi to RPI:

    1 - http://ivanx.com/raspberrypi/raspberrypi_wifi.html

  Tunnel the local service to the world:

    1 - http://www.hongkiat.com/blog/accessible-local-web-server/

    2 - https://github.com/localtunnel/localtunnel

# What to do after following all the steps above?
  1 - Moving things around:

    1.1 - For lirc_web
      Move the folders 'db/', 'views/' and the file 'app.js' to the folder 'lirc_web'.

      This will change the behaviour of the website where we can access the remote controls.
      Since our local server is going to be tunneled, it'll need a login area.
      It's NOT interesting the everyone with the link could access the devices in our house.
      It's better if ONLY people with username and password could to it.

      To add a new user and password open the file 'users.js' under the folder 'db/'.
      Just follow the structure under 'var records'.
      To test the web server type:
          username: batman
          password: robin

      Another change is that we'll be using port 80, instead of 3000.

    1.2 - For LIRC lib
      For a quick test of the functionalities of this project:
        - Move the file 'lircd.conf' in this repo to the directory ~/ (which is supposed do be pi/home/).
        - After that type irsend list '' '' . You should see 'MasterControl'.
      This means you'll see the commands from this remote control on the website.
      * It's not a good idea to change 'lircd.conf' from it's original place. Believe me, I've tried.

      The folder 'lircFiles/' contains handy scripts for automating the process of:
        - Recording a new command,
        - Deleting a command and
        - Renaming an existing command.
      * See instructions on how to use them bellow.

      After making these small changes you should be able to:
        - Use the built-in functions from LIRC lib.
        - Run a local web server with NodeJS.
        - Tunnel the local web server to the world.
        - Use username and password to access the web server.
        - See my commands on the Internet.

  2 - Add your own stuff
