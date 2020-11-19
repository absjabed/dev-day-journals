## Fri 20/12/20
### vscode unable to watch for file changes in this large workspace (watchman issue)
- Open a new terminal.
- `cat /proc/sys/fs/inotify/max_user_watches` (might be a number 8k+)
- `sudo nano /etc/sysctl.conf`
- go all the way down and add a new line with: `fs.inotify.max_user_watches=524288` (make sure you DONT have a # in front of the command)
- type **ctrl + x**, type **y** and press enter
- type `sudo sysctl -p`
- type again: cat /proc/sys/fs/inotify/max_user_watches (should be 500k+ now)

[Reference](https://stackoverflow.com/a/56292289/5277438)

---

## Wed 17/06/20
### The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging 
```sh
  curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
```
[Reference](https://github.com/yarnpkg/yarn/issues/7866)

### Renewing all expired GPG signatures
```bash	
sudo apt-key adv --refresh-keys --keyserver keyserver.ubuntu.com	
```

### How can PPAs be removed? 
```bash
  sudo add-apt-repository --remove ppa:whatever/ppa
```
[Reference](https://askubuntu.com/questions/307/how-can-ppas-be-removed)

---
