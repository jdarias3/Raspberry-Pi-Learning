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

and to use the proxy in apt-get

``Acquire::http::Proxy "[http://yourproxyaddress:proxyport"](http://yourproxyaddress:proxyport%22/);``

in a file placed in /etc/apt/conf.d (named similar to "10proxy" for example). It should also work when placed in /etc/apt/apt.conf but I don't remember if this file still exists on the latest Raspbian.

Now reboot your Pi `$sudo reboot`

**Note:** If you want to remove the proxy configuration, just access to the *environment* file and add a **#** at the beginning of each line and reboot the Pi again.

Finally, I have internet connection to install new software in my Pi and it is updated.

We are ready, we have our Rasberry Pi with our initial configuration, you can keep working in the command line interface or you can move o the graphical interface. To move from command line to graphical interface, you can use the following command:

```sudo apt-get install raspberrypi-ui-mods```

I selected **Raspberry Pi Desktop (RDP) GUI**, and the installation requires 878 MB on the SD.

After the installation, you need to reboot the Pi and by default, you will go to the graphical interface. Now you have access to the graphical interface and you can start building your projects.

Now I will show you some configuration changes I made:

1. I prefered to use the command line interface on the boot, since I connect to the Pi throught SSH and make the changes. On the graphical interface I opened the terminal and access to the Raspberry configuration using the command ``$ sudo raspi-config`` 

On *Boot options*, I selected the option to **Console Boot**, so in the next boot of the Pi, it will boot on the command line interface.

After next boot, we are on the command line interface and start working, if you want to go to the Graphical interface use the following command:

``$ sudo systemctl start lightdm``

# Programs to install

``$ sudo apt-get install git``
For proxy to git

``git config --global http.proxy http://proxyUsername:proxyPassword@proxy.server.com:port
``

``$ sudo apt-get install vim``

Adding proxy on PIP
``pip install <name_of_module> --proxy [user:passwd@]proxy.server:port``

**VS CODE**

Follow the steps below:
1. Install the dependecies if you have not installed:

```$sudo apt install apt-transport-https```

2. Open an interactive session:

``$sudo -i
. <( wget -O - https://code.headmelted.com/installers/apt.sh )``

3. Install VS Code

``$sudo apt install code-oss``

On March, and error on Raspberry PI was reporter in Github, in order to avoid it until it is fixed, please install the following version of the program:

``$sudo apt install code-oss=1.29.0-1539702286``






# Other issues 

## Unable to install using apt-get

```sudo nano /etc/resolv.conf```

Add the DNS server list

``
nameserver 8.8.8.8 nameserver 8.8.4.4
``




To develep


The apt.sh script further down the page will typically add the required GPG keys for the package to install correctly. However, I have had issues with it working correctly. To install the correct GPG keys simply run the following command.

wget https://packagecloud.io/headmelted/codebuilds/gpgkey -O - | sudo apt-key add -
To install Visual Studio Code, you only need to run a straightforward command.

curl -L https://code.headmelted.com/installers/apt.sh | sudo bash
Once done you should be able to find the visual studio code under the accessories menu called Code-OSS.