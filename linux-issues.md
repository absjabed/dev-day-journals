## Tue 23/02/21
### Resize & Move linux **Swap partition** or **Swap file** from **SSD** to another partition
#### [Why are swap partitions discouraged on SSD drives, are they harmful?](https://askubuntu.com/questions/652337/why-are-swap-partitions-discouraged-on-ssd-drives-are-they-harmful)
- Open a new terminal.
- Use below commands to see current swap memory
```sh
  $ sudo swapon --show
  [sudo] password for abs: 
  NAME      TYPE      SIZE USED PRIO
  /dev/dm-1 partition 976M   0B   -2
  
  $ free -h
                  total        used        free      shared  buff/cache   available
    Mem:           15Gi       2.1Gi        11Gi       104Mi       1.7Gi        13Gi
    Swap:         975Mi          0B       975Mi
```
- Turnoff swap memory `$ sudo swapoff -a`
- Create a new file (example swapfile) with your desired size (example 4GB) and location `$ sudo fallocate -l 4G /dev/sdX/swap/swapfile`
- Change proper permissions `$ sudo chmod 600 /dev/sdX/swap/swapfile`
- Create the swapspace file with the new filename like **swapfile** `$ sudo mkswap /dev/sdX/swap/swapfile`
- and Start the swap file `$ sudo swapon /dev/sdX/swap/swapfile`
- To make this change permanent edit **/etc/fstab** file `$ sudo nano /etc/fstab`
- Add this line `/dev/sdX/swap/swapfile none   swap    sw      0       0` and comment out previous previous swap memory address.
- Save changes & Exit **Ctrl+O** -> **Ctrl+X**
- Now Restart your OS or run `$ sudo swapon --all --verbose` to start your new swapspace.
- To remove previous swapspace [check this-> swap-removing](https://web.mit.edu/rhel-doc/5/RHEL-5-manual/Deployment_Guide-en-US/s1-swap-removing.html)

[Reference-> How to move swap file to another physical disk](https://forums.linuxmint.com/viewtopic.php?t=317474)

[Reference-> How do I add swap after system installation?](https://askubuntu.com/questions/33697/how-do-i-add-swap-after-system-installation)

---

## Fri 20/12/20
### vscode unable to watch for file changes in this large workspace (watchman issue)
- Open a new terminal.
- `cat /proc/sys/fs/inotify/max_user_watches` (might be a number 8k+)
- `sudo nano /etc/sysctl.conf`
- go all the way down and add a new line with: `fs.inotify.max_user_watches=524288` (make sure you DONT have a # in front of the command)
- type **ctrl + x**, type **y** and press enter
- type `sudo sysctl -p`
- type again: cat /proc/sys/fs/inotify/max_user_watches (should be 500k+ now)

[Reference-> VSC unable to watch for file changes in this large workspace weird](https://stackoverflow.com/a/56292289/5277438)

---

## Wed 17/06/20
### The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging 
```sh
  curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
```
[Reference-> Yarn Debian key expiry date updated](https://github.com/yarnpkg/yarn/issues/7866)

### Renewing all expired GPG signatures
```bash	
sudo apt-key adv --refresh-keys --keyserver keyserver.ubuntu.com	
```

### How can PPAs be removed? 
```bash
  sudo add-apt-repository --remove ppa:whatever/ppa
```
[Reference-> How can PPAs be removed?](https://askubuntu.com/questions/307/how-can-ppas-be-removed)

---
