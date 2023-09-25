# Welcome to E2E Patterns
ℹ️ Please be informed, this repository is being refactored for use here using https://github.com/boconnor2017/e2e-patterns.git. All labs and code snippets will be migrated here shortly. In the meantime, please feel free to use the https://github.com/boconnor2017/e2e-patterns.git repository while we work on the build of this one. 

![alt text](https://github.com/boconnor2017/e2e-patterns/blob/main/img/E2E-Patterns-Logo-01.png)
This repository is intended to provide code samples to help you build immutable VMware Patterns. 

:heavy_exclamation_mark: ***WARNING: the contents of this repository are not intended for production networks in their current state. It is recommended that these scripts are certified in a Development environment, functionally tested, and refactored with the appropriate security and operational considerations. Proper SDLC practices are advised.***

# What is a Pattern?
Think of a "Pattern" like a Docker Image. A Docker Image might be very generic or it might be fully baked with specific packages. Similarly, a Pattern is a set of packages (from this repo) designed to function on a PhotonOS virtual machine. The result of a Pattern (a Docker Container using the Docker analogy) is the VMware environment that the Pattern creates. For example: a Workload Domain Pattern might consist of a vCenter Server, an NSX Manager, and a few nested ESXi hosts. The Pattern in this example would contain all code from this repo to automate the build of a workload domain, formatted to run on PhotonOS. 

# Prerequisites for Running a Pattern 
## VMware Software
All VMware software in this lab must be downloaded manually prior to running the pattern. Each pattern will contain instructions for obtaining the proper packages. It is recommended you download an SFTP tool such as FileZilla or WinSCP to make it easier to drop software bundles onto a given photon machine, although this is not mandatory. 

## Hardware and Networking Requirements
To run these patterns you will need a physical ESXi host and a /24 subnet. Development and testing of these labs were facilitated using:
* 1x Ubiquiti Edgerouter 4 uplinked to home wifi
* 1x Cisco Catalyst 2950 uplinked to the Edgerouter
* 1x PowerEdge R710 with 8 CPU (Intel Xeon E5620 @ 2.40GHz), 192 GB of RAM, and 2.72 TB of storage uplinked to the Cisco switch

It is not mandatory to have these exact specs in your home lab. In fact its not even mandatory that you use a server (a beefy laptop will suffice) or a switch. The more resources the better the experience, but build with what is available. The following ESXi version was used on the PowerEdge:

* ESXi version 6.7.0 (build 8169922)

## Licensing
All Patterns are designed to be immutable. Licensing is not required. If a VMware environment has been running longer than the duration of the evaluation, you may choose to buy the appropriate licenses from VMware or you may choose to destroy and rebuild the environment. 

# Patern 00: Deploy the Master Controller
There is one PhotonOS server used as the master control plane for all Patterns. This PhotonOS server will be referred to as the Master Photon Controller. The steps to deploy the Master Photon Controller are outlined in the Quick Start README.md page. If you haven't already, the following are the steps to configure the Master Photon Controller.

Step 1: Deploy Photon (photon-ova-4.0-ca7c9e9330.ova)
For downloads visit: https://github.com/vmware/photon/wiki/Downloading-Photon-OS 

The default password is `changeme`. For all labs, use `/usr/local/` as the working directory.
```
cd /usr/local/
```

Step 2: Download controller prep script 
```
curl https://raw.githubusercontent.com/boconnor2017/e2e-patterns/main/prep-photon.sh >> prep-photon.sh
```

Step 3: Download refresher script
```
curl https://raw.githubusercontent.com/boconnor2017/e2e-patterns/main/refresh-e2e-patterns.sh >> refresh-e2e-patterns.sh
```

Step 4: Run E2E lab PhotonOS prep script
```
sh prep-photon.sh >> _prep_photon.log
```

Step 5: Refresh local repo (as needed)
```
sh refresh-e2e-patterns.sh
``` 

## Update Configuration File
The configuration file contains all environment specific information. The configuration file is located at:
```
/usr/local/e2e-patterns/config.py
```
Note: its obviously a bad practice to store sensitive information in a code repository. The configuration file in this repo contains sample data so that you understand the proper syntax when creating your own file. Its recommended to store your config file in a safe location. Replace the `config.py` file stored in `/usr/local/e2e-patterns` after every refresh. 

# Next Steps (see table of contents)
[Basic Photon OS Patterns](https://github.com/boconnor2017/e2e-patterns/wiki/Basic-PhotonOS-Patterns)
