# socketserver
portable raspberry pi based server running syncthing and borgbackup

## Setup process:
* Flash Raspberry Pi OS on sd card. Run `sudo apt update && sudo apt full-upgrade` to enable booting from usb on older pi 4's.
* Flash either Raspberry Pi OS or Ubuntu Server 20.10 for rasberry pi on usb ssd
* set up wifi according to OS
* For enabling power button on pins 5 & 6, modify config.txt in boot partition, comment out `dtparam=i2c_arm=on` and add `dtoverlay=gpio-shutdown`. (File in repository)
* via apt install syncthing and borgbackup
* If Pi is headless: Edit syncthing config and change gui address from `127.0.0.1:8384` to `0.0.0.0:8384` to allow access from the network. https://docs.syncthing.net/users/config.html
* start syncthing service with `sudo systemctl start syncthing@.service`
* access gui, set password and configure synchronization
* create borgbackup repository https://borgbackup.readthedocs.io/en/stable/quickstart.html
* create backup script (working example in repository)
* add entry to users crontab by running `crontab -e` and adding the line `0 * * * * ~/syncthing_borg/backup_script.sh` (change path to location of your script). This entry runs the script every hour, thus performing a backup
* optional: add entry to root crontab to perform automated reboots. run `sudo crontab -e` and add `30 3 * * * shutdown -r now`. This reboots daily at 3:30 am.
* check if everything works ;D
