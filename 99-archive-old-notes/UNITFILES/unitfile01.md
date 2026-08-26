
# Dummy Python App Systemd Unit File

Below is an example of a systemd unit file to run a dummy Python app as a service.

Create a file named `my-python-app.service` in `/etc/systemd/system/`:

[Unit]
Description=Dummy Python App Service
After=network.target

[Service]
Type=simple
User=ec2.user
WorkingDirectory=/path/to/your/app
ExecStart=/usr/bin/python3 /path/to/your/app/app.py
Restart=on-failure

[Install]
WantedBy=multi-user.target


