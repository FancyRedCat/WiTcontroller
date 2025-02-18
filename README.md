# WiTcontroller

A WiTcontroller is a simple DIY, handheld controller that talks to a WiThrottle Server (JMRI, DCC-EX EX-CommandStation, Digitrax LnWi and many others) using the WiThrottle protocol to control DCC model trains. 

[See a video of it in use here.](https://youtu.be/RKnhfBCP_SQ)


[Discussion on Discord.](https://discord.com/channels/713189617066836079/735156882511102033)

[3d Printed Case](https://www.thingiverse.com/thing:5440351)

---

## Prerequisites

1. Some basic soldering skills.

    The components will work if just plugged together using jumpers, but they take a lot of space that way, so soldering them together is advised to make it more hand held.

2. Loading the code (sketch) requires downloading of one of the IDEs, this sketch, the libraries, etc. so some experience with Arduinos is helpful, but not critical.

3. A WiThrottle Server to connect to. WiTcontroller will work with any WiThrottle Server. e.g.

    * JMRI
    * DCC-EX EX-CommandStation
    * MRC WiFi
    * Digitrax LnWi

---

## Building

### Required Components

* WeMos Lite LOLIN32  (ESP32 Arduino with LiPo charger) ([Example](https://www.ebay.com.au/itm/284800618644?hash=item424f709094:g:-soAAOSwHslfC9ce&frcectupt=true))
* 3x4 Keypad  ([Example](https://www.jaycar.com.au/12-key-numeric-keypad/p/SP0770?pos=2&queryId=20aedf107668ad42c6fe1f8b7f7a9ca7))
* Polymer Lithium Ion Battery LiPo 400mAh 3.7V 502535 JST Connector (or larger capacity) ([500mAh Example](https://www.ebay.com.au/itm/133708965793?hash=item1f21ace7a1:g:tlwAAOSwfORgYqYK))
* KY-040 Rotary Encoder Module ([Example](https://www.aliexpress.com/item/1005003946689694.html?albagn=888888&&src=google&albch=search&acnt=479-062-3723&isdl=y&aff_short_key=UneMJZVf&albcp=21520181724&albag=168529973707&slnk=&trgt=dsa-1464330247393&plac=&crea=707854323770&netw=g&device=c&mtctp=&memo1=&albbt=Google_7_search&aff_platform=google&gad_source=1&gclid=Cj0KCQjwiOy1BhDCARIsADGvQnBPdlEVLYbYnLoOnN1p2bdjte0jYmInrgFD0WG16aF3GZtvrWTb6o0aAo8VEALw_wcB&gclsrc=aw.ds))
* OLED Display 0.96" 128x64 I2C IIC SSD1306 ([Example](https://www.ebay.com.au/itm/273746192621?ssPageName=STRK%3AMEBIDX%3AIT&_trksid=p2060353.m2749.l2649))
* Case - my one was 3d printed (see below)
* Knob ([Example](https://www.jaycar.com.au/35mm-knob-matching-equipment-style/p/HK7766?pos=7&queryId=cbd19e2486968bca41273cc2dbce54a4&sort=relevance))
* Wire - If you plan to solder the connections,which is the recommended approach, then stranded, coloured wire is advisable.  ([Example](https://www.jaycar.com.au/rainbow-cable-16-core-sold-per-metre/p/WM4516))

### Optional Components

* Optional: Up to 7 additional push buttons can be added, each with their own independent commands. ([Example](https://www.jaycar.com.au/red-miniature-pushbutton-spst-momentary-action-125v-1a-rating/p/SP0710))
* Optional: A 1.3" OLED Display 128x64 can be used instead of the 0.96" OLED Display 128x64 ([Example](https://www.aliexpress.com/item/32683094040.html?spm=a2g0o.order_list.order_list_main.110.25621802jRBB7y)) Note: You will need to make a small configuration change for this to work correctly.
* Optional: You can use a 4x4 keypad instead of the 3x4 keypad. Note: You will need to make a small configuration change in ``config_buttons.h`` for this to work correctly.

### Pinouts

*Standard Configuration Pinouts*
![Assembly diagram](WiTcontroller%20pinouts%20v0.1.png)

*Pinouts for Optional Additional Buttons*
![Assembly diagram - Optional Additional Buttons](WiTcontroller%20-%20Optional%20Buttons%20-%20pinouts%20v0.1.png)

*Pinouts for Optional 4x4 keypad and Additional Buttons*
![Assembly diagram - 4x4 keypad and Optional Additional Buttons](WiTcontroller%20-%204x4%20keypad,%20Optional%20Buttons%20-%20pinouts%20v0.1.png)

*Pinouts for Optional Battery Monitor and Additional Buttons*
![Assembly diagram - Optional Battery Monitor and Additional Buttons](WiTcontroller%20-%20Optional%20battery%20monitor.png)

*Default Pins for the keypads*

3x4 Keypad - Left to Right
 * C1 PIN 0
 * R0 PIN 19
 * C0 PIN 4
 * R3 PIN 16
 * C2 PIN 2
 * R2 PIN 17
 * R1 PIN 18

4x4 keypad - Left to Right
 * C0 PIN 4
 * C1 PIN 0
 * C2 PIN 2
 * C3 PIN 33
 * R0 PIN 19
 * R1 PIN 18
 * R2 PIN 17
 * R3 PIN 16
 
Notes: 

* Different keypads often arrange the pins on the base of the keypad differently.  So it is important make sure the pins on the keypad are correctly identified and adjusted as needed.

### Case

![3D printer case 1](images/witcontroller1.jpg)

![3D printed case 2](images/witcontroller1.jpg)

Notes:

* My case was 3D Printed for me by peteGSX (See the [Thingiverse.](https://www.thingiverse.com/thing:5440351) )
* The 3x4 keypad petGSX designed the case for came from Jaycar and is slightly narrower than the one you see in the 'deconstructed' view in the video above.
* The case requires about a dozen M2x4mm screws

* For a different take on what is possible by extending the design, have a look at: https://1fatgmc.com/RailRoad/DCC/page-5-B.html

## Loading the code

The instructions below are for using the Arduino IDE and GitHub Desktop. Visual Studio Code (VSC) can be used instead of the Arduino IDE but no instructions are included here.

 1. Download the Arduino IDE.
    * Available from  https://support.arduino.cc/hc/en-us/articles/360019833020-Download-and-install-Arduino-IDE
2. Download the **esp32** boards in the Arduino IDE.
    * Add the esp322 support with the following instructions:  (See here for detailed instructions:  https://randomnerdtutorials.com/installing-the-esp32-board-in-arduino-ide-windows-instructions/)
        * In the Arduino IDE, go to *File* > *Preferences*
        * Enter the following into the 'Additional Board Manager URLs' field:  https://dl.espressif.com/dl/package_esp32_index.json
    * Then Use the *Boards Manager* in the *Arduino IDE* to install the esp32 board support
        * *Tools* > *Board* > *Boards Manager*
        * Search for "esp32" by Expressive Systems.  Install version 2.0.11
3. Download or clone *this* repository. (Note: if you 'clone' initially, it is easier to receive updates to the code by doing a 'fetch' subsequently.  See Notes below.)
    * Clone - **First Time**
       * Install *GitHub Desktop* from https://desktop.github.com/
       * Create a free account on GitHub and authorise the app to allow it to connect top GitHub
       * Select *file* -> *Clone Repository* - or 'Clone an repository from the internet' from the welcome page then select the 'URL' tab
       * Enter *https://github.com/flash62au/WiTcontroller* as the URL
       * Select a local folder to install it.  The default folder for the Arduino usually looks like "...username\Documents\Arduino\". (This is a good but not essential place to put it.)
       * Click *Clone*
       * **Subsequently**  (Anytime after the first 'clone')
         * click *Fetch Origin* and any changes to the code will be bought down to you PC, but you config_buttons.h and config_network.h will not be touched.
    * Download 
       * Open *https://github.com/flash62au/WiTcontroller*
       * Click the green "Code" button and select download zip
       * Extract the zip file to a local folder.  The default folder for the Arduino usually looks like "...username\Documents\Arduino\". This is a good, but not essential, place to put it.
4. Load the needed libraries to your PC. <br/> These *MUST BE* loaded from the *Library Manager* in the *Arduino IDE*. 
    * *U8g2lib.h* -  Search for "U8g2".   Install version 2.34.22
    * *AiEsp32RotaryEncoder.h* - search for "Ai Esp32 Rotary Encoder".  Install Version 1.6
    * *Keypad.h* - Search for "Keypad" by Mark Stanley.   Install version 3.1.1
    * *WiThrottleProtocol.h* - Search for "WiThrottleProtocol" (not "WiThrottle").  Install version 1.1.14 or later if available.
    
      Note: <br/> **DO NOT** download these libraries *directly*. Use the *Library Manager*. <br/> **DO NOT** put them in the WiTcontroller folder.
5. These should have been automatically installed when you downloaded the esp32 boards.  *YOU SHOULD NOT NEED TO DO ANYTHING SPECIFIC TO GET THESE*
    * *WiFi.h*  - https://github.com/espressif/arduino-esp32/tree/master/libraries/WiFi
    * *ESPmDNS.h* - https://github.com/espressif/arduino-esp32/blob/master/libraries/ESPmDNS

      Note: <br/> **DO NOT** download these libraries *directly*. Use the *Boards Manager*. <br/> **DO NOT** put them in the WiTcontroller folder.
6. Copy the two example config files. <br/> You will need to use a *File Manger* type of app on the PC to do this.
    * Copy ``config_network_example.h`` to a new file to ``config_network.h``. 
    * Copy ``config_buttons_example.h`` to a new file ``config_buttons.h``.

      Note: <br/> these files are not included in the download, so that you can personalise your configuration without fear that those configurations will be overridden if you update (download again) the WiTcontoller code.

6. Open the Arduino IDE and **THEN** find and open the ``WiTcontoller.ino`` file.

      Note: <br/> *If you open the file **from** the IDE*, rather then opening it from a File Manager, will automatically open *all the files in the WiTcontroller folder* in the IDE. 
      
      Whereas, *if you open it from a File manger app* (by double clicking on it) only the file you selected will open.

7. Edit your personal ``config_network.h`` file. 
    * Edit it to include the network SSIDs you want to use.  (Not essential, but entering passwords via the encoder is tedious.)
7. Edit your personal ``config_buttons.h`` file.
    * Optionally, edit this to change the mapping of the keypad buttons to specific functions.
    * Optionally, edit this to configure the additional buttons (if you have included them) to specific functions.
    * Optionally, edit this to change if you want the function buttons to display when you press #, instead of the default of showing the Key Definitions
8. Upload the sketch.  
    * Select the board type as ``WEMOS LOLIN32 Lite`` in the *Arduino IDE*.
    * Connect the board via USB and select the appropriate port in the *Arduino IDE*.
    * Click ``Upload`` **-->**

Notes: 
   * WiTcontroller version 1.82 or later requires WiThrottleProtocol version 1.1.26
   * WiTcontroller version 1.73 or later is recommended to use WiThrottleProtocol version 1.1.25 or later to address a bug in heartbeat send  but only seen with JMRI WiThrottle 
   * WiTcontroller version 1.66 or later requires WiThrottleProtocol version 1.1.24
   * WiTcontroller version 1.65 or later requires WiThrottleProtocol version 1.1.23
   * WiTcontroller version 1.57 or later requires WiThrottleProtocol version 1.1.20 or later for the E_STOP and E_STOP_CURRENT_LOCO to work correctly.
   * WiTcontroller version 1.45 or later requires WiThrottleProtocol version 1.1.14 or later.
   * WiTcontroller version 1.41 or later requires WiThrottleProtocol version 1.1.12 or later.
   * WiTcontroller version 1.39 or later requires WiThrottleProtocol version 1.1.11 or later.
   * WiTcontroller version 1.38 or later requires WiThrottleProtocol version 1.1.10 or later.
   * WiTcontroller version 1.35 or later requires WiThrottleProtocol version 1.1.7 or later.
   * WiTcontroller version 1.33 or later requires WiThrottleProtocol version 1.1.6 or later.
   * WiTcontroller version 1.19 - 1.32 requires WiThrottleProtocol version 1.1.3 - 1.1.5.
   * WiTcontroller version 1.06 or later requires WiThrottleProtocol version 1.1.2 or later.
   * WiTcontroller version 1.01 or later requires WiThrottleProtocol version 1.1.0 or later.
   * WiTcontroller version 0.10 or later requires WiThrottleProtocol version 1.0.3 or later.
   * The *WiFi.h* and *ESPmDNS.h* libraries were automatically installed for me when I installed the esp32 boards, however you may need to install them manually.
   * Later versions of the ESP board support are available and do appear to work, but if you have difficulties version 1.0.6 appears to be stable.
   * Later versions of the libraries generally should work, but if you have difficulties use the versions listed above.
   * To get the WiTcontroller sketch I recommend using either the git command line, or the far more friendly 'GitHub Desktop' app.  See instructions above.
   * If you receive and error related to Python, and you are on MacOS 12 and above please edit the platform file, change from python to python3 as follows; preferences->user/path/arduino/packages/hardware/esp32/version/platform.txt and edit the line that looks as follows:tools.gen_esp32part.cmd=python3 "{runtime.platform.path}/tools/gen_esp32part.py"

---

## Using WiTController

**Currently functioning:**
- Provides a list of discovered SSIDs with the ability to choose one. When you select one:
  - if it is one in your specified list (in the sketch), it will use that specified password 
  - if it is a DCC++EX WiFi Command Station in access Point mode, it will guess the password
  - otherwise it will ask to enter the password (Use the rotary encoder to choose each character and the encoder button to select it.  * = backspace.  # = enter the password.) 
- Optionally provides a list of SSIDs with the specified passwords (in the sketch) to choose from
- Auto-connects to the first found WiThrottle Protocol Server if only one found, otherwise 
  - Asks which to connect to
  - If none found will ask to enter the IP Address and Port
  - Guesses the WiThrottle IP address and Port for DCC++EX WiFi Access Point mode Command Stations
  - optionally can add a #define (a preference) to disable this auto connect feature
- Rudimentary on-the-fly consists
- Assign commands directly to the 1-9 buttons (in the sketch) (see list below)
  - This is done in config_button.h
  - Latching / non-latching for the function is provided by the roster entry of WiThrottle server
- Optionally use a potentiometer (pot) instead of the rotary encoder
- Optional ability to assign commands directly to the 1-7 additional buttons (in the sketch) (see list below)
  - These are defined config_button.h
- Command menu (see below for full list) including:
  - Able to select and deselect locos 
    - by their DCC address, via the keypad
      - On NCE systems, a leading zero (0) will force a long address
    - from the first 50 locos in the roster
  - Able to select multiple locos to create a consist
    - Able to change the facing of the additional locos in the consists (via the 'extra' menu after selection)
  - Able to activate any function (0-31)
    - Showing of the roster function labels (from the WiThrottle server if provided)
    - Quick access to the functions by pressing #. Temporarily enabled via the Extras menu (or permanently enabled in config_button.h)
    - Limited ability to configure which functions are sent to the first or all locos in a consist (defined in config_button.h)
  - Able to throw/close turnouts/points
    - from the address
    - from the first 50 turnouts/points in the server list
  - Able to activate routes
    - from their address
    - from the first 50 routes in the server list
  - Set/unset a multiplier for the rotary encoder
  - Power Track On/Off
  - Disconnect / Reconnect
  - Put ESP32 in deep sleep and restart it
  - Option to switch between Single Loc and Consist/MU (Drop before Acquire)
  - Option to save the currently select locos (on multiple throttles) and have them automatically re-acquired on next connection.
- Option to have up to 6 command sequences executed on connection
- Option to automatically acquire a loco if there is only one loco in the roster
- Have up to 6 throttles, each with an unlimited number of locos in consist. Default is 2 throttles, which can be increased or decreased temporarily via the Extras menu (or permanently enabled in config_button.h)
- Limited dealing with unexpected disconnects.  It will throw you back to the WiThrottle Server selection screen.
- Boundary between short and long DCC addresses can be configured in config_buttons.h
- The default speed step (per encoder click) can be configured in config_buttons.h
- The controller will automatically shut down if no SSID is selected or entered in 4 minutes (to conserve the battery)

**ToDo:**
- Speed button repeat (i.e. hold the button down)
- Deal with unexpected disconnects better
  - automatic attempt to reconnect
- Keep a list of ip addresses and ports if mDNS doesn't provide any

### Command menu:
- 0-9 keys = pressing these directly will do whatever you has been preset in the sketch for them to do  (see \# below)
- \* = Menu:  The button press following the \* is the actual command:
  - 1 = Add loco.  
     - Followed by the loco number, followed by \# to complete.  e.g. to select loco 99 you would press '\*199\#'
     - or \# alone to show the roster   \# again will show the next page
  - 2 = release loco:
     - Followed by the loco number, followed by \# to release an individual loco.  e.g. to deselect the loco 99 you would press '\*299\#'
     - Otherwise followed directly by \#  to release all e.g. '\*2\#'
  - 3 = Toggle direction.
  - 4 = Set / Unset a 2 times multiplier for the rotary encoder dial.
  - 5 = Throw turnout/point.  
     - Followed by the turnout/point number, followed by the \# to complete.  e.g. Throw turnout XX12 '\*512\#'  (where XX is a prefix defined in the sketch) 
     - or \# alone to show the list from the server   \# again will show the next page
  - 6 = Close turnout.    
     - Followed by the turnout/point number, followed by \# to complete.  e.g. Close turnout XX12 '\*612\#'  (where XX is a prefix defined in the sketch)
     - or \# alone to show the list from the server
  - 7 = Set Route.    
      - Followed by the Route number, followed by \# to complete.  e.g. to Set route XX:XX:0012 '\*60012\#'  (where \'XX:XX:\' is a prefix defined in the sketch)
      - or \# alone to show the list from the server   \# again will show the next page
  - 0 = Function button. Followed by...
      - the function number, Followed by \# to complete.  e.g. to set function 17 you would press '\*017\#'
      - \# alone, to show the list of functions.
  - 8 = Track Power On/Off.
  - 9 = Extras. Followed by...
      - 0 then \# to toggle the action the the \# key does as a direct action, either to show the direct action key definitions, or the Function labels.  
      - 1 to change the facing of locos in a consist.
      - 3 to toggle the heartbeat check.
      - 4 to increase the number of available throttle (up to 6)
      - 5 to decrease the number of available throttle (down to 1)
      - 6 to Disconnect/Reconnect.  
      - 7 to put into deep sleep
      - 8 Toggle between Single loco and Consist/MU (Drop before Acquire)
      - 9 Save the Currently selected locos so they will be automatically acquired on reconnection
Pressing '\*' again before the '\#' will terminate the current command (but not start a new command)
 - \# = Pressing # alone will show the function the the numbered keys (0-9) perform, outside the menu.
       Optionally, you can configure it so that the the Function labels from the roster show 

Pressing the Encoder button while the ESP32 is in Deep Sleep will revive it.

----

### Screens

## WiFI/SSID Connection Screens

*Start-up - browsing for SSIDs*<br />
![Start-up - browsing for SSIDs](images/screenshots/browsing_for_ssids.jpg)

*SSID (WiFi networks) list*<br />
![SSID list](images/screenshots/ssid_list.jpg)

*Trying to to connect to SSID*<br />
![Trying to to connect to SSID](images/screenshots/trying_to_connect.jpg)

## WiThrottle Server Connection Screens

*WiThrottle Server List*<br />
![WiThrottle Server List](images/screenshots/wit_server_list.jpg)


#### Throttle Screen

*Throttle Screen with no loco acquired*<br />
![Throttle Screen with no loco acquired](images/screenshots/throttle_no_loco_acquired.jpg)

*Throttle Screen - with locos selected on throttle 1 and throttle 2*<br />
![Throttle Screen](images/screenshots/throttle.jpg)

```
TT LLLL LLLL LLLL               BBBBB
TT ----------------------------------
f f f f f f f f f f f f f f f f f f f
              SSSSS  DDDD
              SSSSS  DDDD
              SSSSS            
M             SSSSS              llll
P  h                          d sss d
-------------------------------------
mmmmmmmmm
```

* TT   = Current Throttle Number
* LLLL = Currently acquire loco(s) on this throttle
* SSSS = Speed of current throttle (0-126)
* DDDD = Direction of current throttle (Fwd,Rev)
* f    = state of each function of 30 functions (number displays if the function is active)<br /><br />
* llll = First Loco on *next* available throttle
* d    = Direction of next next available throttle (<,>)
* sss  = Speed of next available throttle (0-126)<br /><br />
* h    = heartbeat (only displays if heartbeat is disabled)
* M    = Speed step multiplier
* P    = Track Power
* BBBB = Optional battery state
* mmmm =  menu, other instructions or broadcast messages

#### * Menu

![Menu](images/screenshots/menu.jpg)

#### # Direct Commands List

![Direct Commands List](images/screenshots/direct_commands_list.jpg)

----

### Default number key assignments (0-9)  (outside the menu)

* 0 = FUNCTION_0 (DCC Lights)
* 1 = FUNCTION_1 (DCC Bell)
* 2 = FUNCTION_3 (DCC Horn/Whistle)
* 3 = FUNCTION_3
* 4 = FUNCTION_4
* 5 = NEXT_THROTLE
* 6 = SPEED_MULTIPLIER
* 7 = DIRECTION_REVERSE
* 8 = SPEED_STOP
* 9 = DIRECTION_FORWARD

### Allowed assignments for the 0-9 keys:

Note: you need to edit config_buttons.h to alter these assignments   (copy config_buttons_example.h)
- FUNCTION_NULL   - don't do anything
- FUNCTION_0 - FUNCTION_31
- SPEED_STOP
- SPEED_UP
- SPEED_DOWN
- SPEED_UP_FAST
- SPEED_DOWN_FAST
- SPEED_MULTIPLIER
- E_STOP   - E Stop all locos on all throttles
- E_STOP_CURRENT_LOCO - E Stop locos on current throttle only
- POWER_TOGGLE
- POWER_ON
- POWER_OFF
- SHOW_HIDE_BATTERY
- DIRECTION_TOGGLE
- DIRECTION_FORWARD
- DIRECTION_REVERSE
- NEXT_THROTTLE
- SPEED_STOP_THEN_TOGGLE_DIRECTION   - stops the loco if moving.  Toggles the direction if stationary.
- MAX_THROTTLE_INCREASE    - change the number of available throttles on-the-fly
- MAX_THROTTLE_DECREASE    - change the number of available throttles on-the-fly

---

### instructions for optional use of a potentiometer (pot) instead of the encoder for the throttle

config_buttons.h can include the following optional defines:

  * \#define USE_ROTARY_ENCODER_FOR_THROTTLE false
  * \#define THROTTLE_POT_PIN 39
  * \#define THROTTLE_POT_USE_NOTCHES true 
  \#define THROTTLE_POT_NOTCH_VALUES {1,585,1170,1755,2340,2925,3510,4094}
  * \#define THROTTLE_POT_NOTCH_SPEEDS {0,18,36,54,72,90,108,127} 

  If ``USE_ROTARY_ENCODER_FOR_THROTTLE`` is set to ``false`` the rotary encoder is ignored and a pot on the pin defined with ``THROTTLE_POT_PIN`` will be used instead.

  You must specify the PIN to be used.  Currently PINs 34, 35 and 39 are the only ones that cannot be used by the app for other purposes, so these are the safest to use.  This should be connected to the centre pin of the pot. The 3v and GND should be connected to the outer pins of the pot.

  The pot can be set to have 8 defined 'notches' (the default) or just a linear value.

  If you want to have the 8 notches:
  
  a) You must define the values the pot will send at each of 8 points - ``THROTTLE_POT_NOTCH_VALUES``.  Note that you should avoid the value zero (0) for notch zero.  Use at least 1 instead.

    The example values above are useble for a 10k ohm pot but any value pot can be used. Just adjust the numbers.

  b) You must define what speed should be sent for each notch - ``THROTTLE_POT_NOTCH_SPEEDS``

  If you want a linear speed instead of notches:

  a) You must define the values the pot will send at at zero throw and full throw in the first and last of the 8 values in ``THROTTLE_POT_NOTCH_VALUES``.  The other values will be ignored but you still need to include 8 values.  (They can be zero.)  Note that you should avoid the value zero (0) for notch zero.  Use at least 1 instead.

  Sumner Patterson is developing an app to help find the appropriate pot values for the ``THROTTLE_POT_NOTCH_VALUES``.

---

### Instructions for optional use of a voltage divider to show the battery charge level

See diagram above for how to wire in the volage divider.  47k resistors are used, but this can be varied as long as the output to the pin is limited to below 3.3v. See additional information related to the Pangodream Library that WiTcontroller uses here... https://www.pangodream.es/tag/18650-ion-li

The diagram has the voltage divider spliced into battery leads, but you can solder the positive in to the back of the battery connector (on the ESP32) if you prefer. The ground can be taken from any ground pin.

*To enable the battery monitor*, set the following to ``true``. The default is ``false``.

``#define USE_BATTERY_TEST true``

*To set which pin to use.* The default is ``34``.  In theory 34, 35, 36, or 39 should be able to be used, but only 34 and 36 have been tested.   (36 is marked 'VP' on the board.  39 is marked 'VN' on the board.)

``#define BATTERY_TEST_PIN 34``

If the battery does not show 100% when plugged into the charger, you may need to adjust this value. The default is ``1.7``.

``#define BATTERY_CONVERSION_FACTOR 1.7``

    To help work out the correct BATTERY_CONVERSION_FACTOR, you can enable so serial monitor message that will assist.

    In your ``config_buttons.h`` add (or uncomment) these defines:
    
      #define WITCONTROLLER_DEBUG    0
      #define DEBUG_LEVEL   2

    DEBUG_LEVEL must be 2 or greater

    a) Make sure your battery is fully charged.
    b) Upload the code and open the serial monitor. 
    c) Wait. Don't connect.
    You will see lines like...

      BATTERY TestValue: 100 (10003)
      BATTERY lastAnalogReadValue: 2491 (10003)
      BATTERY If Battery full, BATTERY_CONVERSION_FACTOR should be: 1.69 (10014)

    Let it run for a while.
    d) Note one of the recommend values (it will vary a bit) and enter it into the define in your config_buttons.h
    e) Re-upload code and connect to a server
    f) Confirm that the battery reads 100% (repeat if not)
    g) Run the HandCab on battery for few hours and confirm the battery level is droping at an expected rate. (adjust the conversion factor if not.)

*To show the calculated percentage*, set the following to ``true`` The default is ``false``.

``#define USE_BATTERY_PERCENT_AS_WELL_AS_ICON true``

*To force the HandCab to go to sleep at a specific level*, set this value. (e.g. to 3 or 5.) A value of less than zero (e.g. -1) will disable the feature. By default it is disabled (-1).

``#define USE_BATTERY_SLEEP_AT_PERCENT 3``

The display of the battery can be temporarily toggled by setting a key or button to ``SHOW_HIDE_BATTERY``.  The display will cycle between none, icon only and icon plus percent value. Note that ``USE_BATTERY_TEST`` must be set to `true` for this to have any effect.

Note: 
I recommend adding a physical power switch to disconnect the battery as this feature will, slowly, continually drain the battery, even when not being used.

---

``#define STARTUP_COMMAND_1 ""`` .. ``#define STARTUP_COMMAND_4 ""``

Optional. If defined, the up to four commands will be executed, in order, after connection to the WiThrottle Server.
Each must be ONLY ONE single valid command.  Either a direct action or a menu action.  Any can be blank or not defined, the others will still be executed.

Note: Selecting from the roster/turnouts etc. is not possible as the commands will execute before the roster loads.

---

``#define ACQUIRE_ROSTER_ENTRY_IF_ONLY_ONE true``

Enabling this option will automatically acquire the only roster entry after connection to the WiThrottle Server, but only if there is ***only one*** roster entry. 

---

### Instructions for German Translations     Anleitung für deutsche Übersetzungen

The file ``language_deutsch.h`` contains German translations (by Bastian Zechendorf).  Uncomment (or add) the ``#include "language_deutsch.h"`` line in ``config_buttons.h`` to see menus and messages in German.

You can override any of these translations individually by adding an appropriate ``#define`` statement in the ``config_buttons.h``, but it *must* be *before* the ``#include...`` statement.

Die Datei ``language_deutsch.h`` enthält deutsche Übersetzungen (von Bastian Zechendorf).  Kommentieren Sie die Zeile ``#include "language_deutsch.h"`` in ``config_buttons.h`` aus (oder fügen Sie sie hinzu), um Menüs und Meldungen auf Deutsch anzuzeigen.

Sie können jede dieser Übersetzungen einzeln überschreiben, indem Sie eine entsprechende ``#define`` -Anweisung in ``config_buttons.h`` hinzufügen, diese muss jedoch *vor* der ``#include...`` -anweisung stehen.

I would appreciate any assistance to improve these translations.
If you are interested, please contact me directly for instructions.

Ich würde mich über jede Hilfe zur Verbesserung dieser Übersetzungen freuen.
Bei Interesse kontaktieren Sie mich bitte direkt für eine Anleitung.

### Instructions for Other Translations

If you create a copy of the file ``language_deutsch.h`` (with a new name) and change the German text it contains to any language you wish (using the English text on the right as a guide to what is needed) you can add that file as an include in ``config_buttons.h``.

I would welcome it if you then sent me the file you created for inclusion in this repository.

---
---

## Change Log

### V1.83
- log any unknown commands from the server.  Requires WiThrottleProtocol version 1.1.26 or later

### V1.82
- Made ``RESTORE_ACQUIRED_LOCOS`` default to true.
  - Added an Extra Menu option to save the current locos
  - Removed the save when deliberately disconnected or slept the device (extra menu ``#96`` or ``#97``)

### V1.81
- Show the battery status on the Start, SSID browse, Wit browse and Shutdown screens.

### V1.80
- Added ``RESTORE_ACQUIRED_LOCOS`` option. If this option is enabled, and you have deliberately disconnected or slept the device (extra menu ``#96`` or ``#97``), then the next time you connect the device it will try to load the previously acquired locos.

### V1.78
- Added ``DROP_BEFORE_ACQUIRE`` option and also toggle for this in the Extras menu

### V1.77
- Bug fix for when a DCC-EX EX-CommandStation has the password changed from the default.

### V1.77
- The additional CR+LF are now sent ahead of all commands to all command stations by default. This was originally only sent for WiFiTrax, but other commercial CSs seem to have the same issue that this resolved. This can be disabled if needed with ``#define SEND_LEADING_CR_LF_FOR_COMMANDS false`` in ``confing_network.h``.
- Added a message when the server has just connected and is caught up receiving the roster etc. and is unable to process commands yet.

### V1.76
- Option to automatically acquire the only roster entry on connection to the WiThrottle server, but only if there is ***only one*** roster entry.  ``#define ACQUIRE_ROSTER_ENTRY_IF_ONLY_ONE true``

### V1.75
- Option for up to four start-up commands ``#define STARTUP_COMMAND_1 ""`` .. ``#define STARTUP_COMMAND_4 ""``

### V1.74
- German translations by Bastian Zechendorf.
- Made it simpler to change the language.
- Improvements for non-English language display.
- Bug fix. Removed duplicated first entry in the Roster (at the end).

### V1.73
- Add debug level option ``#define DEBUG_LEVEL``
- A bug in the heartbeat send in the protocol library was fixed at the same time as this release.
- if heartbeat is enabled, deliberately send the command to server to start it. (I had previously assumed that this was not required.)

### V1.72
- add the ability to sort the roster with the new define ``ROSTER_SORT_SEQUENCE``
   - 0 = no sorting.  As it comes from the server
   - 1 = sort by name (first 10 chars only)  - Default
   - 2 = sort by DCC Address

### V1.71
- add the ability to define the consist follow function options for all 32 functions ``CONSIST_FUNCTION_FOLLOW_F0`` to ``CONSIST_FUNCTION_FOLLOW_F31``

### V1.70
- add define to enable or disable the heartbeat by default    ``#define HEARTBEAT_ENABLED true``

### V1.69
- New define added for if no response is received from the server in the specified period (milliseconds), shut down. MAX_HEARTBEAT_PERIOD   default is 4 minutes = 240000 

### V1.68
- improve bouncing on the pot values
- bug fix for functions list & menus closing when the pot value bounces

### V1.67
- bug fix for adding locos greater than 300 and less than 499

### V1.66
- Add support for setting the additional button as latching or non-latching, overriding the WiThrottle defaults. Requires WiThrottleProtocol version 1.1.24.

### V1.65
- Fix for individual loco direction (facing) changes in a consist. Requires WiThrottleProtocol version 1.1.23 or later

### V1.63 - v1.64
- bug fix for the user defined menus

### V1.62
- rewrite of the menu code to support user defined menus
- bug fix for the Edit Consist not working

### V1.61
- Bug fix - Speed step multiplier not being displayed
- Added screenshots to the Readme

### V1.60
- ignore broadcast alert "Steal from other WiThrottle or JMRI throttle Required"

### V1.59
- Experimental attempt to automatically steal locos on Dijitrax systems

### V1.58
- bug fix when not using the battery test

### V1.56 / 1.57
- Moved the battery position to the top line
- added an Action to show or hide the battery
- Added some of the UI improvements from HandCab
- Fixed the E_STOP VS E_STOP_CURRENT_LOCO. Requires WiThrottleProtocol version 1.1.20 to actually work differently.
- Updated documentation. (Particularly on the use of the battery)

### V1.55
- automated fix the latest versions of the ESP32 Board Library (3.0.0 and later) having renamed an attribute. The code now automatically adjusts for this.  
- German translation file included

### V1.54
- minor format change 

### V1.53
- Add support for hardware build that utilises a bare EC11 rotary encoder (with no physical resistor pullups) in place of the KY040 encoder module (which incorporates physical pullups)
- This version will switch on GPIO internal pullups if EC11_PULLUPS_REQUIRED is set true in config_buttons.h
- added auto deep sleep on low battery 

### V1.52
- Made two changes in main code 1. Comment out random values when displaying battery percentage
- and 2.Invert logic for the test to display the battery percentage 

### V1.51
- changed option to have the battery to show icon as well as a percent

### V1.50
- option to have the battery to show as a percent

### V1.49
- change the battery check to once ever 10 seconds

### V1.48
- change the battery charge level to an icon/glyph

### V1.47
- support for optionally using a voltage divider to show the battery charge level

### V1.46
- support for optionally using a potentiometer (pot) instead of the encoder for the throttle

### V1.45
- support for 4x4 keypads

### V1.44
- support for optional custom commands

### V1.43
- bug fix

### V1.43
 - text, button and display PIN configurations moved to defines that can be overridden in personal config_buttons_etc.h files
 - no functional changes

### V1.42
 - minor bug fix
 
### V1.41
  - support for broadcast messages. Requires WiThrottleProtocol version 1.1.12 or later.

### V1.40
 - fix for the debounce of the rotary encoder button. Will now ignore rotations when the button is pressed for (default) 200ms.  The #define for the debounce has been moved from config_keypad_etc.h to config_buttons as: #define ROTARY_ENCODER_DEBOUNCE_TIME 200

### V1.38 & V1.39 
- fix problem with wifiTrax

### V1.36 & V1.37
- failed attempt to fix problem with wifiTrax

### V1.35
- add option to send commands twice

### V1.34
- minimum time separation/delay between commands sent

### V1.33
- changes to allow the use of VSC

### V1.32
- add support for 32 functions
- bypass WiT server search if EX-CS is in AP mode

### v1.31
- option to auto-connect to first SSID

### prior 
- various
