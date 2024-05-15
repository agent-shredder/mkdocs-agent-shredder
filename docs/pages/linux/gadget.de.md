# Mass Storage

# Serial

``` systemd title="/etc/systemd/system/usbcon.service"
[Unit]
Description=USB console on ttyGS0

#ConditionKernelCommandLine=usbcon

[Service]
Type=oneshot
RemainAfterExit=yes

ExecStart=/sbin/modprobe g_serial
ExecStart=/bin/systemctl start serial-getty@ttyGS0.service

ExecStop=/bin/systemctl stop serial-getty@ttyGS0.service
ExecStop=/sbin/modprobe -r g_serial

[Install]
WantedBy=getty.target

```