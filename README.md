# Setting Up Windows Subsytem for Linux 2

### Requirements: Windows computer, 8+ GB ram
### Setup time: 10 minutes

This supplemental text is just an outline of the complete video walkthrough. Click here for the comprehensive video.

### Benefits of using Windows Subsystem for Linux 2:

- Follow Linux commands in class, just like a Linux/Mac user
- No need for GitBash for Windows
- No more Putty tools for ssh access to remote computers
- No more Sending files to yourself from a virtual machine

We are setting up Ubuntu in this walkthrough, but you can use any distro you are familiar with
through the Microsoft Store.

## Setting up Windows Terminal

* Press the Windows key and search for “Microsoft Store” → run it
* In Microsoft Store, search for “Windows Terminal” → click on the first option (furthest to the left). Press Install on the next screen.
* Use the keyboard shortcut `Windows + R` to open the Run window
* search for `shell:AppsFolder`
* In the new Explorer window that appears, find and Right-click on Windows Terminal
* create shortcut → yes to the popup menu

* Go to your Desktop and Right-click the new Windows Terminal shortcut
* Select `Properties` then use the keyboard shortcut `Ctrl` + `Alt` + `T` to set the shortcut.
* click Apply, then Ok

#### Now you can use the shortcut to open Terminal, just like Linux!

* Go back to Microsoft Store, search for “Ubuntu” click the `install` button
* While Ubuntu is installing, press the Windows key and search for Powershell, then Run as Administrator 
* Click yes to the pop up.

  > `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`
  
  > `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`

* Restart the computer
* Download the WSl 2 upgrade
  at https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
* Run the installation
* Open Powershell in Administrator Mode again
* Type command
  > `wsl --set-default-version 2`
* Keep Powershell open, we will come

## Install VcXsrv

#### VcXsrv will allow you to use your computer's display for WSL 2 applications

* Download VcXsrv at https://sourceforge.net/projects/vcxsrv/ and run the executable. It may take a minute to ask for permission to run.
    + click next
    + click install
    + wait for install
    + close it


* You will see a new desktop shortcut for "XLaunch". Run it.
    + Select Multiple windows → click next
    + Select Start no client → click next
    + Check all three boxes → click next
    + Save configuration as config.xlaunch to desktop
    + Click Finish
    + Check both boxes, then click "Allow access"

* Use `Windows + R` again to open the Run window
    + type `shell:startup` and press `Enter`
    + click and drag the newly-created `config.xlaunch` shortcut from the desktop into the startup folder.

### Now your couputer will automatically configure VcxSrv to allow WSL 2 to use you computer's display!

## Set up username and password on Ubuntu App

* Press the Windows key and search for “Ubuntu” from the Start menu → run it.
    + Wait for Ubuntu to prompt you for a username and password that you will not forget
        - Note: in Linux, the password characters do no appear. Sometimes it’s easier to write
          something in Notepad, copy it, then right-click once to paste it. This is easier to do
          with passwords, especially when you can’t see them.
    + Close Ubuntu

## Set up Ubuntu as the default profile for Windows Terminal

* Run Windows Terminal
    + At the top of Windows Terminal, notice you can have multiple tabs like a browser. Click on the `∨` button to get to a drop-down menu, and select Settings.
    + In the settings tab, choose Ubuntu as the new default profile, hit the save button toward the
      bottom, then close the settings tab
    + Click the `+` button to make a new tab.
    + Notice that you are now in Ubuntu. This is a more feature rich
      terminal than the One we set up username and password on. Basically, use this instead of using
      the Ubuntu app directly. close the original tab, which is running Powershell.

## Configure Ubuntu GUI apps to run in Windows

* One line at a time, copy paste this text block into the file:
    > sudo apt update -y && sudo apt upgrade -y<br>
    > sudo apt install ntpdate -y<br>
    > echo -e "sudo ntpdate time.windows.com\n" >> ~/.bashrc<br>
    > echo -e "export DISPLAY=$(grep -Po '(\d+\.\d+\.\d+\.\d+\.*)' /etc/resolv.conf):0.0\n" >> ~/.bashrc<br>
    > echo -e "export LIBGL_ALWAYS_INDIRECT=1\n" >> ~/.bashrc<br>
    > sudo apt install -y x11-apps<br>

* Start a new terminal and try opening a Linux gui application<br>
    > xeyes

    > xclac

#### You should now see a new window in the taskbar with a pair of eyes. Click on in. You are running gui applications from Ubuntu. Congratulations, your life just got a lot easier. Explore Bash and get familiar with it because it's about to be your best friend. Enjoy!
