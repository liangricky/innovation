
# Overview

`Humix` is an open source robot connectivity and design framework that make it easy to 
bridge cloud API with hardware sensors and devices. Combining with Watson APIs, 
the framework help everyone, from kids and enterprise, to build their own cloud-brained robot with a few minimal steps.

The goal of Humix ( HUmanity & blueMIX) is taking the best part of IBM cloud offerings to provide a software skeleton 
for building a robot.It leverages NodeRed as the flow-editor for designing how the robot behaves. On top of NodeRed, 
a few new nodes are added to support Humix’s module programming model, as well as to make it easier to connect with 
the commonly used messaging channel ( Facebook Node ). 
As to connectivity, Humix offers two options : one is based on Watson IoT architecture, and the other is based on WebSocket.
If there is one-to-one mapping between a physical robot and it’s cloud-brain, then WebSocket would be sufficient 
for most cases. But using Watson IoT framework would make it more flexible to scale ( e.g. one brain for multiple robots ) 
and integrate with other IBM IoT Services, such as IoT Realtime Insight.

#Architecture 

Essentially, Humix consists of two major components - Humix Think and Humix Sense. 
`Humix Think` is the cloud-side component that embeds a NodeRed flow editor for design robot behaviour. 
`Humix Sense`, on the other hand, is located on the device that acting as a robot. 
Humix Sense use `NATS` as local messaging framework for all registered Humix Modules 
to send sensor events and receive the commands. Humix Sense would monitor the local messaging bus 
and deliver the messages to cloud for further processing. 
With Humix Sense, each could focus on its own logic without worrying about how messages 
are sent to Humix Think for further processing. This micro service architecture make Humix an extensible 
module systems that could be enhanced incrementally.
Currently the core Humix module that comes with Humix framework is ‘humix-dialog-module’. 
This module leverages Watson Speech recognition to support basic interaction with robot. 
People can also choose to use google services if that is a preferable option.



# Setup Your Humix

In general, the highlevel steps you need to setup a Humix-based robot are

0. Prepare your hardware. The project use RPI 2 as default device. You can download a pre-build image from [here](http://119.81.185.45/humix_image/20160330-humix-jessie-alpha.img.gz). 
   Connect your RPI 2 with speaker microphone. 
1. deploy Humix Think on Bluemix 

2. deploy Humix Sense on your device acting as robot. 
  * Config $INSTALL_DIR/sense/config.js with Humix Think URL and the id of this robot
  * Config $INSTALL_DIR/sense/modules/core/humix-dialog-module/lib/config.js. 
    Provide the username and password for Watson Speech-Recognition-Service.

3. Launch Humix Sense  

For details steps, please refer to [humix-doc](https://github.com/project-humix/humix-docs) repository 




# Copyright and License

Copyright 2016 IBM Corp. Under the Apache 2.0 license.


