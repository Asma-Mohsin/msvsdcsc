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
![Screenshot from 2023-02-12 08-30-45](https://user-images.githubusercontent.com/65780913/218292161-300dc021-d90b-4a71-8c08-1f5a340e30bc.png)

![Screenshot from 2023-02-12 08-36-29](https://user-images.githubusercontent.com/65780913/218291932-7646165c-3a61-4afe-a402-eef5fbd2d922.png)

Rise time= 10ns

Fall time = 10ns

Time period = 1u

Delay between vin and vout= 2.502us -2.50132us = 68ns

# Inverter post layout characterization using magic
Open magic by going to mag directory and type
```
magic -d XR
```

Now go to file, and click on import spice and select inverter.spice file present in /home/.xschem folde. You will get pmos and nmos loaded. Now you have to make connections to make an inverter. Do all the connections and clear all DRCs.
![Screenshot from 2023-02-11 23-59-10](https://user-images.githubusercontent.com/65780913/218292449-7a22e3d9-1913-4648-a65b-1f6910925e70.png)

Now open the tcl window and write these commands to generate netlist.
```
% extract do local
% extract all
% ext2spice lvs
% ext2spice
```
If we run an ls in this directory we should see our .ext files and .mag files for the circuit - inverter.mag inverter.ext We can also see a .spice netlist. This inverter.spice netlist generated post layout contains the parasitics that were absent in pre-layout netlist.
![Screenshot from 2023-02-12 09-10-23](https://user-images.githubusercontent.com/65780913/218292600-4c2c208f-cecc-4677-8a1f-348a3b2fb3c7.png)

Now we need to use our pre-layout spice witht he post-layout parasitics netlist and perform spice simulations.

 Step I Paste the pre-layout netlist of inverter testbench into the magic generated inverter spice netlist
 
 ## Pre-layout spice netlist of inverter_tb
 ```
 ** sch_path: /home/asma_mohsin/Desktop/Lab1_and/xschem/inverter_tb.sch
**.subckt inverter_tb in out
*.ipin in
*.opin out
x1 net1 in out GND inverter
V2 net1 GND 1.8
.save i(v2)
V1 in GND pulse(0 1.8 0 1n 1n 500n 1u 0)
.save i(v1)
**** begin user architecture code

.lib /usr/local/share/pdk/sky130A/libs.tech/ngspice/sky130.lib.spice tt


.control
save all
tran 100n 10u
plot v(in) v(out)
.endc

**** end user architecture code
**.ends

* expanding   symbol:  inverter.sym # of pins=4
** sym_path: /home/asma_mohsin/Desktop/Lab1_and/xschem/inverter.sym
** sch_path: /home/asma_mohsin/Desktop/Lab1_and/xschem/inverter.sch
.subckt inverter vdd vin vout vss
*.ipin vin
*.opin vout
*.iopin vdd
*.iopin vss
XM1 vout vin vss vss sky130_fd_pr__nfet_01v8 L=0.18 W=4.5 nf=3 ad='int((nf+1)/2) * W/nf * 0.29' as='int((nf+2)/2) * W/nf * 0.29'
+ pd='2*int((nf+1)/2) * (W/nf + 0.29)' ps='2*int((nf+2)/2) * (W/nf + 0.29)' nrd='0.29 / W' nrs='0.29 / W'
+ sa=0 sb=0 sd=0 mult=1 m=1
XM2 vout vin vdd VDD sky130_fd_pr__pfet_01v8 L=0.18 W=3 nf=3 ad='int((nf+1)/2) * W/nf * 0.29' as='int((nf+2)/2) * W/nf * 0.29'
+ pd='2*int((nf+1)/2) * (W/nf + 0.29)' ps='2*int((nf+2)/2) * (W/nf + 0.29)' nrd='0.29 / W' nrs='0.29 / W'
+ sa=0 sb=0 sd=0 mult=1 m=1
.ends

.GLOBAL GND
.end
```
After selectively pasting this netlist into the inverter.spice generated(extracted) from Magic Tool, save it as inverter_tb_magic.spice. The netlist looks like this

```
* NGSPICE file created from inverter.ext - technology: sky130A
** sch_path: /home/asma_mohsin/Desktop/Lab1_and/xschem/inverter_tb.sch
**.subckt inverter_tb in out
*.ipin in
*.opin out
x1 net1 in out GND inverter
V2 net1 GND 1.8
.save i(v2)
V1 in GND pulse(0 1.8 0 10n 10n 500n 1u 0)
.save i(v1)
**** begin user architecture code

.lib /usr/local/share/pdk/sky130A/libs.tech/ngspice/sky130.lib.spice tt


.control
save all
tran 100n 10u
plot v(in) v(out)
.endc

**** end user architecture code
**.ends

* expanding   symbol:  inverter.sym # of pins=4
** sym_path: /home/asma_mohsin/Desktop/Lab1_and/xschem/inverter.sym
** sch_path: /home/asma_mohsin/Desktop/Lab1_and/xschem/inverter.sch
.subckt inverter vdd vin vout vss
*.ipin vin
*.opin vout
*.iopin vdd
*.iopin vss
XM1 vout vin vss vss sky130_fd_pr__nfet_01v8 L=0.18 W=4.5 nf=3 ad='int((nf+1)/2) * W/nf * 0.29' as='int((nf+2)/2) * W/nf * 0.29'
+ pd='2*int((nf+1)/2) * (W/nf + 0.29)' ps='2*int((nf+2)/2) * (W/nf + 0.29)' nrd='0.29 / W' nrs='0.29 / W'
+ sa=0 sb=0 sd=0 mult=1 m=1
XM2 vout vin vdd VDD sky130_fd_pr__pfet_01v8 L=0.18 W=3 nf=3 ad='int((nf+1)/2) * W/nf * 0.29' as='int((nf+2)/2) * W/nf * 0.29'
+ pd='2*int((nf+1)/2) * (W/nf + 0.29)' ps='2*int((nf+2)/2) * (W/nf + 0.29)' nrd='0.29 / W' nrs='0.29 / W'
+ sa=0 sb=0 sd=0 mult=1 m=1
.ends

.GLOBAL GND
.end

.subckt sky130_fd_pr__nfet_01v8_N39HBR a_n33_172# a_n275_n324# a_18_n150# a_114_n150#
+ a_n129_n238# a_63_n238# a_n78_n150# a_n173_n150#
X0 a_114_n150# a_63_n238# a_18_n150# a_n275_n324# sky130_fd_pr__nfet_01v8 ad=4.425e+11p pd=3.59e+06u as=4.5e+11p ps=3.6e+06u w=1.5e+06u l=180000u
X1 a_n78_n150# a_n129_n238# a_n173_n150# a_n275_n324# sky130_fd_pr__nfet_01v8 ad=4.5e+11p pd=3.6e+06u as=4.425e+11p ps=3.59e+06u w=1.5e+06u l=180000u
X2 a_18_n150# a_n33_172# a_n78_n150# a_n275_n324# sky130_fd_pr__nfet_01v8 ad=0p pd=0u as=0p ps=0u w=1.5e+06u l=180000u
.ends

.subckt sky130_fd_pr__pfet_01v8_KG2LE3 a_n78_n100# a_n173_n100# a_n129_n197# a_18_n100#
+ a_63_n197# a_114_n100# w_n311_n319# a_n33_131#
X0 a_18_n100# a_n33_131# a_n78_n100# w_n311_n319# sky130_fd_pr__pfet_01v8 ad=3e+11p pd=2.6e+06u as=3e+11p ps=2.6e+06u w=1e+06u l=180000u
X1 a_114_n100# a_63_n197# a_18_n100# w_n311_n319# sky130_fd_pr__pfet_01v8 ad=2.95e+11p pd=2.59e+06u as=0p ps=0u w=1e+06u l=180000u
X2 a_n78_n100# a_n129_n197# a_n173_n100# w_n311_n319# sky130_fd_pr__pfet_01v8 ad=0p pd=0u as=2.95e+11p ps=2.59e+06u w=1e+06u l=180000u
.ends

.subckt inverter vdd vout
Xsky130_fd_pr__nfet_01v8_N39HBR_2 a_90_1528# VSUBS vout vss a_90_1528# a_90_1528#
+ vss vout sky130_fd_pr__nfet_01v8_N39HBR
Xsky130_fd_pr__pfet_01v8_KG2LE3_0 vdd vout a_90_1528# vout a_90_1528# vdd w_80_1786#
+ a_90_1528# sky130_fd_pr__pfet_01v8_KG2LE3
.ends
```
Now open this file with ngspice. Also place .spiceinit file in this directory to perform the simulations without any error
![Screenshot from 2023-02-12 09-27-09](https://user-images.githubusercontent.com/65780913/218292989-03fa81b3-05a2-4d9d-9cc0-cc8dc58e3cb8.png)

Now run the following commands in the ngspice window
```
run
dsiplay   //list of plots available
plot vin vout
```
![Screenshot from 2023-02-12 09-31-55](https://user-images.githubusercontent.com/65780913/218293101-d9daffd4-2005-46a0-ad21-9263b1b7514e.png)

![Screenshot from 2023-02-12 09-31-35](https://user-images.githubusercontent.com/65780913/218293114-8c03858f-47c5-42ac-827c-d1abb3ad1d47.png)

Rise time= 10ns

Fall time = 10ns

Time period = 1u

Delay between vin and vout= 2.005us -2.0023us = 2.7ns




