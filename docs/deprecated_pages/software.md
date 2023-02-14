## Ubuntu+Octoprint+Motion

Hey everyone!

I've spent the past few hours configuring and setting up octoprint to work on my Kobra Go (KG). I learned quite a lot through this process, and figured someone else may want to do something similar. I know octoprint is usually installed on a pi, but those are currently unavailable and/or being scalped for 2-3x MSRP. I've made it through the GPU shortage and dont want to bother with another! Anyways I found an old lenovo circa 2016 and threw Ubuntu on it.

Host Info:
```
2016 Lenovo Ideapad

Intel Pentium 4405U (2C/4T)

8GB DDR3

Ubuntu 22.04.1 LTS
```
I followed the, "The Slightly Tricky Way", part of [this guide published by ALL3DP](https://all3dp.com/2/octoprint-linux-ubuntu-tutorial/){target=_blank}. After doing most (I just realized now, typing this, that the tutorial does in fact mention adding the user to the correct groups. That'll be relevant later, woops!**) of those steps I noticed that my printer wasn't showing up in the devices list.

Seeing this I took a look at dmesg to see what it was doing:

    sudo dmesg | grep tty

It turns out that a plugin, 'brltty', was causing my printer to connect, register on the bus, then disconnect. I found a solution here, which was to uninstall brltty:

    sudo apt remove brltty

After that I rebooted the machine, thinking surely it'd be a quick connect and off to the printing wonderland. Unfortunately this wasn't the case; Octoprint saw the printer in the usb port, but could not establish a connection. I again checked dmesg to see if the printer had been recognized, thankfully it was. Yet octoprint would fail on auto detect, but hang when I selected a baud rate. It turns out it was just a permissions issue!** During the steps to install octoprint, a new user, octo, was created with minimal permissions. In order to allow 'octo' to read the USB devices and access them it must be added to the 'dialout' group via:

    sudo adduser octo dialout

After doing that the auto connect worked! I got my KG to connect automatically with a baud rate of 115200.

One of the awesome features of octoprint is camera monitoring, which the laptop has built in via the webcam. Unfortunately, octoprint doesn't support native cameras but instead supports viewing a stream from some camera. This is where things get a little more interesting, so I'm going to move to step-by-step:

Login to your host as the normal user (not octo).

Install motion:
    
    apt install motion

Set motion to be started automatically on boot:
    
    sudo systemctl start motion

Restart your host.

Find where motion is hiding its master config file, normally it is in:
    
    /etc/motion/motion.conf

Edit the config file with sudo privilege:

    sudo nano motion.conf

In the file find the following lines and change them:

move_output, on or off, toggles writing video clips to your host.

    movie_output off

stream_port specifies the port that motion will use for the stream, can be any integer

    stream_port 1566

stream_localhost sets if other computers on the local network can see the stream, off for public on for private

    stream_localhost off

stream_maxrate sets the frame-rate for the stream.

    steam_maxrate 30

stream_quality is pretty self explanatory, it goes from 0 to 100.

    stream_quality 50

stream_preview_method look to the documentation to decide on this one.

    stream_preview_method 4

Save this file by pressing ctrl+x

Restart the motion service:

    sudo systemctl restart motion

In a web browser type in the IP of your machine and the port specified in the config file, as an example: 

    192.168.53.234:1566

The stream should now show up! Full motion, full color video!

Now we can go to the octoprint settings, to 'Webcam & Timelapse", and enter the previous URL into the 'Stream URL' section.

Hit test and watch!

So thats how I went about using an old laptop and integrated webcam to monitor my prints with octoprint!

### Followup 
I have since moved on from octoprint and installed Klipper. Alongside Klipper I've added an Arducam OV5647 which is mounted to the frame of the Go for a much better viewing angle.
