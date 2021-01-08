# Teaching Textbooks 4.0 on Linux

Teaching Textbooks (https://teachingtextbooks.com) is a computer-based math course for elementary through high school students. Their 3.0 web version was designed to use Flash Player, which had its end of life January, 2021. Their 4.0 version supports Windows, Mac OS, and Chromebook/Android. Unfortunately, this leaves Linux users hung out to dry.

## The Workaround - ANBOX
Anbox, short for "Android Box" is an android emulator that runs on Linux. When correctly set up, it can run ChromeOS and Android apps on your Linux computer.

## Installing

Even if you are not familiar with the Linux terminal you can do this though it does help to know a bit about Linux. If you're unsure, ask your student if they want to follow these instructions and learn how to use the terminal. One of our students has become a Linux wizard, and would rather type commands than click the mouse!

Run the following commands in the terminal (Control-Alt-T will open a new terminal). If prompted for your password on any of the `sudo` commands, enter your Linux user password to continue.

## Prerequisites
Some versions of Ubuntu and Mint come with the required Anbox modules already installed. If the either of the following commands results in an error, you must to complete this **Prerequisites** section. Otherwise, continue with the **General Installation** section.

```
sudo modprobe ashmem_linux
sudo modprobe binder_linux
```

### Ubuntu Linux
Ubuntu 19 and higher should come with the modules pre-installed. If you are running an older version, or the above commands worked, you can skip this section.

```
# Skip the following line if you already have the modules installed
sudo apt install anbox-modules-dkms
```

### Mint Linux
It seems that the newest version of Mint still may not ship with the Anbox modules installed. If the above `modprobe` commands ran without error, you may skip this section. We don't have Mint, so we can't directly test this out. Please open an issue if the following is incorrect and we will update the guide accordingly.

```
sudo add-apt-repository ppa:morphis/anbox-support
sudo apt update
sudo apt install linux-headers-generic anbox-modules-dkms

sudo modprobe ashmem_linux
sudo modprobe binder_linux
```

### General Install

The rest of the commands below should get Anbox installed and running:
```
# Install some required utilities
sudo apt-get install -y curl lzip squashfs-tools wget unzip tar

# Activate the required modules
sudo modprobe ashmem_linux
sudo modprobe binder_linux

# Enable the modules to load on restart
echo "ashmem_linux" | sudo tee -a /etc/modules-load.d/anbox.conf
echo "binder_linux" | sudo tee -a /etc/modules-load.d/anbox.conf

# Install anbox using the Snap installer
snap install --devmode --beta anbox

# Download the script to install Google Play Store on Anbox
wget https://raw.githubusercontent.com/geeks-r-us/anbox-playstore-installer/master/install-playstore.sh
chmod 755 install-playstore.sh

# Run the Google Play Store install (takes several minutes)
./install-playstore.sh

```

### Sign in and install the TT App
* Look in your start menu and look for Anbox, and run it.
* Click on the Google Play Store icon, and sign in with your Google account.
* Search for the correct TT app in Play Store and install it.
* Once installed, click on the TT app icon, sign in with your parent account and proceed as normal.

## Student Instructions
Once set up, your student will run Anbox from the start menu, then click on the TT app icon in Anbox. One extra step for them, but allows them to use Teaching Textbooks 4.0 on Linux.

## Known Issues
* On some computers Anbox won't start the very first time. If it shows a "Loading..." screen, then exits, try running it a second time. If it still doesn't start, try running `anbox session-manager` from the terminal before clicking on the Anbox icon again.
* During the initial setup, the screen sometimes doesn't refresh. If it appears to have frozen, click on a different Anbox window, then go back to the TT window. Our student hasn't noticed any other glitching while using the app on a regular basis.

## Questions?
If you have any questions, please open an issue on this project and we'll do our best to answer. Note, we are NOT affiliated with Teaching Textbooks, but rather home educators who prefer to use Linux on our computers, and always happy to help!
