*****************************
TMA Simulation Configurations
*****************************

Here you will find sets of instructions that document the different configurations that are avilable. Each of these configurations test a certain functionality. In order of increasing complexity the following are the configurations available to the TMA software.

1. HMI NSV Simulation

HMI NSV Simulation
==================
The following instructions will help you understand and configure a simulation environment for the TMA Humane Machine Interface, which can be shortened to HMI. This is the most basic simulation that can be done. This is called the "HMI NSV Simulation" because we are simulation only the NSV's (Network Shared Variables) on a Windows machine to verify that the HMI is comminicating to the NSV's. Random NSV's will be generated so we will see the HMI behave eratically. The meat and potatoes of this configuration is to modify a configuration file to have the right IP addresses which point to the NSV hosting Windows machine. 

	1. Install the HMI, if you have not done so you can find the instructions here [TO DO]
	#. On a Windows machine :download:`download the NSV Simulator <_static/software/NSVSimulator.zip>`.
	#. Identify the IP Address of the Windows machine. The IP address that I set my windows machine to is 192.168.1.11. Manually set yours if you need to.
	#. Identify the IP Address of the CentOS machine which is running the HMI. I manually set mine to be 192.168.1.10. Manually set yours if you need to. 
	#. Connect both machines to a switch and verify that the CentOS and Windows machine can ping each other. 

	.. note:: At this point we are confident that both machines can communicate with each other, we continue by editing configuration files of the HMI. The specific repo name is "HMIComputers". This repository contains the LabVIEW GUI which is referred to as the HMI.

	6. Open HMICOmputers/Configuration/HMIConfig.xml. This file contains paths, IP Addresses, and locations to various elements of the HMI. 

	#. Look for a tag named <ErrorTaskDirectoryPath dim='[5]' type='String'>. There will be a series of <String> tags below. These series of tags make a path to the ErrorHistory folder. Modify these strings to the path of your local machine. Don't forget to update the integer value '5' if you change the number of <String> tags.
	#. Look for a tag named <TMA_Management_Linux_Options mems="3">. There will be a nested tag named <Working_Path type="Path">/home/Andrew/gitrepos/lsst/tma_management/build</Working_Path>. Modify this path to the path of your local machine.
	#. Look for a tag named <WindowTelemetryDirectoryPath dim='[5]' type='String'>. There will be a series of <String> tags below. These series of tags make a path to the WindowsLogging folder. Modify these strings to the path of your local machine. Don't forget to update the integer value '5' if you change the number of <String> tags. We are done editing this file, save and close. 

	#. Open HMIComputers/Configuration/HMITelemetryVariablesURLs.ini. This file contains URL's, IP's, and other configuration tags.
	#. Do a global search for 10.1.22.154 and replace these with the IP address of the Windows machine running the NSV Simulator. In my case I will be replacing them with 192.168.1.11. At the time of writing this document there are 1116 occurances when doing a global search and replace. 
	#. Do a global search for 192.168.209.10 and replace these with the IP address of the Windows machine running the NSV Simulator. In my case I will be replacing them with 192.168.1.11. At the time of writing this document there are 282 occurances when doing a global search and replace.

	#. Well done! The EUI is now configured to operate with the NSV Simulator. Open HMI as you normally would [TODO LINK FOR OPENING THE EUI]

Installation for the NSV Force shared 
=====================================

Installating PXI

1) Install a git tool, I use source tree
2) git pull the PXI software onto the windows machine
3) Download Tekniker Labview Libraries by clinging https://gitlab.tekniker.es/aut/libraries/labview/labview
4) Checkout branch LV_2018
5) copy files in the local folder including the .git folder to Nationa Instruments/LabVIEW2019
6) Select the preselected option that Labview asks to load
7) Cancel when labview cannot find the HMI module
8) Cancel when labview cannot find the DatabaseSettingsConfig.ctl
9) Cancel when labview cannot find the Axis Data.ctl
10) When labview asks to find FGV_BasicFGVAction.ctl find it my navigating to Program Files (x86)\National Instruments\LabVIEW 2019\templates\TeknikerTemplates\_controles

The reason we have the HIL needs to be true when in simulation mode. And False when do real telescope control. 
We need atleast another ethercat 

Alberto will send tomorrow how ethernet ports we will need

We now configure the PXI for proper ethernet connections

"Deploy ethercat master to PXI" -> what this really means to do is

we currently have 2 issues. We can't change the network to ethercat. -> We think this can be solved purchases 2 4 port cards that ALberto will send us. The second is that I do not have the correct drivers. Only install compilations tools,
12 - 0
