[Original russian how-to](https://github.com/sigma7i/zigbee-wiki/wiki/zigbee-firmware-install)
without description of SDK patch applying.  
Here you can find machine translation and additional description of SDK patch applying.  

### Build zigbee firmware from source.
In this article I will try to describe the process of building firmware for Zigbee using the IAR Embedded Workbench® for 8051 environment.  

## Foreword:
You must immediately answer the question: why not immediately give the firmware? There are many reasons for this:

1. This is contrary to the philosophy of open source: if you want to tweak something, you will not succeed.  
1. If you find an error / revision / optimization, but the author has abandoned the project for a long time, then without the source code the project will simply “die”.  
1. If you need to change something very simple, for yourself, even not knowing how to program, you can always figure out which numbers are responsible for what.  
1. When there is open source, and information on how to put everything together, written in an accessible language, there is always an opportunity to experiment with the settings, to figure out what works and how.  

And many other pluses.

To demonstrate the installation, I installed a clean system to show you how to do it from scratch.

## Setting up the development environment
The IAR Embedded Workbench will be used as the development environment, where 8051 is the chip architecture, and not the system version, as you might think. First you need it [download from the link](https://www.iar.com/iar-embedded-workbench#!?architecture=8051)

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/1.png?raw=true)

We start, you must select the item "Install IAR Embedded Workbench® for 8051"

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/2.png?raw=true)

When installing IAR, you must select the custom mode:

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/custom.png?raw=true)

and uncheck the Dongle drivers installation

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/dongle%20drivers.png?raw=true)

When trying to start a project, there may be an error like this:

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/7python.png?raw=true)

Therefore, before starting the project, you need to make sure that python is installed.
You can check this on the command line:

`python –-version`  

If all is well, it will show the currently installed version of python, as in the example:  
![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/10python.png?raw=true)

If not, then [go to install python](https://www.python.org/)
![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/8python%20install.png)
Install it. Be sure to check the "add python **** to path"

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/9install.png?raw=true)

## Install git and a simple client for it.

go in and [download git](https://git-scm.com/)
Install, all checkboxes can be left by default.

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/downloadGit.png?raw=true)

go to the site https://tortoisegit.org/
We download the program depending on the bitness of the system (well, or just choose 32 bit, it does not play any significant role)
If necessary, you can download the Russification. I will not do this in this manual.

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/getTortoise.png?raw=true)

Install tortoisegit, after installation, tick the "Run first start wizard" (usually it is by default)
By default, the path to git.exe will be written, or you need to specify the path yourself.

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/TortoiseSetup.png?raw=true)

You can immediately generate ssh keys "Generate PuTTy key pair":

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/generate.png?raw=true)

Press generate, actively move the mouse / press the keys (the person acts as an RNG)
After generation, save the "Save private key"
public key (in the figure it starts with "ssh-rsa AA ..."), copy it to the clipboard (you can also save it if necessary "Save public key")

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/putty.png?raw=true)

[Go to your git account in the SSH keys section](https://github.com/settings/keys)

Click "Add new" and paste the previously copied public key.
![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/gitPuttyKey.png?raw=true)

Install firmware [Z-Stack 3.0.2](https://www.ti.com/tool/Z-STACK) - this is an SDK for developing firmware.

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/zstack.png?raw=true)

We answer tricky questions, download.

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/zstack2.png?raw=true)

Install, you can slightly reduce the path to zstack: C:\Z-Stack 3.0.2\. There should be no questions here.

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/zstackPath.png?raw=true)

## Apply SDK patch

After installing the IAR, you should apply the patch to correctly compile the sources.  

You can find the patch [here](https://github.com/diyruz/AirSense/blob/master/0001-Fixes.patch)  


How-to install:  

1. Save 0001-Fixes.patch to your Z-stack working directory (C:\Z-Stack 3.0.2)  
1. Open console at Z-stack working directory  
1. Run `git apply 0001-Fixes.patch`

## Download source code from repository
An example would be [Zigbee CO2 Sensor](https://github.com/diyruz/AirSense)

and select Code, SSH and click on the copy to clipboard icon:

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/5.png)

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/gitHubCopy.png?raw=true)

We go to the computer in zstack: C:\Z-Stack 3.0.2\Projects\zstack\HomeAutomation (if you did not change the path, then first there will be a folder "Texas Instruments")

right mouse button, "Git clone ..."

Put the URL address from the clipboard, current directory,
be sure to check the recursive checkbox, this will help to pull together the BME280_driver and zstack-lib dependencies

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/gitClone.png?raw=true)

Success screen:

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/susesfuly.png?raw=true)

The IAR Embedded Workbench can now be launched.
Open the project using the Open workspace menu item
![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/openWorkspace.png?raw=true)

We find our folder with the downloaded project, then in the CC2530DB folder we find the project file

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/projectFile.png?raw=true)

Select the RouterEB configuration and execute Rebuild All.

![](https://github.com/sigma7i/zigbee-wiki/blob/master/images/buildAll.png?raw=true)
