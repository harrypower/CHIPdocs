# Update Remove and Installing software

At this writing the CHIP OS i am using is ** *headless os 4.4* ** .

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
