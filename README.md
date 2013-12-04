# dmenu-extended

An extension to dmenu allowing super fast access to your files, folders, and programs. Install the dmenu_extendedSettings plugin to further extend the menu - adding the ability to download new plugins and manage settings.

# Installation

dmenu-extended requires that dmenu is installed. While dmenu-extended works with older versions of dmenu, it is recommended that you have at least version 4.5 to enable fuzzy searching. If you already have dmenu installed you may [skip this step](#installing-dmenu-extended-this-extension).

## Prerequisite: Installing dmenu

Choose one of the following options to install dmenu

*Which option is best?* - Install using your package manager first - you can update dmenu at any time without breaking anything. If you find that searching isn't as good as it could be (e.g. on Debian) download and install from source to get the newest version of dmenu.

### Option A: Installing dmenu from your package manager
Installation command to install dmenu on the most popular linux distributions are:

#### Debian, Ubuntu, Linux-Mint

    sudo apt-get install suckless-tools
    
#### Fedora

    sudo yum install dmenu
    
#### Arch

    sudo pacman -S dmenu
    
Once installed, skip to [Installing dmenu-extended](#installing-dmenu-extended-this-extension)
    
### Option B: Installing dmenu from source

Before executing the following commands make sure you have installed `build-essential`, `libx11-dev` and `libxinerama-dev` from your package manager.
This can be done on Debian based systems (i.e. Ubuntu, Linux Mint) by executing the following in a terminal

    sudo apt-get install build-essential libx11-dev libxinerama-dev
  
Then, copy and paste the following block of code into your terminal to download and install dmenu 4.5
  
    cd /tmp && \
    wget http://dl.suckless.org/tools/dmenu-4.5.tar.gz && \
    tar -xzf dmenu-4.5.tar.gz && \
    cd dmenu-4.5 && \
    make && \
    sudo make install && \
    echo "dmenu has been installed"
    ;

## Installing dmenu-extended (this extension)

Installing this extension is as simple as copying and pasting the following block of code into a terminal and pressing enter.

    cd /tmp && \
    wget https://github.com/markjones112358/dmenu-extended/archive/master.zip && \
    unzip master.zip && \
    cd dmenu-extended-master && \
    sudo python setup.py install && \
    dmenu_extended_build && \
    cd /tmp && \
    sha1sum master.zip > ~/.config/dmenu-extended/signature.txt && \
    echo "" && \
    echo "FINISHED: dmenu-extended installation complete" && \
    echo "EXECUTE: dmenu_extended_run"
    ;
    

## Installing dmenu-extendedSettings (recommended)

Installing this extra extension enables rebuilding the cache, easy access to configuration files, and the ability to download and remove plugins.

To install this extension, copy and execute the following commands in a terminal

    cd ~/.config/dmenu-extended/plugins && \
    wget https://gist.github.com/markjones112358/7700097/raw/dmenuExtended_settings.py && \
    dmenu_extended_build && \
    echo "" && \
    echo "FINISHED: settings plugin installed" && \
    echo "Extension will appear in dmenu-extended on next run"
    ;

# Usage

## Create a keybinding

Test that the new menu has been installed by running `dmenu_extended_run` from your terminal. **NOTE:** The first run will be slow as it is set to scan you home folder recursively to build the cache.

The nicest way to enjoy dmenu-extended is to bind the command `dmenu_extended_run` to an easy to reach key-combination. The way in which you do this will be different depending on your desktop environment.

### Ubuntu (Unity), Debian (Gnome), Mint (Cinnamon)
1. Open **System settings** -> **Keyboard** -> **Shortcuts**
2. Click **Custom shortcuts** and then the **+** (*add custom shortcut*) to add a new command
3. Enter "dmenu_extended" as the name
4. Enter "dmenu_extended_run" as the command and click apply
5. Click next *disabled* (*unassigned*)
6. Press the desired combination of keys (e.g. Alt+Enter)

### Tiling window managers
If you use a tiling window manager, you may already have a key-combination bound to launch dmenu (i.e. Ctrl+P). Edit your window managers configuration file to launch `dmenu_extended_run` instead.

## Rebuilding the cache (without dmenu-extendedSettings)
Entering 'rebuild cache' into dmenu-extended or executing `dmenu_extended_build` rebuild the cache.

## General Configuration

Two json formatted configuration files are placed in *~/.config/dmenu-extended/* that control the appearance and functionality of the menu:
* **configuation.conf** - how the menu looks and the default programs used
* **user_preferences.conf** - contains a list folders to be indexed, file extensions to include, manually added entries, and more

If these files are saved with syntax errors they will be opened in the default text editor next time they are read. This happens *instead* of executing the requested action.

## Advanced usage
Dmenu-extended understands the following three modifier characters:

1. **+** (plus) - Add/remove the following item from the store
2. **:** (colon) - Open with
3. **;** (semi-colon) - Execute in terminal

These modifiers are entered into the menu; examples follow.

### **+** (plus) - Add/remove items from the store
If there is something you wish to run that isn't in the menu then you can add it by prepending with a +.

* `+gksudo shutdown now` will add 'gksudo shutdown now' to the index.
* `+libreoffice` will add libreoffice to the index.

The plus modifier also removes the item if it already exists in the store, or adds it if it does not. **Adding it a second time removes it from the index**

### **:** (colon) - Open with
There are a few different ways to use the colon operator, summarised by example below. In these examples `gedit` is the name of a text edititing application.

* `gedit:` - Use gEdit to open a file. A list of all files and folders will be returned to select from.
* `gedit:.txt` - Use gEdit to open a text file. A *filtered list* containing only text files will be shown to select from.
* `/home/me/Documents/writing.txt:` - Open this file using... Returns a list of applications to launch the given file
* `/home/me/Documents/writing.txt:gedit` - Open this file with gedit.

### **;** (semi-colon) - Execute in terminal
Dmenu-extended doesn't know when the application you enter needs to be executed in a terminal window. To tell dmenu-extended to launch the following in a terminal, append a semi-colon to the end.

For example,

* `htop;` - Launches htop in a terminal window. Without the semi-colon nothing would happen.
* `alsamixer;` - Launches the ALSA sound volume manager in a terminal. Without the semicolon nothing would happen.
