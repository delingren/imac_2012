# 27" iMac 2012 (A1419, EMC 2546) reuse project

Someone was selling this iMac on craigslist for $80. He claimed that the motherboard side of the display connector was busted when he tried to clean up the internal. So I jumped on it, hoping to convert it into an external display and docking station. When I was going to pick it up, the seller told me the connector on the display was damanged too and I could have it for free. I couldn't argue with free. So here we are.

## Disassembly
The screen is glued to the body with adhesive strips. The previous owner already opened it up for cleaning. If you have an unopened one, you could just heat up the edges, pry open with guitar picks, and life the screen with suction cups. There's plenty of youtube videos on this topic. Note that this one is different from 2011 models where the screen is mounted with magnets. There's also [this post](https://www.ifixit.com/Teardown/iMac+Intel+27-Inch+EMC+2639+Teardown/17828) on iFix for a similar model.

After examining the connectors, I suspect that it was only the cable that was damanged. So I ordered a video controller to give it a try. After I got the controller and hooked it up, the screen lit up without problems. Yay! So, I decided to embark on the whole project. This post documents the journey.

Here's the list of components I wanted to reuse:

* P0: LCD panel
* P0: Speakers
* P1: Camera
* P1: Microphone
* P3: PSU
* P3: RJ45 & USB 2.0 ports

I already know the LCD panel can be reused. The speakers should be relatively straight-forward. The camera looks a little problematic. The microphone is probably OK. I'd love to reuse the power supply if possible. But it's not a big deal if I can't. I'm also hoping to reuse at least the port openings on the back side for a few USB ports as well as the RJ45 for Ethernet.

```
DC to PD adapter

+--------------+
| USB Hub &    | -> | USB Ethernet adapter|
| HDMI adapter | -> | USB 2.0 hub |
+--------------+

Video controller

Crossover
```

## Display
## Speakers
![Crossover](crossover.svg)
## Power Supply
## Camera
## Microphone
## IO Panel
## Final Assembly