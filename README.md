# RemoteApps-Linux Tutorial
###### My apologies for the crudeness of this tutorial, I intend to make it more precise in the future. I do not guarantee this will work for your system, tinker and adjust accordingly. I cannot provide support for this.
## Assumptions
###### This tutorial makes the following assumptions: 
* you are comfortable with the command line and you know your way around your distribution of choice.
* that you either have access to a remote app server and `.rdp` files
* or you have the ability to set up a remote app server (setting up an RDP server is outside of the scope of this tutorial)
* if you are accessing a remote app provided by your company, this tutorial assumes that you have the permissions to use the app and have a working VPN connection (if required)

## Prerequisites
* Icons - I recommend the [Papirus](https://www.gnome-look.org/s/Gnome/p/1166289)  icon pack since it has over 5,000 icons. Chances are you will find one for your app. If not, the internet is your friend. 
* An `.RDP` file for the RemoteApp. 
* [FreeRDP](https://www.freerdp.com/) installed for your system.
* [xdpyinfo](https://docs.oracle.com/cd/E36784_01/html/E36870/xdpyinfo-1.html) this may or may not come with your systems as part of X11, if it is not installed, please install it from your package manager. this is used to check for HiDPI displays and adjust resolution accordingly.

## Steps
* Download the `.RDP` file for your app. If you are accessing a 
* Create a folder where you would like to store the config for these apps e.g. `/home/username/.config/Remote`
* Create folders with the name `RDP `and `Scripts` in that directory. Optionally you can create an `Icons` folder there as well, or use `/home/user/.local/share/icons` as your icons directory, up to you.
* Copy `.RDP` files into `/home/username/.config/Remote/RDP`
* For each app - create a shell script with the following code: (modify names and paths for each app)
```{Bash}<space>{#!/bin/bash
xdpyinfo | grep resolution|
if grep -q '97'
  then xfreerdp '/home/username/.config/Remote/RDP/YourRDPfile.rdp' /p:'P@$$w0Rd'
  else xfreerdp '/home/username/.config/Remote/RDP/YourRDPfile.rdp' /scale:180 /p:'P@$$w0Rd'
fi}
```
_Alternatively, you may use a password file for more security, but that is beyond the scope of this, for now._

* as root create a file in `/usr/share/applications` with `.desktop` extension. this will be your application shortcut in GNOME (theoretically, this should work for most other DE’s, but I haven’t tested it)

* the contents of that file should be in the following format:
```[Desktop Entry]
Type=Application
Name=APPLICATION NAME
Terminal=false
Type=Application
StartupNotify=true
Exec=/home/username/.config/Remote/Scripts/YourShellScript.sh
Icon=/home/username/.config/Remote/Icons/YourIcon.png
```

* finally, run `xfreerdp /path/to/your/RDPfile.RDP` and follow the prompts. this is important because you need to accept the certificate of the RDP server, otherwise your shortcuts worn work.

* once you restart, your app should in the GNOME app menu.
