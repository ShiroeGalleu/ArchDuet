# Lenovo Duet post setup script for cadmium

## Hardware support:
### Note: (NW) means Needs Workaround: listed below
| Hardware support matrix  	| Y/N  		| 
|-------------------------	|--------	|
| Internal Display	       	| Y		   	|
| Display autorotation    	| Y	    	|
| Local Install	          	| y  			|
| Bluetooth                 | y       |
| Touchscreen	    	  	    | Y		   	| 
| Pen Input		            	| Y			  |
| WiFi		     	         	  | Y		  	|
| 3D Acceleration	        	| Y		    | 
| GPU reclocking	         	| Y			  |
| Sleep                     | Y       |
| Display Rotation         	| Y  			|
| Audio output 	          	| Y				|
| Built in mic              | NW      |
| Hardware video decoding  	| N	  		|
| KVM Virtualtization      	| N  			|
| External Display	      	| N		  	|
| Front + rear camera		   	| N  			|
| x11                       | N       |


## WARNING: if you want to use a desktop or wm, it will need to have wayland support
### known working:
- KDE Plasma
- Plasma Mobile
- Cinnamon (Experimental)
- Gnome
- sway
- hyperland
- phosh
- phosh-table


### Installation
- Download [cadmium-arm64-debian.img.xz](https://github.com/Maccraft123/Cadmium/releases/tag/v0.4.0-pre2) and fallow the guide
- after running `./install` and setting up wifi click quit in the bottem right. note that it will fail (this is fine)
- run the fallowing command `apt update && apt full-upgrade` depending on your usb speed this may take a while
- run `./install` again and when on the wifi page click quit
- once you hit `one of: gnome kde phosh sway or none?` type in `none`
- it will now run finnish installing. once you see `done!` type `reboot` and once you see the white boot screen you can remove your usb
- once you have booted of the internal storage, you will need sign in as root and connect to wifi click [here](https://www.makeuseof.com/connect-to-wifi-with-nmcli/). you can skip to step 2
- at this point you can use ssh or contiune type on the tablet.

### SSH: Setup Over Network
- download ldps.sh file from above then `cd` into the folder where you downloaded it
- ssh into your duet with `ssh username@ip` then run `su` to switch to root
- run ```git clone https://github.com/ShiroeGalleu/ld-post-setup.git && cd ld-post-setup```
- run ```chmod +x ldps.sh``` then ```./ldps.sh```
- when you see ```auto-cpufreq installer``` type `I` then hit enter
- once done reboot ```systemctl reboot```

### ON Device:
- sign in as root
- run ```git clone https://github.com/ShiroeGalleu/ld-post-setup.git && cd ld-post-setup```
- run ```chmod +x ldps.sh``` then ```./ldps.sh```
- when you see ```auto-cpufreq installer``` type `I` then hit enter
- once done reboot ```systemctl reboot```

### FIXED:
- INTERNAL SPEAKER 08/13/24 05:40 UTC -05

## Work Arounds:
### FIX MIC:
- run `pactl list > tmp.sh` . Note that the .sh is not needed, just easyer to read
- you will need to look for the fallowing in the tmp file `Name: alsa_input.platform-mt8183-sound.HiFi__InternalMic__source` once found you need to copy the numbers of `Source #xx` xx being the numbers
- run the fallowing commands `pactl set-source-volume xx 400%` xx being the numbers from the tmp file
- to have it load at boot do `sudo alsactl store`

## CREDIT:
[Adnan Hodzic](https://github.com/AdnanHodzic) for the auto-cpu-freq script

[Maya](https://github.com/Maccraft123) for cadmium

[kaitlyn](https://github.com/catgirlcataclysm)

[Radical](https://github.com/Radiicall)

[Azull](https://azull.giize.com/)
