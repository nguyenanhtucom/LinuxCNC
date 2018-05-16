# LinuxCNC
Download the source code of LinuxCNC
Enter the Terminal window ans place the following code:

$ git clone git://github.com/linuxcnc/linuxcnc.git linuxcnc-dev

$ cd linuxcnc-dev

# Resolving build dependencies

$ cd debian 

$ ./configure -a 

$ cd .. 

$ dpkg-checkbuilddeps 

This list is all the packages that it's deeded to install to be able to compile the source code.

It can be installed by using the command:

$ sudo apt-get install "name of the dependency"

In this case, the dependencies names that have to be installed are:

$ sudo apt-get install dvipng 

dvipng 
texlive-extra-utils 
texlive-latex-recommended 
texlive-fonts-recommended 
imagemagick 
texlive-lang-french 
texlive-lang-german
texlive-lang-spanish
texlive-lang-polish
tcl8.5-dev
tk8.5-dev
libxaw7-dev
libncurses-dev
libreadline-dev
asciidoc
source-highlight
groff
python-lxml
libglu1-mesa-dev
libgnomeprintui2.2-dev
libboost-python-dev
texlive-lang-cyrillic
libmodbus-dev
libusb-1.0-0-dev
graphviz
inkscape

After all those dependencies are installed, issue the command:

$ dpkg-checkbuilddeps 


# Building LinuxCNC

Run these commands in the linuxcnc-dev

$ cd src 

$ ./autogen.sh 

$ ./configure 

or

$ ./configure  --with-realtime=/usr/realtime-$VERSION

Example: --with-realtime=/usr/realtime-3.4-9-rtai-686-pae

or 

$ ./configure --with-realtime=uspace

Now is time to compile the code:

$ make 

$ make install-menus 

$ sudo make setuid 

# Run Linuxcnc (run in place)

Now that LinuxCNC is compiled, its time to run it.

$ . ../scripts/rip-environment 

$ linuxcnc 

And LinuxCNC should start, in this case we run a simulation configuration (axis_9axis).

# Installation and Configuration EtherCAT-Master

$ git clone https://github.com/sittner/ec-debianize

$ cd ec-debianize

$ debian/configure -r

$ dpkg-checkbuilddeps

$ sudo apt -y install debhelper gettext autoconf automake libtool dpatch libxenomai-dev

$ dpkg-buildpackage

$ cd ..

$ sudo dpkg -i etherlabmaster*deb

$ sudo cp ec-debianize/debian/tmp/etc/init.d/ethercat /etc/init.d

Edit in /etc/init.d/ethercat:

/etc/sysconfig/ethercat

etc:

/etc/default/ethercat

$ sudo update-rc.d ethercat defaults

Edit eth0 and e1000e:

$ /sbin/ifconfig
$ sudo vi /etc/default/ethercat
MASTER0_DEVICE="eth0"
DEVICE_MODULES="e1000e"
Installation ntp:

$ sudo apt-get -y install ntp

$ sudo usermod -aG ethercat koppi # replace 'koppi' with your user id

#Test:

$ sudo /etc/init.d/ethercat start

$ ethercat slaves

0  0:0  PREOP  +  EK1100 EtherCAT-Koppler (2A E-Bus)

1  0:1  PREOP  +  EL2004 4K. Dig. Ausgang 24V, 0.5A

2  0:2  PREOP  +  EL2004 4K. Dig. Ausgang 24V, 0.5A

3  0:3  PREOP  +  EL1004 4K. Dig. Eingang 24V, 3ms

4  0:4  PREOP  +  EL7041-1000 1K. Schrittmotor-Endstufe (50V, 5A, standard)

5  0:5  PREOP  +  EL7041-1000 1K. Schrittmotor-Endstufe (50V, 5A, standard)

6  0:6  PREOP  +  EL7041-1000 1Ch. Stepper motor output stage (50V, 5A, standard)

7  0:7  PREOP  +  EL2622 2K. Relais Ausgang, Schlie�er (230V AC / 30V DC)

# LinuxCNC / EtherCAT HAL-Module

Installation als Debian-Paket:

$ git clone https://github.com/sittner/linuxcnc-ethercat

$ cd linuxcnc-ethercat

$ sudo apt -y install machinekit-dev

$ dpkg-checkbuilddeps

$ dpkg-buildpackage

$ cd ..

$ sudo dpkg -i linuxcnc-ethercat*deb

alternative: manuelle Installation:

$ sudo apt -y install machinekit-dev

$ git clone https://github.com/sittner/linuxcnc-ethercat

$ make -C linuxcnc-ethercat all

$ sudo make -C linuxcnc-ethercat install
