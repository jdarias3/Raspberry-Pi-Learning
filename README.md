# Raspberry-Pi-Learning

How to use the Raspberry Pi

### Introduction


### Installing OS images
1. Download the OS to use on the Raspberry, go to the official website and select the OS you desire. (If you are starting with Raspberry Pi and Linux, you can choose **Raspbian**, it is the the Foundation’s official supported operating system.
https://www.raspberrypi.org/downloads/
	
2. Now we need to write the image to the SD card, we can use **balenaEtcher** software that is supported in Linux, Mac and Windows (it supports writing images directly from the zip file, you don't need to use an unzipping software) to write the image to the SD card.

	2.1. Download [balenaEtcher](https://www.balena.io/etcher/)and install it.
	2.2. Connect the SD card on your computer.
	2.3. On balenaEtcher, select the .zip or .img file
	2.4. Select the SD card to write the image
	2.5. Then press in Flash! and wait until shows **Flash Complete!**

Note: I selected the image *Raspbian Buster Lite*.
			
## First booting
1. After the first booting, it will ask you the username and password. By default the username is **pi** and password is **raspberry**, we will see how to change those later.
2. As I used the image *Raspbian Buster Lite*, after type the username and password, I got the terminal prompt, so we will make our first configurations steps:
* The first command we will use is 
 `$sudo rasp-config`
	 it will open a graphical interface to check and change the Raspberry configuration.
* Here is the changes I made:
	 * On *Change User Password*, changed the password for user **pi** (this configuration change is very importar for security reasons, try to don't skip this step and use a different password)
	 *  On *Network Options*, I keep the same Hostname and selected a Wifi connection.
		 * On the Wifi connection, first it will ask you for the country in which the Pi is to be used, select your country, the it will ask you for the SSID and then for the password.
	 * On *Boot Options*, you can select to boot into a desktop environment or the command line, I selected keep into command line.
	 * On *Localisation Options*, you can chane the language and regional settings, time zone and keyboard layout. I just changed the Timezone to CST.
	 * On *Interface Options*, enabled the following:
		 * SSH, to enable remote command line access using SSH
		 * VNC, to enable graphical remote access using RealVNC (To enable this options, you need Internet connection)
	 * On update, you can update the Rasberry Pi Configuration Tool.


In the distribution I have installed, it doesn't have the graphical interface pre-installed, here is the process to install it, we need internet connection, if you already configured the Wifi access you are good, but I don't have Wifi connection at the moment so I will show you how to check our Ethernet connection on the Rapsberry Pi:

To check if we have connection to the network, use the following command:

    $ ifconfig

It will show the 3 connections:
	- eth0 : Ethernet Connection
	- lo: Loopback Connection
	- wlan0: Wireless Connection 

I have connected the Ethernet cable to the Pi and run the command, as result I can see the eth0 is UP and I have IP address. I will try to update the Pi to then install the Graphical interface environment:

To update the and upgrade use the following command:

    $ sudo apt-get update && upgrade -y

After run the command I cannot get the Pi be updated, and it is because I need to use a proxy settings to my connection to the network (maybe you won't have this issue in your environment), to configure the Proxy on your Pi follow the steps below:

1. Open the file *environment* located in */etc/*, to edit the file use the text edito **nano**:

    `sudo nano /etc/environment`

2. Edit the file and add the proxy configuration:

```
export http_proxy="http://proxyipaddress:proxyport"
```

Replace the proxyipaddres for the real *IP address or URL* and replace the *proxyport* for the port of your Proxy.

If your proxy requieres username and password, here is the command you should use:

```
export http_proxy="http://username:password@proxyipaddress:proxyport"
```
If you proxy is HTTPS base, you have to use the following command:

```
export https_proxy="http://username:password@proxyipaddress:proxyport"
```

And for the addresses you don't need proxy:

```
export no_proxy="localhost, 127.0.0.1"
```

In order to use the proxy configuration in the operations that needs to run with **sudo**, we need to make the following changes:

1. To open the sudo configuration, use the following command:
```
sudo visudo
```
2. Add the following line to the **sudo** file use the proxy environment variables created.
```
Defaults    env_keep+="http_proxy https_proxy no_proxy"
```

Now reboot your Pi `$sudo reboot`

Finally, I have internet connection to install new software in my Pi and it is updated.

We are ready, we have our Rasberry Pi with our initial configuration, you can keep working in the command line interface or you can move o the graphical interface. To move from command line to graphical interface, you can use the following command:

```sudo apt-get install raspberrypi-ui-mods```

I selected **Raspberry Pi Desktop (RDP) GUI**, and the installation requires 878 MB on the SD.
