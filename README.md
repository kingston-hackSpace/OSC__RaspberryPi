# OSC Communication in Python __ on RaspberryPi

***OSC (Open Sound Control)*** is a network-based messaging protocol used to transmit numeric and textual data between devices or software processes.

Like it’s older sibling - MIDI, OSC was originally designed for music performance contexts, but it is now widely used across many disciplines. Just a few examples of software with OSC capability include Ableton Live, Reaper, Max, Pure Data, QLab and Unreal Engine.

Read more about OSC [here](https://itp.nyu.edu/networks/explanations/open-sound-control/)

---
## OSC Roles

In OSC communication, there are two key roles: CLIENT AND SERVER

### 1. OSC Server

An **OSC server** is a program that **listens** for incoming OSC messages and reacts to them.

- Listens on a specific **port number**  
- Responds to messages sent to specific **OSC addresses** (e.g., `/test`)  

**Analogy:** a radio receiver
- **Port:** frequency it is tuned to  
- **OSC address:** type of message it reacts to  
- **Data:** content of the message  

### 2. OSC Client

An **OSC client** is a program that **sends** OSC messages to a server.

- Sends data to a specific **IP address** and **port**  
- Uses OSC addresses to indicate the type of message  
- Sends numeric or textual values  

**Analogy:** a radio broadcaster — sends messages, which only servers tuned to the correct frequency (port) and channel (OSC address) can receive.

----
## How Client and Server Work Together

| Role        | Function           | Analogy          |
|------------|------------------|----------------|
| OSC client | Sends messages    | Broadcaster     |
| OSC server | Receives messages | Radio receiver  |


----

# TUTORIAL

----
### Virtual Environments

First, activate your virtual environment.

```
cd Desktop
source venv/bin/activate
```

Read more [here](https://github.com/kingston-hackSpace/Virtual-Environments__RaspberryPi).

----
### Install Python-osc Library*

Second, download the Python-osc Library. It will allow us to send and receive data via OSC. 

Read more [here](https://pypi.org/project/python-osc/)

- Open your terminal, and once inside your venv, type:

`pip install python-osc`

----
### Create a simple OSC Server __ Python file

- Go to the Desktop and create an OSC directory

```
cd Desktop
mkdir -p OSC
cd OSC
```

- Create a new Python file called osc_server.py:

`nano osc_server.py`

- Paste the following code into the editor:

```python
from pythonosc import dispatcher
from pythonosc import osc_server
        
def print_message(address, *args):
    print(f"Received {args} from {address}")
        
disp = dispatcher.Dispatcher()
disp.map("/test", print_message)
        
server = osc_server.ThreadingOSCUDPServer(
    ("127.0.0.1", 5005),
    disp
)
        
print("OSC Server is running on {}:{}".format(*server.server_address))
print("Waiting for messages...")
```
        
server.serve_forever()
        
  - Save and exit:

```
Press CTRL + O → Enter

Press CTRL + X
```

- Test that you can run your osc_server.py

`python3 osc_server.py`

- The terminal will display:

```
OSC Server is running on 127.0.0.1:5005
Waiting for messages...
```

- The server is now listening for OSC messages.

----
### Create a simple OSC Client __ Python file

- Without closing the previous Terminal window, open a new terminal window and type:

```
cd Desktop
source venv/bin/activate
nano osc_client.py
```

- Paste the following code:

```
from pythonosc import udp_client
import time

client = udp_client.SimpleUDPClient("127.0.0.1", 5005)

for i in range(5):
    client.send_message("/test", i)
    print(f"Sent {i} to /test")
    time.sleep(1)
```

- Save and exit (CTRL + O, Enter, CTRL + X).

- Run the client while the server is running in another terminal:

`python3 osc_client.py`

- You will see the numbers 0–4 printed in the server terminal as they arrive.

Success! you have sent messages from one program to another via OSC protocol.

----
### NOTES

- Two terminals are needed: one for the server, one for the client.

- 127.0.0.1 = local machine. If you want to run the client on another Pi, replace with the server’s IP.

- The port (5005) must match in both scripts.

- The OSC address (/test) is like a channel; the server reacts only to messages sent to it.
