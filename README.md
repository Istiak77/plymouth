Plymouth Setup on Arch Linux

###clone this repo :

    git clone https://github.com/Istiak77/plymouth

    
###Move the Steam folder to 

    /usr/share/plymouth/themes/

    
###THEME CREDIT GOES TO - MagiBoot-D3bootanimations


### https://t.me/MagiBoot




		                  #########FOLLOW THE INSTRUCTIONS BELLOW#########
    
This guide provides step-by-step instructions for installing and configuring Plymouth on Arch Linux. Plymouth is a graphical boot splash screen that enhances the boot experience with animations and themes. This documentation covers:

   1.Installation

   2.Plymouth Setup

   3.Adding a Delay Script

   4.Changing Themes
   
   

1. Installation

Install Plymouth

#To install Plymouth, run the following command:

	sudo pacman -S plymouth

#This installs Plymouth and its dependencies.


2. Plymouth Setup

##Configure GRUB

#Plymouth requires the quiet splash parameters to be added to the kernel command line.

#Open the GRUB configuration file:
    
    sudo nano /etc/default/grub

#Modify the GRUB_CMDLINE_LINUX_DEFAULT line to include quiet splash:

    GRUB_CMDLINE_LINUX_DEFAULT="loglevel=3 quiet splash"

#Save the file and update GRUB:

    sudo grub-mkconfig -o /boot/grub/grub.cfg


##Rebuild Initramfs

#Plymouth needs to be integrated into the initramfs. Rebuild the initramfs with:

	sudo mkinitcpio -P

##Enable Plymouth Service

#Enable the Plymouth service to start at boot:

	sudo systemctl enable plymouth-start.service


3. Changing Themes

##List Available Themes

#To see the list of available Plymouth themes, run:


	plymouth-set-default-theme -l


##Set a New Theme

#To set a new theme (Steam), use the following command:


	sudo plymouth-set-default-theme -R Steam


#The -R flag applies the theme immediately and rebuilds the initramfs automatically.

4. Reboot and Enjoy

##Reboot your system to see the Plymouth splash screen with the new theme and delay:

    sudo reboot
