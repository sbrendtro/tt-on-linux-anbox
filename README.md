# Teaching Textbooks 4.0 on Linux

Teaching Textbooks (https://teachingtextbooks.com) is a computer-based math course for elementary through high school students. Their 3.0 web version was designed to use Flash Player, which had its end of life January, 2021. Their 4.0 version supports Windows, Mac OS, and Chromebook/Android. Unfortunately, this leaves Linux users hung out to dry.

## The Workaround - ANBOX
Anbox, short for "Android Box" is an android emulator that runs on Linux. When correctly set up, it can run ChromeOS and Android apps on your Linux computer.

## Installing

Even if you are not familiar with the Linux terminal you can do this though it does help to know a bit about Linux. If you're unsure, ask your student if they 

Run the following commands in the terminal (Control-T will open a new terminal). If prompted for your password on any of the `sudo` commands, enter your Linux user password to continue.

First, if you are running Ubuntu 18 or Mint 18, you will need to first install a module package. __If you are running Ubuntu 19 or higher, or Mint 19 or higher, you can skip this step, as these versions come with the modules pre-installed.__


```
# Skip the following line if you are running Ubuntu/Mint 19 or higher
sudo apt install anbox-modules-dkms
```

The rest of the commands below should get Anbox installed and running:
```
# Install some required utilities
sudo apt-get install -y curl lzip squashfs-tools wget unzip tar

# Activate the required modules
sudo modprobe ashmem_linux
sudo modprobe binder_linux

# Enable the modules to loaded on restart
echo "ashmem_linux\nbinder_linux" | sudo tee /etc/modules-load.d/anbox.conf

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
