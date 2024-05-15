cryptocontainer erstellen:
``` shell
truncate -s <size> <containerfile>
echo -n <password> | cryptsetup -c aes-xts-plain64 -s 512 -h sha512 -y luksFormat <containerfile> -d -
```

öffnen so:
``` shell
echo -n <password> | sudo /usr/sbin/cryptsetup luksOpen <containerfile> <cryptdevicename> -d -
```
