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

# Verifying the installation of open source tools
An initial working directory can be made by copying the required files as follows:
```
$ mkdir Lab1_and
$ cd Lab1_and
$ mkdir mag
$ mkdir netgen
$ mkdir xschem
$ cd xschem
$ cp /usr/local/share/pdk/sky130A/libs.tech/xschem/xschemrc .
$ cp /usr/local/share/pdk/sky130A/libs.tech/ngspice/spinit .spiceinit
$ cd ../mag
$ cp /usr/local/share/pdk/sky130A/libs.tech/magic/sky130A.magicrc .magicrc
$ cd ../netgen
$ cp /usr/local/share/pdk/sky130A/libs.tech/netgen//sky130A_setup.tcl .
```
Checking if magic works
![Screenshot from 2023-02-12 08-07-06](https://user-images.githubusercontent.com/65780913/218290703-f27de2e5-83b7-4a33-8b4d-ac3e9a818ece.png)

Checking if xschem works
![Screenshot from 2023-02-12 08-09-59](https://user-images.githubusercontent.com/65780913/218290782-9e1e3177-bf64-478f-a78f-e317e83c81b4.png)

Checking if netgen works
![Screenshot from 2023-02-12 08-11-18](https://user-images.githubusercontent.com/65780913/218290833-41535f66-15f2-4022-ac45-fcd130a6cb01.png)

Checking if ngspice works
![Screenshot from 2023-02-12 08-12-21](https://user-images.githubusercontent.com/65780913/218290870-d6616286-d53a-4797-8ad9-21ae73e11d43.png)


# Inverter pre-layout characterization using xschem and ngspice
## Creating invereter using xscheme
Create this schematic using xschem. Then click on netlist to generate netlist and save file as inverter.sch.

![Screenshot from 2023-02-12 08-29-26](https://user-images.githubusercontent.com/65780913/218291635-6905365c-3153-41db-8832-b2396c503ffb.png)

## Generate symbol of inverter
Now in order to generate the symbol, create a box on inverter in inverter.sch, press A and check yes. It will make inverter.sym file in the same directory.
![Screenshot from 2023-02-12 08-29-29](https://user-images.githubusercontent.com/65780913/218291761-8a3396f1-91ea-4eea-a53f-3d83dcab7a4a.png)

## Create test bench for inverter
Now in order to test that our inverter is actually working, we create a test bench as shown below. press ctrl+i to open choose devices window. After creating test bench, again click on netlist and then simulate. You might get error so what you should do is put the .spiceinit present in your current xschem folder file in home-> .xschem -> simulation folder
![Screenshot from 2023-02-12 08-29-33](https://user-images.githubusercontent.com/65780913/218291891-67f753b7-8587-4c39-b8f3-57658ba1df59.png)

## Simulations Results
![Screenshot from 2023-02-09 15-02-05](https://user-images.githubusercontent.com/65780913/218291918-8cd3a1b8-f555-44b7-8aee-36617982259e.png)
![Screenshot from 2023-02-12 08-36-29](https://user-images.githubusercontent.com/65780913/218291932-7646165c-3a61-4afe-a402-eef5fbd2d922.png)

Rise time= 10ns

Fall time = 10ns

Time period = 1u

Delay between vin and vout= 2.502us -2.50132us = 68ns



