# OSC Communication in Python __ RaspberryPi

***OSC (Open Sound Control)*** is a network-based messaging protocol used to transmit numeric and textual data between devices or software processes.


Like it’s older sibling - MIDI, OSC was originally designed for music performance contexts, but it is now widely used across many disciplies. Just a few examples of softwares with OSC capability include Ableton Live, Reaper, Max, Pure Data, QLab and Unreal Engine.

In this tutorial, **we will create a simple local OSC server** that follows the OSC protocol. This is a Python programme that runs on the RPi and listens for incoming OSC messages and reacts to them. 

You can think of an OSC server like a radio receiver: where the port is the frequency it is tuned to, the OSC address is the type of message it reacts to, and the data is the content of the message.

**You can think of an OSC server like a radio receiver:**

- the ***port*** is the frequency it is tuned to,

- the ***OSC address*** is the type of message it reacts to, and

- the ***data*** is the content of the message.


**Our OSC server will:**

- listen on a specific port number, and

- respond to messages sent to specific OSC addresses (for example, /test).




Read more about OSC [here](https://itp.nyu.edu/networks/explanations/open-sound-control/)

----
### Python-OSC

Python-osc is a Python library that allow us to send and receive data via OSC. 

Read more [here](https://pypi.org/project/python-osc/)

----
### Virtual Environments

Activate your virtual environment.

Read more [here](https://github.com/kingston-hackSpace/Virtual-Environments__RaspberryPi).

----
### Install Python-osc Library*

- Open the Terminal and type:

      pip install python-osc

----
### Create a simple OSC server

