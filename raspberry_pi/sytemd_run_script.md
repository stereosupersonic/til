# run any script at startup with systemd

1. Create a new unit file in `/lib/systemd/system/` called `rpi-lcd.service`:
   ```sh
   sudo vim /lib/systemd/system/rpi-lcd.service
   ```

2. Copy and paste the following in the new unit file:
   ```sh
   [Unit]
   Description=RPi Python script for a 16x2 LCD

   [Service]
   Type=simple
   ## Edit the following according to the script permissions
   User=root # or pi or 
   #Group=users

   ## Edit the following with the full path to the compatible Python version and your script
   ExecStart=/usr/bin/python3 /home/stereosonic/raspi-lcd-16x2/lcd.py

   Restart=always
   RestartSec=5

   KillMode=process
   KillSignal=SIGINT

   [Install]
   WantedBy=multi-user.target
   ```

3. Enable the service and start it:
   ```sh
   sudo systemctl enable rpi-lcd.service
   sudo systemctl start rpi-lcd.service
   ```

4. Check that the LCD is displaying the correct information; otherwise, check the service status:
   ```sh
   systemctl status rpi-lcd.service
   ```
