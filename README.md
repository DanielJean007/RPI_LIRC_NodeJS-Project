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
          Using: sudo node lirc_web/app.js
        - Tunnel the local web server to the world.
          Using: lt -p 80 --subdomain your_subdomain
        - Use username and password to access the web server.
        - See the commands I recorded on the Internet.

  2 - Add your own stuff:
    You can use the built-in functions from LIRC lib, or my automated scripts.
    To begin using my scripts give them the right access:
      sudo chmod 777 recordIR renameIR deleteIR

    Using the scripts:
    2.1 - recordIR
      This script used 'mode2' built-in function from LIRC to record the RAW data from a remote control.
      This is so, for some remote controls I tested had such a lengthy encoding.
      Then, I had to use 'mode2' function instead of 'irrecord' function.

      To use the script type:
        ./recordIR name_of_command
      After that just follow the instructions that will pop up.

        - The expected result is 'name_of_command recorded graciously.'
        That means you'll be set and able to see the new command when typing:
          irsend list '' ''

        - If the result is 'Couldn't record command.' It's because no data was acquired.

    2.2 - deleteIR
      This script just manipulates the file where the commands are stored.

      To use the script type:
        ./deleteIR name_of_command
      After that just follow the instructions that will pop up.

        - The messages are self explanatory.

    2.3 - renameIR
      This script just manipulates the file where the commands are stored.

      To use the script type:
        ./renameR name_of_command_stored new_name_of_command
      After that just follow the instructions that will pop up.

        - The messages are self explanatory.
