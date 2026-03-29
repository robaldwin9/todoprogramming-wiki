---
title: Systemd
description: 
published: true
date: 2025-03-23T19:20:50.161Z
tags: 
editor: markdown
dateCreated: 2024-10-20T17:39:22.072Z
---

# Systemd Cheat Sheet

## Service files
service files are located at `/etc/systemd/system` services are often time applications ran at statrtup.

### Create a service file
Instructions for creating a service file. Typically I create a `start.sh` script for each application so that all services will have a similar `ExecStart` line. If using `start.sh` be sure to use `chmod +x start.sh` to make the startup script executable.

1. `sudo touch /etc/systemd/system/<service>.service` to create your service file

2. `sudo nano /etc/systemd/system/<service>.service` to edit

```
[Unit]
Description=Pixoo Discord Bot                                  # Name of your service
Wants=network.target                                           # Indicates service needs to be stopped before network shutdown                            
After=syslog.target network-online.target                      # Start service after network is online

[Service]
Type=simple                                                    # The default value. The process started with ExecStart is the main process of the service.
ExecStart=/bin/bash /home/<user>/pixoobot/start.sh             # Replace with the actual path to your JAR file
user=root                                                      # User to execute application under
Restart=on-failure                                             # Restart application if it dies
RestartSec=10                                                  # Duration to wait for restart on failure

[Install]
WantedBy=multi-user.target                                     # means that the custom service will start when systemd loads 
```

3. `systemctl daemon-reload` loads service file changes
4. `systemctl restart <service>`
5. `journalctl -fu <service>` to watch logs and verify started



## Usefull Systemctl Commands

List running services
`systemctl`

Start a service
`systemctl start <service>`

Stop a service
`systemctl stop <service>`

Restart a service
`systemctl restart <service>`

Show status of a service
`systemctl status <service>`

Enable service to start on boot
`systemctl enable <service>`

Disable service start on boot
`systemctl disable <service>`

Check if service is enabled
`systemctl is-enabled <service>`

