# Update Remove and Installing software

At this writing the CHIP OS i am using is _**headless os 4.4**_ .

### Stuff to Remove

* avahi

```
sudo apt-get remove --auto-remove avahi-daemon
sudo apt-get purge --auto-remove avahi-daemon
```

### Stuff to Update

* update and upgrade

```
sudo apt-get update
sudo apt-get upgrade
```

### Stuff to add

* GCC stuff for programing with

```
sudo apt-get install build-essential
```

* Git to make life pullable

Note change the username and useremail@place.com below to be the correct information for git!

```
sudo apt-get install git-core
git config --global user.name "username"
git config --global user.email useremail@place.com
```

* Gforth stuff to use it and its tools!

[My gforth install post for raspberry pi device](https://www.raspberrypi.org/forums/viewtopic.php?f=34&t=43300)

There are a few basic steps.  First install the debian gforth current version and some dependency's needed for the next step.
Second get the latest debian package version.  The raspberry pi instructions could be used loosly to compile from sources but to
get the most bleeding edge version from source and then compile it locally but this seems to not all be working on the CHIP device.

```
sudo apt-get install libtool libtool-bin libltdl-dev libffi-dev autoconf m4 gforth
```

_*note libtool-bin is needed because there is some issue in jessy but the normal way to install was just use libtool*_
This installs the most recent gforth that is available in Debian.  If you type `gforth` now at the command line you should see something like the following:

```
Gforth 0.7.2, Copyright (C) 1995-2008 Free Software Foundation, Inc.
Gforth comes with ABSOLUTELY NO WARRANTY; for details type `license'
Type `bye' to exit
```

Just type `bye` to exit the gforth command line environment.  Continue to get the a newer debian package for gforth.

```
sudo wget http://www.complang.tuwien.ac.at/forth/gforth/Snapshots/0.7.9_20160306/gforth-common_0.7.9-20160306_all.deb
sudo wget http://www.complang.tuwien.ac.at/forth/gforth/Snapshots/0.7.9_20160306/gforth-bin_0.7.9-20160306_armhf.deb
sudo wget http://www.complang.tuwien.ac.at/forth/gforth/Snapshots/0.7.9_20160306/gforth-lib_0.7.9-20160306_armhf.deb
sudo wget http://www.complang.tuwien.ac.at/forth/gforth/Snapshots/0.7.9_20160306/gforth_0.7.9-20160306_armhf.deb

sudo dpkg -i gforth-common_0.7.9-20160306_all.deb
sudo dpkg -i gforth-bin_0.7.9-20160306_armhf.deb
sudo dpkg -i gforth-lib_0.7.9-20160306_armhf.deb
sudo dpkg -i gforth_0.7.9-20160306_armhf.deb

sudo apt-get install -f
```

This gets and installs the latest debian package. So now at the command line if you invoke `gforth` you should see the following:

```
Gforth 0.7.9_20160306, Copyright (C) 1995-2015 Free Software Foundation, Inc.
Gforth comes with ABSOLUTELY NO WARRANTY; for details type `license'
Type `bye' to exit
```

Again you can exit with `bye`.  

At this moment you have a newer version of Gforth but for the bleeding edge version do the following:

```
sudo wget http://www.complang.tuwien.ac.at/forth/gforth/Snapshots/0.7.9_20161109/gforth-0.7.9_20161109.tar.xz
sudo tar -xf gforth-0.7.9_20161109.tar.xz
cd gforth-0.7.9_20161109
sudo ./BUILD-FROM-SCRATCH
```

This will take some time and generate many messages of which some will look like error messages.   Just ignore them until it is done then do the following:

```
sudo make
sudo make install
cd ..
```

At the command line `gforth` will bring up version 0.7.9_20150306.  And `gforth-arm` will now bring up version 0.7.9_20161109.  These names are sim links that could be changed to work in any way you want.  This means that both version of gforth are now available so be aware what version you are using.  I have not tested this but if you later redo this setup to install even a newer version then only the original version and the newest version will work with these sim links but all three version will be on the system.  This means that you may want to simply change the sim links to point to what ever version you want to use!

* Apache web server install and setup with cgi turned on

[CHIP Apache setup information](http://www.chip-community.org/index.php/CGI_program_on_CHIP)
I have summarized the information here from the link with some changes.  

```
sudo apt-get install apache2
cd /etc/apache2/mods-enabled
sudo ln -s ../mods-available/cgi.load
sudo apachectl -k graceful
```

At this moment Apache is running and the _*index.html*_ file should be changed in this directory `/var/www/html/`.
The cgi code should be placed at `/usr/lib/cgi-bin/` and given the correct privileges.
So basically these two directory's are the places to put stuff to be accessed remotely on the network.

Gforth script can be in a simple file that has or does not have an extension.  The file needs the following in its first line:

```
#! /usr/local/bin/gforth-arm
```

This first line simply tells the system where the gforth engine is located in the system that is to be used with the script.  
Once you make the gforth script and save it you need to change its permissions to be executable as follows:

```
sudo chmod +x name-of-cgi-code
```

You can test and access the files served locally by using any of the commands below.

```
ping localhost
wget localhost/cgi-bin/name-of-cgi-code
wget localhost
```

Each of the above lines will give different information but they should all show the system working!

* Install and setup mail program sSMTP

  * Install

  ```
  sudo apt-get install ssmtp  mailutils mpack
  ```

  * Configure

  ```
  sudo nano /etc/ssmtp/ssmtp.conf
  ```

  Add the following or edit the following lines:

  ```
  root=mygmail@gmail.com  # put my real email address here.
  mailhub=smtp.gmail.com:587
  rewriteDomain=gmail.com
  hostname=localhost
  FromLineOverride=YES
  UseTLS=YES
  UseSTARTTLS=YES
  AuthUser=myusername  # put my real gmail user name less the @gmail.com
  AuthPass=mypassword  # put my generated application password here see note below
  AuthMethod=LOGIN
  ```

  The password above needs to be generated and maintained at [googles account application password pages](https://security.google.com/settings/security/apppasswords) so it is not my normal password!

  * Test the mail
    ```
    echo "A message from chip!" | mail -s "Test Mail" youremail.address@mail.com  
    ```
    Check you email for this test message!  Note the above ssmtp installation does not need to be restarted after the setup so this test email should arrive soon!
