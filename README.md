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
      First, we added a login area.
      Since we'll be tunneling our local server.
      It's NOT interesting the everyone with the link could access the devices in our house.
      It's better if ONLY people with username and password could to it.

      To add a new user and password open the file 'users.js' under the folder 'db/'.
      Just follow the structure under 'var records'. To test the web server type:
          username: batman
          password: robin

      Another change is that we'll be using port 80, instead of 3000.

    1.2 - For LIRC lib
      For a quick test with the commands I've recorded, you can move the file 'lircd.conf' in this repo to the directory ~/ (which is supposed do be pi/home/).

      It's not a good idea to change this file from there. Believe me, I've tried.

      The folder 'lircFiles/' contains handy scripts for automating the process of recording a new command, deleting a command and renaming an existing command.

    After making these small changes the reader is able
