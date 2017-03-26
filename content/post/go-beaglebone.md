+++
title = "Get started with BeagleBone"
Description = ""
Tags = ["iot"]
Categories = []
date = "2017-03-26T10:20:55+01:00"
+++

# Get started with BeagleBone

I have to admit, the power of IoT did not yet reach my little nerd life here in Berlin. Therefore, I took an effort this year and went to an IoT Hackathon. It was a fun weekend, I think there were just 5 developers and the rest of the crowd came from a social and educational background. Which made it even more fun and interesting.

Anyway, since this weekend I ordered a RaspberryPi and tried to do something useful with it. This idea, and my other habit of simplyfing my life clashed a little bit. So the RaspberryPi sat around for way too long with no real purpose. After browsing the internet though, I found an interesting <a href="https://blog.sayan.ee/bbb">post from Sayan who set up a BeagleBone board with Go</a>. After React, Go is one of the new technologies I really like. After reading the article, I ordered the BeagleBone Black Wireless and waited impatiently for it to arrive.

Finally there, I did around 4 hours of trial and error to finally figure out how this little board works and what I have to do. Mainly, I wanted:

- Install Debian on it
- Booting it without the need of a SD Card
- Run a Go server or something useful on it

At the Hackathon back then, I created a temperature and noise dashboard (<a href="https://github.com/gruberb/IoTHack16">code is on GitHub</a>). Maybe the BeagleBone could do the same for me at home?

During this simple steps, I bricked the device twice, found some old post in some forum how to rebuild it and now I have working BeagleBone Black Wireless. In addition, I installed my own Go server on it to access it without a USB connection.

## Sane HowTo (without the errors)

1. Connect the BeagleBone with your Mac, wait until it's booted, and then open the newly mounted Volume. In it, you find two drivers for the Mac you need to install before you can continue.

1. Afterwards, there is a "Flasher" version of Debian for the BBB. It will install the OS on the emmc of your board so you don't need the SD Card every time you boot. I had problems finding a proper "Flash-Debian-EMMC-Version". I tried a bunch of different ones, but nothing seemed to work. So I recommend this image here:

```wget https://rcn-ee.com/rootfs/2017-03-09/flasher/BBB-eMMC-flasher-debian-8.7-console-armhf-2017-03-09-2gb.img.xz```

2. Download it, and then unarchive it with Unarchiver for Mac or 7zip.

3. You can now use your Terminal to create a working SD Card with this image, or <a href="https://etcher.io">just use this tool</a>.

```sudo dd if=BBB-eMMC-flasher-debian-7.5-2014-05-14-2gb.img of=/dev/disk2s1```

To find out the name of the SD Card, insert it and execute:

```df -h```

4. Power off your BeagleBone Black, unplugg the power/usb cord, and insert the SD Card. 

5. Hold down the S2 button, and while holding it down, plug the power/usb cable in.

6. The LEDs need to light up at least once, afterwards you can release the S2 button again.

CRITICAL: This step 6 didn't work for me in a long time. What I did was to find the right image, and during this process plug the BeagleBone onto a power outlet and NOT via the USB cable in the Mac. 

7. The LEDS are doing now some crazy things, lighting up in order 1-2-3-4-3-2-1-2... 

8. The system is shutting itself down.

9. Plug the BeagleBone back to your Mac, wait until it's booted, and then look at the right IP address in the network settings of your Mac.

10. Open the Terminal and execute this command (with the right IP address)
```ssh debian@192.168.6.2```
 
11. The password is ```tmppwd``` and can be changed.
 
Voilà, you have a working BeagleBone Black Wireless! 
   