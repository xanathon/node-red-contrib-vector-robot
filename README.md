# node-red-contrib-vector-robot

## A Node-Red Contribution for the Anki Vector Robot

This is a fork by the original [Node-RED](https://nodered.org) contribution by dastultz (Node-RED is a graphical user interface to create workflows, follow the link for details). I forked it to try to get it to run on a more recent version of Node-RED and to remove some errors from the original code. But anyway: Thanks to dastultz for creating this and sparing me a lot of work on the basics.

**it has to be noted that I am quite new to Node-RED so not everything I do here may work - or it may break something. You have been warned. Use at your own risk. :) Backup your Node-RED.**

Prerequisite: **You will need to have your Vector (or Vectors) already authenticated with the Python SDK so you have retrieved the cert and tokens on the computer you want to use this!** (or you can copy the cert and token files manually from another computer).

You want an example what can be done with this? Here:

In my first test I was able to get a carbon dioxide reading from one of my Netatmo sensors and if it is above 900 ppm, Vector tells me so, so I can let fresh air in. The possibilities are endless (Caveat: there seem to be connection timing problems, see at the end of this readme. Another caveat: one of the libraries is reported as outdated, I have to update it to a newer one).

## Installation into Node-RED

To install this from github you have (for now) to download the code as zip, unzip it and rename it from,

`node-red-contrib-vector-robot-master`

to 

`node-red-contrib-vector-robot`

after that you copy that folder into the node_modules folder, ususally this is something like

`/home/username/.node-red/node_modules`

on Linux, or

`C:\Users\username\.node-red`

on Windows (unfortunately I cannot tell you where this is on Mac OS, since I do not own a Mac).

after that you have to open a console cd to that folder and issue the following command:

`npm install`

That downloads and installs neccessary dependencies and the Vector nodes will show up in the Node-RED UI after it finished.

## Configuring Vector.

In Node-RED you will have to configure your Vector. 

Prerequisite: You will need to have your Vector (or Vectors) already authenticated with the Python SDK!

The token an cert files for your Vector(s) can be found in

`/home/username/.anki-vector`

on Linux, or

`c:\Users\username\.anki-vector`

on Windows.

Here you will find a cert file for every one of your Vector you authenticated with  the Python SDK (or Cyb3rVector or Vector Explorer).

They are named after this scheme:

`Vector-R2D2-00000000.cert`

Where the 8 zeros of course in reality are only placeholders for a hexdecimal code and the same as your robot's serial.

Also there is a file called

sdk_config.ini

In it you will find an entry for each of your robots, starting with the serial in brackets and then other information in the following format:

`[00000000]`

`cert = C:\Users\admin\.anki_vector\Vector-R2D2-00000000.cert`

`ip = 192.168.178.56`

`name = Vector-R2D2`

`guid = abcdefXYZaBcDE21fZkvgG==`

The order of the data fields may be different, that is okay.

For the usage in Node-RED, or to be more precise to configure your Vector, you need the robot name, the IP adress (please notice that the actual IP adress of your robot may be another one),  the GUID (called "bearer token" in the config node) and the cert path. it took me some kind to find out what exactly is what and goes where, so I want to spare you the challenge:

<img src="/gitimg/configure_node.jpg" width="500" />

That's it for configuration (for now), you can now user the Vectort nodes with the configured Vector Configuration node.

More to come (especially more detailed explanations on using this).

### Below is the original text from the project I forked fom dastultz:

Vector is a home robot developed by Anki and taken over by Digital Dream Labs. The official SDK is in Python. I do not favor JavaScript over Python (or vice-versa), however I really wanted something that would integrate with Node Red. This is the beginning of a JavaScript SDK. It is not intended to be scripted in JavaScript but there's no reason you can't do that. It is designed to be run from Node Red.

Presently there are 9 nodes for some basic behavior and event monitoring. Using Node Red it is super easy to hook up the event stream to a browser-based UI graphing battery voltage over time, for example. I have connected my home automation system. Vector just told me it's getting late and my garage door is still open.

I had hoped to make this a great thing, but I have decided it's too much work for me to take on so I offer this to the community with the hopes someone will run with it.

Presently I am struggling with "longevity". I have a Linux server in the house running Node Red. There is no problem with Node Red running 24x7, but the connection(s) to Vector tend to fail after some time, and a number of different attempts to reconnect have not proven fruitful. I have found that the same happens with the official SDK in Python, so it may be a general problem with Vector or I'm doing the same thing wrong with both models. It would be great if someone who understands the underlying gRPC protocol better could get this working more robustly.
