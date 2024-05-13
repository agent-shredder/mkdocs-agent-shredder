# sudoers File
```
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

dietpi ALL=(ALL) NOPASSWD: /home/dietpi/agent-shredder-stager/scripts/as-crypts$
dietpi ALL=(ALL) NOPASSWD: /home/dietpi/agent-shredder-stager/scripts/as-gadget
dietpi ALL=(ALL) NOPASSWD: /home/dietpi/agent-shredder-stager/scripts/as-utils
```

# polkit für udisks
`/etc/polkit-1/rules.d/10-udisks2.rules`

```
// See the polkit(8) man page for more information
// about configuring polkit.

// Allow udisks2 to mount devices without authentication
// for users in the "storage" group.
polkit.addRule(function(action, subject) {
    if ((action.id == "org.freedesktop.udisks2.filesystem-mount-system" ||
         action.id == "org.freedesktop.udisks2.filesystem-mount" ||
         action.id == "org.freedesktop.udisks2.filesystem-mount-other-seat") &&
        subject.isInGroup("storage")) {
        return polkit.Result.YES;
    }
});

```

`groupadd storage`
`usermod --append --groups storage dietpi`
`systemctl restart polkit.service`

# keyboard
for python lib *keyboard*

```
sudo chmod +0666 /dev/uinput
```
`/etc/udev/rules.d/12-input.rules`
```
SUBSYSTEM=="input", MODE="0666" GROUP="plugdev"
SUBSYSTEM=="misc", MODE="0666" GROUP="plugdev"
SUBSYSTEM=="tty", MODE="0666" GROUP="plugdev"
```
```
loginctl terminate-user $USER
```
logout/login/reboot

# Groups
```
sudo usermod -a -G tty,input,disk,i2c,storage dietpi
```
