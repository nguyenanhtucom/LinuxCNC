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
