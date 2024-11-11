# 27" iMac 2012 (A1419, EMC 2546) reuse project

* iMac 2012
* Model: A1419
* EMC: 2546
* [Spec](https://everymac.com/systems/apple/imac/specs/imac-core-i5-2.9-27-inch-aluminum-late-2012-specs.html)

Someone was selling this iMac on craigslist for $80. He claimed that the motherboard side of the display connector was busted when he tried to clean up the internal. So I jumped on it, hoping to convert it into an external display and docking station, which doesn't need the motherboard. When I was going to pick it up, the seller told me the connector on the display was damanged too and I could have it for free. I couldn't argue with free. So here we are.  I thought I'd give it a try, hoping that the damaged pins are NCs.

## Disassembly
The screen is glued to the body with adhesive strips. The previous owner already opened it up for cleaning. If you have an unopened one, you could just heat up the edges, pry open with guitar picks, and life the screen with suction cups. There's plenty of youtube videos on this topic. Note that this one is different from 2011 models where the screen is mounted with magnets. There's also [this post](https://www.ifixit.com/Teardown/iMac+Intel+27-Inch+EMC+2639+Teardown/17828) on iFix for a similar model.

After examining the connectors, I suspect that it was only the cable that was damanged. The connector actually looked OK under a magnifier. So I ordered a video controller to give it a try. After I got the controller and hooked it up, the screen lit up without problems. Yay! So, I decided to embark on the whole project. This post documents the journey.

Here's the list of components I wanted to reuse:

* P0: LCD panel
* P0: Speakers
* P1: Camera
* P1: Microphone
* P2: RJ45 & USB 2.0 ports
* P3: PSU

I already know the LCD panel can be reused. The speakers should be relatively straight-forward. The camera looks a little problematic. The microphone is probably OK. I'd love to reuse the power supply if possible. But it's not a big deal if I can't. I'm also hoping to reuse at least the port openings on the back side for a few USB ports as well as the RJ45 for Ethernet.

## Display
The model of the LCD panel is LM270WQ1(SD)(F1). Here are the [specs on panelook](https://www.panelook.com/modeldetail.php?id=18520). You can find the datasheet in this folder.

* Resolution: 2560(RGB)×1440, Quad-HD  108PPI 
* Signal Type: eDP (4 Lanes) , 40 pins Connector
* Backlight: 3 strings WLED , 30K hours , No Driver

 I ordered a [controller](https://www.aliexpress.us/item/3256807252731476.html) from AliExpress. If the link doesn't work anymore, just search for the model number. It's powered by RTD2556, a rather popular eDP driver chip. The unit comes with a separate backlight driver board. All other WLED panels I've seen don't need it; the driver would be already on the video controller. My guess that the WLEDs on this panel uses a different voltage and the extra board has a buck-boost converter.
![BL driver](bl_driver.png)

The backlight connector that came with it is a pain in the neck to push into the one on the LCD panel side. And the connection is rather wobbly. So I decided to cut off both connectors and solder or crimp the wires to a new connector and connect it directly to the backlight controller. 

![BL Connector](bl_connector.jpeg)


## Speakers
![Crossover](crossover.svg)

## Camera
Originally, I wanted to reuse the camera. But after opening up the machine and reading the schematic, I realized that camera doesn't have a USB interface. Instead, the controller chip is on the motherborad. The camera talks SMIA. I have no expertise in decoding the protocol, although it's an open standard.

So I decided to get a tiny USB camera module, hoping it'd fit in the tiny space. If that doesn't work, I could always use an external webcam. It's not as aesthetic. But I'm not that picky.

After some research, I came upon this camera sensor ov5693. I also found [boards](https://www.aliexpress.us/item/3256805396719075.html) on Aliexpress that drive the sensor and turn it into a USB device. Then I 3d printed a bracket to fit the sensor into the place evacuated by the original camera, which is quite a challenge, since the space is very packed.

![camera mount](camera_mount.jpeg)

## Microphone
Originally, I also wanted to reuse the microphone. It looks like a MEMS PDM microphone. However, the original connector seems to have a short and I can't figure it out without damaging it. It's a 0.4 mm pitch 6 pin connector. I have no idea where to find a replacement. So I figure it's easier to just replace it altogether. And I'm replacing the camera anyway. So I might as well remove everything in that space.

## IO Panel

The original IO panel has openings for 4 USB A, 2 mini DP, and 1 RJ45 ports. I have no use for the mini DP ports. But I need a USB C female connector. So I decide to cut the bridge between the two mini DP ports to make it big enough for the USB C connector.

I really wanted to provide an Ethernet adapter.
 I found this [RJ45 socket](
https://www.aliexpress.us/item/3256806005093192.html) on Aliexpress. I then crimped the wires into a male plug, making it into an extension cable. Then I just need to use a USB Ethernet adapter.

![RJ45 socket](rj45_socket.jpeg)

## Power Supply
The PSU provides a 12V rail `G3H`, which is always on. Other voltages and rails are done on the logic board. So that was easy. I just need to cut the original wires and solder my own. Here's an excerpt from the logic board shcematic.
![PSU](psu.png)

The PSU has a buzzing noise though. Not sure how bad it'll be when running. We'll see.

## Final Assembly