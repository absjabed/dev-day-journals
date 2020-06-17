## Wed 17/06/20
### The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging 
```sh
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
```

[solution](https://github.com/yarnpkg/yarn/issues/7866)
### Renewing all expired GPG signatures
```bash
sudo apt-key adv --refresh-keys --keyserver keyserver.ubuntu.com
```

### How can PPAs be removed? 
```bash
sudo add-apt-repository --remove ppa:whatever/ppa
```
[solution](https://askubuntu.com/questions/307/how-can-ppas-be-removed)


---
