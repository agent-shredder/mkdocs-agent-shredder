# Agent Shredder Service
`/etc/systemd/system/agent-shredder.service`

```
[Unit]
Description=Agent Shredder
After=local-fs.target
Before=network.target

[Service]
Type=simple
RemainAfterExit=yes
User=root
ExecStart=/home/dietpi/agent-shredder-stager/stager.py

[Install]
WantedBy=network.target

```