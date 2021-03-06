# OSC from Python to Pure Data 

alx-s

12-03-2013

## Context 

Once again I'm using the Raspberry Pi to do some cool stuff. 
The idea here is to collect data from sensors and use them to generate sound synthesis.
Tricky part is: data is collected using python (using python's RPi.GPIO https://pypi.python.org/pypi/RPi.GPIO) while sound synthesis is generated with pure data. We therefore need to make them communicate with each other.
To do so we're gonna use Open Sound Control (OSC).

If you want to know more on the subject of OSC I recommend you take a look either here : 
http://opensoundcontrol.org/ 
or there : 
http://en.wikipedia.org/wiki/Open_Sound_Control

## How to install everything

The installation takes place from begining to end in the terminal. Every command written below should be typed there.

### Python.

To achieve this goal I chose to use pyOSC.
You can find it directly on gitorious : http://gitorious.org/pyosc

Once in your Raspberry Pi start by cloning it:

```shell
git clone git://gitorious.org/pyosc/devel.git
```

Installation is then quite simple :

```shell
cd devel
sudo ./setup.py install
```

### Pure Data

If you're using Pd-extended you won't have to deal with the rest of this section. 
For those, like me, who use pd vanilla, here is what needs to be done.

First, let's install the iemnet lib which is needed to deal with data transfer (to do so you will need git or you can get the zip there : https://github.com/umlaeute/pd-iemnet) : 

```shell
git clone git://github.com/umlaeute/pd-iemnet.git
```

You should also be able to download it on the pure data website : http://puredata.info/downloads/iemnet . Nevertheless, I've had problems trying to compile it.

After cloning the repository it simply goes this way :

```shell
cd pd-iemnet
make
sudo make install
```

We then need one last component which is the one managing OSC messages. This library is simply called OSC and compilling it goes this way:

```shell
wget http://puredata.info/downloads/osc/releases/0.1/OSC-0.1.tar.gz
tar -xzvf OSC-0.1.tar.gz 
cd OSC-0.1/
make
sudo make install
```

That's all we need this far, time to move on to the actual fun!


## Code 

Both the python code and the pure data patch are quite simple. You will find them right in this directory.

OSC_send_python.py and OSC_receive_pd.pd work together to transmit data from python to pd. Sending data from pd to python is illustrated when using OSC_send_pd.pd with OSC_receive_python.py.

You can notice that my pd objects specify the library they are using (ie: OSC/...). With pd-extended this won't be needed. With pd vanilla and the startup path correctly set up it won't be needed either. 


## Conclusion

We've been through everything we need to transmit data between python and pure data.
Lots of other functions are available when using OSC but I didn't need them so far, I let them for you to discover!












