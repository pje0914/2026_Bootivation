sudo sed -n '/^\[all\]/,$p' /boot/firmware/config.txt | cat -A

dtoverlay -h imx219 | grep -A5 -B2 cam0

