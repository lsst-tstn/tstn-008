********************
ATS Deployment Guide
********************


1.	Introduction
================
This document describes the procedure run the automatic test system.
The document will show the hardware configuration in section 3 and software deployment in section 4.


2.	Reference documents
=======================

    +----+----------------------------+----------------------+---------+
    | Nº | Document                   | code                 | Version |
    +====+============================+======================+=========+
    | 1  | Deployment document        | 3151_MCS_0036        | 1.0     | 
    +----+----------------------------+----------------------+---------+
    |    |                            |                      |         |
    +----+----------------------------+----------------------+---------+
    |    |                            |                      |         |
    +----+----------------------------+----------------------+---------+


3.	Hardware configuration
==========================
In this section the needed hardware and its configuration is explained.
	3.1	Windows Machine
		This is a Windows 10 machine where LabVIEW simulators and tools will run. Also, a specific tool to manage to simulator in the Speedgoat is implemented here.
		Nothing special is need in this machine
	3.2	Speedgoat
		The Speedgoat is used to simulate the main axis behaviour in real time. 
		The configuration of the hardware is the next one.
		•	Speedgoat
			o	Serial Number: 4539 (ItemID 109200)
			o	Options:
					CPUCorei74200 (ItemID 109211)
					SSD500GB (ItemID 109048)
		•	Input/Output modules:
			o	Ethercat Slaves, IO750 (x2) (ItemID 2B7506)
			o	IO 306
		Software configuration will be download using Tekniker made tool.
	3.3	PILZ CPU
		This will be used to simulate and test safety software
		The hardware needed is the next one.
			o	PIlz PSSu 4000 ref 314070 
			o	PSSu E F 4DI-T 
			o	PSSu E F 4DO 0.5-T 
		The configuration of hardware is part of the project where the code is included, son configuration will be explained in section 4.

4.	Software deployment
=======================
Each hardware has different software parts, and some hardware had more than one software part. In next sections each hardware element is explained
	4.1	Windows Machine
		In the Windows Machine some simulators and some tools are running. 
		Start installing the Force EtherCAT Variables installer, that will install the LabVIEW runtime needed in many other tools and simulators.
		4.1.1	Requirements
		4.1.2	Force EtherCAT Variables
			This tool allows to other simulators writing data to EtherCAT variables using a TCP custom protocol. The value written using this tool we be a forcing value, so any slave value will be overwritten with the written value.
			The source code and more documentation about configuration can be found in https://gitlab.tekniker.es/aut/projects/3151-LSST/hil/forceethercatvars.
			Follow next steps to deploy this software
				1.	If the installer is available continue in step 6
				2.	Clone the repository in the link above
				3.	Open the project ForceEtherCATVars.lvproj
				4.	Go to “Build Specifications” and right click in “ForceIOs” to select “Build”
				5.	Go to “Build Specifications” and right click in “ForceEtherCatVars Installer” to select “Build”
				6.	When finishes compilation open location and copy the “Volume” folder to Windows Machine
				7.	Install the tool using the “install.exe”
				8.	Run ForceIOs.exe.
		4.1.3	Simulate limits
			This software allows to simulate the behaviour of some subsystem limits switches. Those limits could be part of safety system or EtherCAT distributed IOs.
			The source code and more documentation about configuration can be found in https://gitlab.tekniker.es/aut/projects/3151-LSST/hil/simulatelimits
			Follow next steps to deploy this software
				9.	If the installer or executable is available continue in step 
				10.	Clone the repository in the link above
				11.	Open the project SimulateLimits.lvproj
				12.	Go to “Build Specifications” and right click in “SimulateLimits” to select “Build”
				13.	When build finishes go to build folder and copy all files and folder 
				14.	Paste compilation files to desired destination in Windows Machine
				15.	Open the "data" folder and open "GeneralConfiguration.xml" 
				16.	Change the first path of the field TCP_senders_configuration_Path to point to ForceECATVars_TCP_SenderConfig.xml file in the same data folder.
				17.	Change dim='[X]' to dim='[1]' for "TCP_senders_configuration_Path" and for "LimitsDefinition" tags. We are only using the first configured limit because you need the safety full simulator with PILZ hardware to use other limits, When you get this hardware (perhaps you have one in the submit) we can download code to it and use those other limits.
				18.	Run SimulateLimits.exe
		4.1.4	Write/Read Network Shared Variables Tool
			This tool allows to other simulators writing and reading data from network shared variables using a TCP custom protocol
			The source code and more documentation about configuration can be found in https://gitlab.tekniker.es/aut/projects/3151-LSST/hil/readvariables
			Follow next steps to deploy this software
				1.	If the installer or executable is available continue in step 
				2.	Clone the repository in the link above
				3.	Open the project ReadVariables.lvproj
				4.	Go to “Build Specifications” and right click in “Executable” to select “Build”
				5.	When build finishes go to build folder and copy all files and folder 
				6.	Paste compilation files to desired destination in Windows Machine
				7.	Open the "data" folder and open "WriteReadVarConfig.xml".
				8.	Change the path of the field TCP_configuration_file to point to TCP_ServerConfig.xml file in the same data folder.
				9.	Run ReadWriteNSVs.exe

	4.2	TMA PXI
		This is the PXI where the control code for all subsystem is running. To be able to configure the TMA PXI, the development PC should be configured as shown in the deployment document 
			1.	Download the PXI repository: https://gitlab.tekniker.es/aut/projects/3151-LSST/LabVIEWCode/PXIController
			2.	Open the LSST_MainControllerPXI.lvproj.
			3.	Ensure that in the project properties the Conditional Disable Symbol “HIL” is set to “True”
				a.	Right click in the project an select properties
				b.	In the opened window go to Conditional Disable Symbols page and set the value for HIL symbol to “True”.
			4.	Continue with steps 3.a to 3.c of the point 6.2 in the Deployment document.
			5.	Open the RT_MCS_Main.vi
			6.	Run the VI
			7.	When the vi is deployed to the target, disconnect the target
				a.	Right click TMA_PXI target and click Disconnect
 

