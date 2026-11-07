# Dummy Systemd Service

## Project Overview

This project demonstrates how to create and manage a custom Linux systemd service using Bash.

The objective is to create a Bash script that prints a message with the current date and time every 10 seconds, then configure systemd to run and manage it in the background.

## Technologies Used

- Ubuntu Linux
- Bash
- systemd
- GNU Nano
- Oracle VirtualBox

## Project Structure

```text
02-systemd-service/
├── dummy.sh
├── dummy.service
├── README.md
└── screenshots/
    └── service-status.png
```

## Implementation

### 1. Create the Bash script

Create the script:

```bash
nano dummy.sh
```

The script uses:

- `#!/bin/bash` – specifies the Bash interpreter.
- `echo` – prints messages.
- `date` – displays the current date and time.
- `while true` – creates a continuous loop.
- `sleep 10` – pauses execution for 10 seconds.

Make the script executable:

```bash
chmod +x dummy.sh
```

Run it:

```bash
./dummy.sh
```

Press `CTRL + C` to stop manual execution.

### 2. Create the systemd service

Find the absolute path:

```bash
realpath dummy.sh
```

Create the service configuration:

```bash
nano dummy.service
```

The service file contains three sections:

- `[Unit]` – service description and dependencies.
- `[Service]` – execution and restart configuration.
- `[Install]` – startup configuration.

Configuration:

```ini
[Unit]
Description=Dummy systemd service
After=network.target

[Service]
Type=simple
ExecStart=/home/rollie/Desktop/devops-journey/phase-1-foundations/02-systemd-service/dummy.sh
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

### 3. Validate and install the service

Validate the configuration:

```bash
systemd-analyze verify dummy.service
```

Install the service:

```bash
sudo cp dummy.service /etc/systemd/system/dummy.service
```

Reload systemd:

```bash
sudo systemctl daemon-reload
```

### 4. Start and manage the service

Start the service:

```bash
sudo systemctl start dummy
```

Check its status:

```bash
sudo systemctl status dummy
```

Enable automatic startup:

```bash
sudo systemctl enable dummy
```

Check whether it is enabled:

```bash
systemctl is-enabled dummy
```

### 5. Monitor service logs

```bash
sudo journalctl -u dummy -f
```

Press `CTRL + C` to exit log monitoring without stopping the service.

### 6. Useful systemd commands

| Command                      | Purpose                     |
| ---------------------------- | --------------------------- |
| `systemctl start dummy`      | Start service               |
| `systemctl stop dummy`       | Stop service                |
| `systemctl restart dummy`    | Restart service             |
| `systemctl status dummy`     | Check status                |
| `systemctl enable dummy`     | Enable at boot              |
| `systemctl disable dummy`    | Disable automatic startup   |
| `systemctl is-enabled dummy` | Check startup configuration |
| `journalctl -u dummy -f`     | Follow service logs         |

## Problems I Hit and How I Fixed Them

**1. Continuous script output**

The `while true` loop printed messages continuously. I learned to use `sleep` inside the loop to control execution intervals.

**2. Script execution and permissions**

Initially, I used `bash dummy.sh`. I learned to use `chmod +x dummy.sh` to make the script executable and run it using `./dummy.sh`.

**3. Incorrect systemd configuration syntax**

I initially used descriptive labels instead of actual systemd directives. I learned to use the correct `Property=value` format.

**4. Incorrect capitalization**

I wrote `Execstart` instead of `ExecStart`. I corrected the capitalization because systemd directives are case-sensitive.

**5. Absolute file paths**

I needed to identify the exact location of my script. I learned to use `realpath dummy.sh` and provide that path in `ExecStart`.

**6. Service validation**

I used `systemd-analyze verify dummy.service` to check the configuration before installation. It returned no output, indicating no reported configuration errors.

**7. Starting versus enabling services**

I learned that `systemctl start` runs a service immediately, while `systemctl enable` configures it to start automatically during boot.

## What I Learned

- Bash scripting fundamentals.
- Variables, commands and loops (introductory practice).
- Linux file permissions and executable scripts.
- Absolute file paths.
- systemd service configuration.
- Starting, stopping and enabling services.
- Monitoring services and viewing logs.
- Understanding automatic service restart policies.

## Project Status

- [x] Bash script created and executed.
- [x] Script made executable.
- [x] systemd unit file created.
- [x] Configuration validated.
- [x] Service installed and started.
- [x] Service status confirmed as `active (running)`.
- [x] Service logs captured.
- [x] Automatic restart tested.
- [x] Screenshot added.

## Screenshot

The `screenshots/` directory will contain a screenshot showing the running service.

## Repository

GitHub: [https://github.com/robert6111/devops-journey](https://github.com/robert6111/devops-journey)

