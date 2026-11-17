# Custom VR Controller guide 2026:

Warning: V0.2, not complete.

## Introduction: 

At long last, this is my guide on converting airsoft or almost any object to become a VR controller. 
This guide will split into two paths for the hardware section and also for the software part. 

The main issue with making these custom controller mainly lies in the software and firmware of VR headset hardware. 
They control and dictate the ability to hook into VR input and as a result, any sudden updates may suddenly cause anything to stop working. 

Since the project switched to Standalone headsets, this guide will not touch on the use of Vive Trackers as they are now obsolete going forward. 
However the main advantage they hold is ease of use for input i.e. no need for external software and lack of occlusion so they maintain tracking even when not in view of the player's headset. 
This could be a different guide one day. 

Hence I created a mechanical version that allows it to always work at the cost of using specific headsets i.e. Steam Frame. 

So at long last, guide begins now. 

## Hardware: 

The two routes for making the hardware are: Mechanical and Electronic. 

### Mechanical method: 

In this guide are a few 3d printed files, one you will use regardless of method and one specifically for mechanical activation of the Controller trigger. 
The files are made with Blender so you can CAD one yourself or adjust it in Blender. 

It is basically this: 

Pic. 1 show photo and diagram. 

You should print these parts slower and with high strength. I used PLA+ and Pro. 
I also recommend using airsoft DBAL-A2 mounts for quick detach. Feel free to modify the 3D files to suit whatever headset and orientation you need. 
My only warning is beware of using recoil in this manner. 
It will work but the risk of damaging the VR controller is much higher due to its closer proxmimity to the moving Bolt Carrier Group of your airsoft GBBR. 
For now this works on VFC/GHK/MWS or most AR shaped GBBRs. But can be adapted to other airsoft GBBR models which you can do yourself. 
Later on I will try this design on AK, G3 etc. 

I acknowledge my designs aren't very good or even decent so I look forward to your improvements. 

The two main mechanical methods are: 

Direct Trigger Linkage and Trigger touch linkage. 

**Direct Trigger Linkage:**
Direct trigger linkage so far only works on AR GBBRs due to the unique placement of the trigger pin hole. 
Show Pic 2. 

You will need to 3D print the specific trigger included so you can mechanically link the inch hex key to the mechanism. 
This design is honestly preferred as it is the mostly reliable however the issue arises with regards to the hammer bite placement i.e. when you print the trigger, the size varies depending on if it is for VFC or WA lowers. 
I haven't tried it, but 3d printing this would be ideal. Also beware of using the hex key as it will grind out the trigger pin hole over time. I recommend using a donor GBBR not a primary one. 

I would also recommend you do not install the hammer at first, to see if it works. 

**Trigger Touch Linkage:** 

Pic 3 show. 

This method is far more delicate as you need to adjust where the Steam Frame trigger activates but you can use it on any AR GBBR due to its external nature.
I recommend jerry-rigging a spring to make sure the arm goes back to its neutral position. 

I won't lie both of these designs are ugly and fickle at best but they do work. 
Later on, I plan to make mechanisms to activate various buttons on the controllers to allow GBBRs to do mag release, bolt catch etc. 

This method works best for specifically Steam Frame as it allows custom user controller offsets as you will need to turn the controller in-game 360degrees and move it up and down into position. This is the tricky part. 
The trigger activation would work on Quest 3 and any other VR headsets but the in-game offsets do not exist for Quest or Pico headsets so unless they update it, this remains unusable. 
Also this mainly only applies to standalone Steam Frame users who do not want to play with a PC. So now you can do free roam with your airsoft controller.

### Electronic method: 

This method is more convoluted but does offer far more satisfying trigger feel and response. 


Pic 4: show diagram of the layout and include pic of the actual itself.

This method is excellent and honestly I prefer and enjoy this more however, I mainly recommend this for only PCVR mods and self-made software. 
I will explain in the Software section but using this for mainline PCVR games puts you at the mercy of game devs and third party software. 
I mainly like the Steam Frame due to the possibility of creating an open source version of VR Input Emulator (by @matzmann) again and have it updated with current and future SteamVR version. 
But be warned if you choose this route, do not expect a smooth journey for PCVR games. 

Hardware wise you will need: 

-XIAO ESP32C6 or any ESP32C6. Make sure you set the Arduino IDE correctly. 
-Seeed Studio Grove board Mini. 
-Some HYP-2.0 cables with hooks. 
-3D printer or get someone to 3d print for you.
-Airsoft GBBR or AEG (duh). NERF is fine too or anything with 20mm NATO spec rail. 
-Battery bank or your own power source. I am not responsible for this but please use your own power bank with USB-C and use a safe one too. 
-Screws needed

I will gloss over the Arduino IDE setup as there are plenty of guides but I recommend this one: link here. 

I have uploaded non-AI written code to this Github and feel free to modify as you wish.
I also acknowledge the code isn't that good due to my non-programming background but I do recommend you leave the trigger pin to be its own block of code as that is the main button that needs to work. 

I also highly recommend you install HijelKB's BT keyboard library to make this work. Yes you are basically making your own mini keypad. 

I am in the process of testing out dongle methods like ZMK and ESP-NOW and even Nordic's own library to ensure 2.4ghz dongle connection for lowest possible latency. 
Will update this guide when that works. 

Also please pick a distinct BT name and basically connect it to your PC, Steam Frame, Quest or VR headsets that specifically support BT keyboard. Which it should since Android itself natively supports it. 

Include: Pic 4 correlating the wiring diagram with the code. 

For those who are more electronically inclined, feel free to add your own mini battery as XIAO ESP32C6 can handle charging and feel free to select your own pins to use and keyboard assignments. 
Also you can also use KiCAD to design your own PCB to handle pin input but I recommend sticking with Grove board as it has built in tabs to securely lock the wires to the pins. 
This is crucial for GBBR recoil. Previously i designed my own PCBs with USB-C as input but it quickly demonstrated how easily it shook out under recoil. 

However if you use the Grove boards your options narrow down significantly. Also ensure your wiring doesn't link to 3.3V as that causes the board to reset. 

Include: Pic 5, wiring diagram for the ports.

For now I recommend wiring buttons for: 
-TRIGGER (MUST!!!). H
-Reload . R
-Safety. M

Optional:
-Grab 
-Bolt catch. 

I also recommend using Gorilla Tack to secure the buttons (wired and soldered) to the receiver or behind the trigger. Feel free to experiment with the key assignments and placements. 
I have also included 3D Files for button holder and mounts for AR GBBRs. 

Explanation: 
How this works is extremely simple, it is basically a simple button switch, that's it. No more no less. 

Show Pic 5 of pins activating the code. 

For XIAO ESP32C6, i highly recommend using pins 1 to 11 only since last 3 pins are for GND and voltage output. 
Leave Pin 0 solely for analogue input in case of future possibilities.

Once you test it on your PC, open notepad or browser and check if the button types in the desired key input. 

Steps to pair: 

1. Make sure you have powered on your device.
2. Turn on BT in your PC or headset.
3. Select it to connect.
4. For password use 0000 or 1234
5. Once paired test it by typing into a search box or document. 


Now the hardware section is over, as you can see, this can be used to make almost anything into a VR controller or just normal controller. 
You can also replace this with a game pad library for more granular features but I chose keyboard as it was easiest to implement and more importantly has lowest latency as Windows already prioritises it for input natively. 

Also be wary atm, Steam Frame doesn't properly support BT keyboard and mouse, I know it should but as of 16/11/2026, it still doesn't work for me. 
But Quest 3 is fine, which means you can use this standalone as long as the game supports keyboard input natively!!

Also, beware of recoil, if you use GBBRs do not use full recoil constantly, it will destroy the IMU and gyro sensors of your controllers. I am not responsible for any harm you cause to your own equipment.
In my testing i found Marui NGRS recoil to be fine. But obviously not enough, again at your own risk. 

Future update to this guide will need a section about mechanical dampening. 

## SOFTWARE GUIDE: 

We are now entering what I would claim to be the hardest and most difficult part of making this work. 
The software is fickle due to constant updates potentially breaking SteamVR input functionality with regards to external hooks and access. 

I will write a separate guide on custom SteamVR drivers in the future once I improve my own programming skills and no I do not intend to vibe code it, I genuinely want to learn it for myself. Foundational knowledge like this is key and ironically, it is also good for training LLM AI to make your life easier going forward. 

So the software section is split into three paths: PCVR Native, PCVR Mods and Custom Software. 

They are ranked in difficulty as below: 
1. PCVR native. Hardest. e.g. Fallout 4 VR, Arizona Sunshine, H3VR etc.
2. PCVR mods. Easier e.g. RON VRO, UEVR mods, Titanfall 2 VR mod etc.
3. Custom Game. Easiest and best. 

Show pic 6 of software flows. 

### 1. PCVR Native guide: 

Long story short, you need to buy and use a program on Steam called Driver4VR. 
Currently that is the only 3rd party program that allows SteamVR to receiver VR input from a keyboard. Hence why this project now works for standalone. 
I hope to crowdsource a open version one day solely focused on input and offset management with profiles but until that day, this will work. 

For now, it seems to work consistently on Quest 3 only as the recent SteamVR updates have broken Steam Frame compatibility, it only worked for me once and it will require the dev to update frequently. 
If this ever stops working I recommend telling the dev on his discord page here: link to discord page for Driver 4VR.
Please be polite as his work is incredible and I wouldn't have gotten this far without it. I believe the price is very much worth it and do not rush him or make demands. He is busy with other aspect of his software as I believe custom input is not his main priority. 

### 2. PCVR Mods. 

Ironically, this is actually far easier to do. Mainly due to the fact most PC games to no one's surprise, natively support keyboards and have natively built in re-mappable inputs.
This one is obvious, just remap the LMB fire/shoot key to the keyboard binding of your choice. 
If this doesn't work i.e. RON VRO mod and Metro Exodus VR mod as some games specifically lock LMB to fire no matter what. 
That is an easy fix, use Auto Hot Key 2.0 (link here) and enter this simple code: write code here.
This will redirect your keymap to activate the LMB button. Be aware you need to turn this off for your key to work normally again. 

### 3. Custom Game. 

This one is also obvious and I won't write the guide here today. 
All game engines allow customisable input and for Unity, UE and Godot, that is 100% the case. 
For this part you will need to find your own way regarding your engine of choice. 
My future updated guide, may (emphasis on may) include a guide on each engine's way of using keyboard mapping to activate in-game actions. 
It is my favourite method as it allows all VR methods to work, so my custom game can use electronic input for PCVR and Standalone. 

I am sure Valve will fix the keyboard issue in the near future so it shouldn't be an issue when I update this guide in 2027. 


Now that the trigger inputs are done, it is time to focus on controller offset adjustments. 

Include pic 7 of the SteamVR UI and Driver4VR. 

The main issue with using Standalone controllers is the need to know its reference or datum orientation and position.
Vive Trackers (1.0 to 3.0), for all its faults, did have this nailed down. 

The issue is the 3d print file i included tries its best to fix the controllers to its reference orientation and position. 
Unfortunately it is a guess at best as I am basing it on the CAD files provided by Valve and Oculus. 

The issue is whether your game will obey them or not as most VR native games to change their own orientation for gameplay reasons. 

I use Driver4VR more often as it has easy adjustments with mouse clicks so i can see it move in real time making it easier to line up the in-game mesh with physical airsoft controller. 

However for standalone, you must use the built in SteamVR offset adjustment hidden in this menu(see pic 7). 

This one is genuinely difficult and a real bother to use, i can only hope valve fixes it. This one is truly to each and their own. 

I wish you all the best. 

For starting reference this is what I would do:

1. Start by Adjust the pitch, yaw then roll axis. Roll is the most dangerous axis as it creates the biggest adjustment issues. Hence my mount tries to lock off roll but with limited success. It works on Quest 3 controllers but not Steam Frame.
2. Then use X, Y and Z to move it into place. Beware of the forward direction, you may experience coordinate zig-zagging to move it into place.

Make sure to keep unpausing your game and check if its lining up. Do your best. 

In the future I would like to create a passthrough view so the 3d mesh can line up exactly with the physical controller with granular adjustments for angle and position. 
There is a vibe-coded Steam Frame app called UTFTBF(correct it) to do quick adjustments so there is hope yet for a better one in the future. 

**Conclusion

This concludes the guide, as you can see, its mostly a technological parlour trick. 
Technically there was nothing difficult apart from figuring out SteamVR driver inputs. 

Please go forth and do whatever you want, just please open source your version and share it around. 

I owe this entire project to people who laid the path before me and I hope to do the same for future generations.

Thank you to @matzmann for his role when making OpenVR IE in 2017, it truly began my journey down this road. 

I am proud to stand on the shoulders of giants. 

Good luck and all the best!!




## Safety and Liability Disclaimer:

The user assumes the risk of undertaking this open source guide. This guide is provided only as an educational guide for the purpose of learning and research. It is provided as is, no form of guarantee or warranty is ensured, expressed or implied.

This project and resulting device has had no certification by any regulatory body or organisation i.e. RoHS, FCC, CA UK or CE. The user i.e. reader or project maker is solely responsible for all risks they under take.

The author is under no liability under any circumstances for any injury, harm, loss, damage arising of their attempt to carry out this project. Do at your own risk!!!


## Open Source License:

This project is published under the CERN OHS-L 2.0 Open Source Liccense.
Copyright November 2026 belonging to ProgrammingBandito. 

This project including all software and hardware files and guide are licensed under the **CERN Open Hardware Licence Version 2 - Strongly Reciprocal (CERN-OHL-S-2.0)**. 
