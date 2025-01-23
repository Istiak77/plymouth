Plymouth Setup on Arch Linux

###clone this repo :

    git clone https://github.com/Istiak77/SteamDeck-BootAnimation-Plymouth

    
###Move the Steam folder to 

    /usr/share/plymouth/themes/

    
###THEME CREDIT GOES TO - MagiBoot-D3bootanimations


### https://t.me/MagiBoot




<iframe width="1920" height="826" src="https://www.youtube.com/embed/DtGghJxokEM" title="Steam Deck Boot Animation on Arch linux" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>




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


3. Adding a Delay Script

##To add a delay during the boot process (e.g., to see the Plymouth animation longer), create a custom initramfs hook.

#Create the Delay Hook

#Create a new hook file:

	sudo nano /etc/initcpio/hooks/plymouth-delay

#Add the following content to the file:

    #!/bin/bash
    run_hook() {
        # Show the Plymouth splash screen
        plymouth --show-splash
        
        # Add a delay (in seconds)
        sleep 5  # Adjust the delay as needed (e.g., 5 seconds)
    }

#Make the hook executable:
    
    sudo chmod +x /etc/initcpio/hooks/plymouth-delay


##Add the Hook to Initramfs

#Open the initramfs configuration file:

    sudo nano /etc/mkinitcpio.conf

#Add plymouth-delay and plymouth to the HOOKS array. Place plymouth-delay before plymouth:

    HOOKS=(base udev autodetect microcode modconf kms keyboard keymap consolefont block filesystems fsck plymouth-delay plymouth)


#Save the file and rebuild the initramfs:
    
    sudo mkinitcpio -P

4. Changing Themes

##List Available Themes

#To see the list of available Plymouth themes, run:


	plymouth-set-default-theme -l


##Set a New Theme

#To set a new theme (Steam), use the following command:


	sudo plymouth-set-default-theme -R Steam


#The -R flag applies the theme immediately and rebuilds the initramfs automatically.

5. Reboot and Enjoy

##Reboot your system to see the Plymouth splash screen with the new theme and delay:

    sudo reboot
