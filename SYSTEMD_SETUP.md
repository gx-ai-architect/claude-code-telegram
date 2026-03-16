# Systemd User Service Setup

This guide shows how to run Lockstep as a persistent systemd user service.

**⚠️ SECURITY NOTE:** Before setting up the service, ensure your `.env` file has `DEVELOPMENT_MODE=false` and `ENVIRONMENT=production` for secure operation.

## Quick Setup

### 1. Create the service file

```bash
mkdir -p ~/.config/systemd/user
nano ~/.config/systemd/user/lockstep.service
```

Add this content:

```ini
[Unit]
Description=Lockstep
After=network.target

[Service]
Type=simple
WorkingDirectory=/home/ubuntu/Code/oss/lockstep
ExecStart=/home/ubuntu/.local/bin/poetry run lockstep
Restart=always
RestartSec=10
StandardOutput=journal
StandardError=journal

# Environment
Environment="PATH=/home/ubuntu/.local/bin:/usr/local/bin:/usr/bin:/bin"

[Install]
WantedBy=default.target
```

**Note:** Update `WorkingDirectory` to your project path.

### 2. Enable and start the service

```bash
# Reload systemd to recognize the new service
systemctl --user daemon-reload

# Enable auto-start on login
systemctl --user enable lockstep.service

# Start the service now
systemctl --user start lockstep.service
```

### 3. Verify it's running

```bash
systemctl --user status lockstep
```

### 4. Verify secure configuration

Check that the service is running in production mode:

```bash
# Check logs for environment mode
journalctl --user -u lockstep -n 50 | grep -i "environment\|development"

# Should show:
# "environment": "production"
# "development_mode": false (implied, not shown if false)

# Verify authentication is restricted
journalctl --user -u lockstep -n 50 | grep -i "auth"

# Should show:
# "allowed_users": 1 (or more if multiple users configured)
# "allow_all_dev": false
```

If you see `allow_all_dev: true` or `environment: development`, **STOP THE SERVICE** and fix your `.env` file immediately.

## Common Commands

```bash
# Start service
systemctl --user start lockstep

# Stop service
systemctl --user stop lockstep

# Restart service
systemctl --user restart lockstep

# View status
systemctl --user status lockstep

# View live logs
journalctl --user -u lockstep -f

# View recent logs (last 50 lines)
journalctl --user -u lockstep -n 50

# Disable auto-start
systemctl --user disable lockstep

# Enable auto-start
systemctl --user enable lockstep
```

## Updating the Service

After editing the service file:

```bash
systemctl --user daemon-reload
systemctl --user restart lockstep
```

## Troubleshooting

**Service won't start:**
```bash
# Check logs for errors
journalctl --user -u lockstep -n 100

# Verify paths in service file are correct
systemctl --user cat lockstep

# Check that Poetry is installed
poetry --version

# Test the bot manually first
cd /home/ubuntu/Code/oss/lockstep
poetry run lockstep
```

**Service stops after logout:**

Enable lingering to keep user services running after logout:
```bash
loginctl enable-linger $USER
```

## Files

- Service file: `~/.config/systemd/user/lockstep.service`
- Logs: View with `journalctl --user -u lockstep`
- Project: `/home/ubuntu/Code/oss/lockstep`
