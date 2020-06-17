## Wed 17/06/20
### The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging 
```sh
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
```

[solution](https://github.com/yarnpkg/yarn/issues/7866)

### Renewing all expired GPG signatures
```sh
sudo apt-key adv --refresh-keys --keyserver keyserver.ubuntu.com
```
---
