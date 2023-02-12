# msvsdcsc
# week 0
| S.No  | Action Item | Status |
| ----- | ----------- | ------|
| 1.  | Install Oracle Virtual box with Ubuntu 20.04 | :heavy_check_mark: |
| 2.  | Install magic and sky130 PDKs | :heavy_check_mark: |
| 3.  | Create inverter and perform pre-layout using xschem or ngspice | :heavy_check_mark: |
| 4.  | Inverter Post-layout characterization using 2) | :heavy_check_mark: |
| 5.  | Update your findings on your GitHub repo with the title “Week 0” | :heavy_check_mark: |


# Installing open source tools and Sky130pdk
In order to integrate open pdk with all the open source tools, it has to be installed last. So follow the steps in the order as described below. Besides this in case you follow any error in installation, it might be cause of any missing dependency. So google the error, there you will find which dependency to install to make your installation successful.


## Magic
Magic is an opensource tool that is basically used to do layout of any circuit.
Before using ./configure install all these dependencies
### M4 preprocessor
```
$ sudo apt-get install m4
```
### tcsh shell
```
$ sudo apt-get install tcsh
```
### csh shell (note that Ubuntu has different csh and tcsh)
```
$ sudo apt-get install csh
```
### Xlib.h
```
$ sudo apt-get install libx11-dev
```
If you wish to have the Tcl/Tk wrapper around magic (recommended) you will need to install the Tcl/Tk libraries. Version 8.5 or higher is highly recommended.
### Tcl/Tk
```
$ sudo apt-get install tcl-dev tk-dev
```
The best graphics for Magic is the OpenGL interface ("magic -d OGL"), but since that is problematic for off-screen rendering on many systems, a good alternative is the Cairo graphics interface ("magic -d XR"). This is optional, but if you want to use it, you need the Cairo library development package:
### Cairo
```
$ sudo apt-get install libcairo2-dev
```
The OpenGL interface itself may need these dependencies:
### OpenGL
```
$ sudo apt-get install mesa-common-dev libglu1-mesa-dev
```
For the non-Tcl/Tk version only: The readline source makes reference to the `tputs` function which is provided by the ncurses library. Although the ncurses library is installed in Ubuntu, the include files to build against it are not, so the development version is required.
### ncurses
```
$ sudo apt-get install libncurses-dev
```

Installation Steps

```
$  git clone git://opencircuitdesign.com/magic
$  cd magic
$	 ./configure
$  make
$  sudo make install
```
More info can be found at http://opencircuitdesign.com/magic/index.html

## Netgen
Netgen is a tool for comparing netlists, a process known as LVS, which stands for "Layout vs. Schematic"

Install steps:
```
$  git clone git://opencircuitdesign.com/netgen
$  cd netgen
$	./configure
$  make
$  sudo make install
```
More info can be found at http://opencircuitdesign.com/netgen/index.html

## Xschem
Xschem is a schematic capture program

Install steps:
```
git clone https://github.com/StefanSchippers/xschem.git xschem_git
sudo apt-get install flex
sudo apt-get install bison
sudo apt-get install libxpm-dev
./configure
make
sudo make install
```
More info can be found at http://repo.hu/projects/xschem/index.html

## Ngspice
Ngspice is the open-source spice simulator for electric and electronic circuits.

Install steps:

After downloading the tarball from https://sourceforge.net/projects/ngspice/files/ng-spice-rework/old-releases/37/ngspice-37.tar.gz/download to a local directory, unpack it using:
```
$ tar -zxvf ngspice-37.tar.gz
 $ cd ngspice-37
 $ mkdir release
 $ cd release
 $ ../configure  --with-x --with-readline=yes --disable-debug
 $ make
 $ sudo make install
 ```
 More info can be found at https://ngspice.sourceforge.io/index.html

Please note that to view the simulation graphs of ngspice, xterm is required and can be installed using.
```
$ sudo apt-get update
$ sudo apt-get install xterm
```

## open pdk
Open_PDKs is distributed with files that support the Google/SkyWater sky130 open process description https://github.com/google/skywater-pdk. Open_PDKs will set up an environment for using the SkyWater sky130 process with open-source EDA tools and tool flows such as magic, qflow, openlane, netgen, klayout, etc.

Install steps:
```
$  git clone git://opencircuitdesign.com/open_pdks
$  open_pdks
$	./configure --enable-sky130-pdk
$  make
$  sudo make install
```
Now that we have all the necessary tools installed let's understand the design flow!



