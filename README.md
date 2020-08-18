# RemoteApps-Linux Toutorial
###### My appologies for the crudeness of this toutorial, I intend to make it more percise in the future.
## Assumptions
###### This tutorial makes the following assumptions: 
* you are comfortable with the commandline and you know your way around your distribution of choice.
* that you either have access to a remote app server and `.rdp` files
* or you have the ability to set up a remote app server (setting up an RDP server is outside of the scope of this tutorial)
* if you are accessing a remote app provided by your company, this toutorial assumes that you have the parmissions to use the app and have a working VPN connection (if required)

## Prerequisites
* Icons - I reccomend the [Papirus](https://www.gnome-look.org/s/Gnome/p/1166289)  icon pack since it has over 5,000 icons. Chances are you'll find one for your app. If not, the internet is your friend. 
* An `.RDP` file for the RemoteApp. 
* [FreeRDP](https://www.freerdp.com/) installed for your system.
* [XDPYINFO](https://docs.oracle.com/cd/E36784_01/html/E36870/xdpyinfo-1.html) this may or may not come with your systems as part of X11, if its not installed, please install it from your package manager. this is used to check for HiDPI displays and adjust resolution accordingly.

## Steps
* Download the `.RDP` file for your app. If you are accessing a 
* Create a folder where you would like to store the config for these apps e.g. `/home/username/.config/Remote`
* Create folders with the name `RDP `and `Scripts` in that directory. Optionally you can create an `Icons` folder there as well, or use `/home/user/.local/share/icons` as your icons directory, up to you.
* Copy `.RDP` files into `/home/username/.config/Remote/RDP`
* Create a shell script with the follwing code: (modify names and paths for each app)
```{Bash}<space>{#!/bin/bash
xdpyinfo | grep resolution|
if grep -q '97'
  then xfreerdp '/home/usename/.config/Remote/RDP/cpub-acad-RD_Galaxy-CmsRdsh.rdp' /p:'P@$$w0Rd'
  else xfreerdp '/home/username/.config/Remote/RDP/cpub-acad-RD_Galaxy-CmsRdsh.rdp' /scale:180 /p:'P@$$w0Rd'
fi}
```
