sudo apt full-upgrade -y
sudo reboot

rpicam-hello --list-cameras

tr -d '\0' < /proc/device-tree/model; echo
grep -nE 'camera_auto_detect|dtoverlay=.*imx219' /boot/firmware/config.txt

sudo cp /boot/firmware/config.txt /boot/firmware/config.txt.bak
ls -l /boot/firmware/config.txt*
sudo nano /boot/firmware/config.txt
sudo reboot
