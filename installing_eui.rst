**************
Installing EUI
**************

This page contains instructions for installing the EUI from scrath.

.. _eui-installation-prereqs:

Pre-requisites
==============
1. Install Git. 

	#. run ``sudo nano /etc/yum.repos.d/wandisco-git.repo``.
	#. Copy and paste the text below and past into ``wandisco-git.repo``.

		| ``[wandisco-git]`` 
		| ``name=Wandisco GIT Repository``
		| ``baseurl=http://opensource.wandisco.com/centos/7/git/$basearch/``
		| ``enabled=1``
		| ``gpgcheck=1``
		| ``gpgkey=http://opensource.wandisco.com/RPM-GPG-KEY-WANdisco``
		| ``Import GPG key for added repository key typing sudo rpm --import http://opensource.wandisco.com/RPM-GPG-KEY-WANdisco``

	#. Import the keys with ``sudo rpm --import http://opensource.wandisco.com/RPM-GPG-KEY-WANdisco``.
	#. Install git ``sudo yum install git``.

#. Install the following CentOS7 libraries for development.

	a. ``sudo yum update``
	#. ``sudo yum groupinstall "Development Tools"``
	#. ``sudo yum install cmake``
	#. ``sudo tum install boost-devel.x86_64``
	#. ``wget http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm``
	#. ``sudo rpm -ivh epel-release-latest-7.noarch.rpm``
	#. ``sudo yum install geany``
	#. ``sudo yum install java-1.7.0-openjdk-devel``

#. Install the following Linux libraries to run Labview

	a. ``sudo yum install glibc.i686``
	#. ``sudo yum install libstdc++.so.6``
	#. ``sudo yum install libXinerama.i686``
	#. ``sudo yum upgrade gnome-packagekit-common``
	#. ``sudo yum install libglvnd-glx-1.0.1-0.8.git5baa1e5.el7.i686``

.. _eui-installation:

EUI Installation
================
#. Install SAL, latest instructions for this can be found here [TODO - insert SAL technote installation guide]. for ts_xml use commit f9156b8bf300e6381b2d505da058c6b6475aed1f.


#. Install TMA Operation Manager
	
	#. ``git clone https://gitlab.tekniker.es/sai/projects/3151-LSST/lsst.git``
	#. ``cd lsst``
	#. ``git checkout feature-rotator-track`` (As of writinig this is branch to use)
	#. ``cd tma_management/``
	#. ``mkdir build``
	#. ``cd build``
	#. ``cmake ..``
	#. ``make``

#. Install LabVIEW and dependencies.

	#. Install Labview 2015. LabVIEW package manager runs on Labview 2015. This is the only reason we install LV 2015.

		#. :download:`Download LabVIEW2015 <_static/software/LabVIEW2015Linux.zip>`
		#. Extract the file.
		#. CD LabVIEW2015/32-bit 
		#. ./INSTALL say yes to everything.

	#. Install Labview 2018. Tekniker provided software was developed on LabVIEW 2018.

		#. :download:`Download LabVIEW 2018 <_static/software/LabVIEW2018Linux.zip>`, say yes to everything.
		#. Extract the file.
		#. CD LabVIEW2018 
		#. ./INSTALL say yes to everythin3/31/20g.

	#. Install Labview package manager https://vipm.jki.net/download, then install the following libraries. 

		.. note::
			I would like to point out an observation while downloading the libraries. For a reason that is not appareant to me the download may sometimes fail. The following are some tricks that worked for me.
			- right click, install
			- Install the rest of the libraries and come back to it
		 	- Manually find the download online

		.. note::
			 if it is your first time running labVIEW you will need to make sure the port on Labview 2018 is configured and has localhost.

		#. ``OpenG Toolkit``, as of writing this all but two dependencies installed. The uninstalled dependencies are OpenG Port IO and OpenG Toolkit. We only need the Toolkit, you can find the link for a manual download here https://sourceforge.net/projects/opengtoolkit/files/lib_openg_toolkit/4.x/openg.org_lib_openg_toolkit-4.0.1.9.vip/download. 
		#. ``GPower All Toolsets``, as of writing this all but two dependencies installed. The uninstalled dependencies are GPower Timing, and GPower Events. We only need Gpower Timing, attempt to install it on VI Package Manager by searching for it just as you would normally search and install any package. 
		#. ``Hidden Gems``
		#. ``NI GOOP Development Suite``
		#. ``NI Event Logger Library``
		#. ``NI GXML``
		#. ``NI LogRotate``
		#. ``NI Syslog Library``

	#. Copy LabVIEW libraries created by Tekniker into the LabVIEW installation directory.

		1. :download:`Download and unzip the Tekniker LabVIEW Libraries <_static/software/TeknikerLabVIEWLibraries.zip>`
		#. cd /usr/local/natinst/LabVIEW-2018-64
		#. sudo rsync -ra /path/to/TeknikerLabVIEWLibraries/* . 
		#. sudo chmod -R 777 ./*

#. Install Docker https://docs.docker.com/install/linux/docker-ce/centos/

#. Install database		

