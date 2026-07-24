sudo sed -n '/^\[all\]/,$p' /boot/firmware/config.txt | cat -A

dtoverlay -h imx219 | grep -A5 -B2 cam0

parkjueun@pje030914:~ $ 
rpicam-hello --list-cameras
Available cameras
-----------------
0 : imx219 [3280x2464 10-bit RGGB] (/base/axi/pcie@1000120000/rp1/i2c@88000/imx219@10)
    Modes: 'SRGGB10_CSI2P' : 640x480 [200.16 fps - (1000, 752)/1280x960 crop]
                             1640x1232 [81.07 fps - (0, 0)/3280x2464 crop]
                             1920x1080 [47.57 fps - (680, 692)/1920x1080 crop]
                             3280x2464 [21.19 fps - (0, 0)/3280x2464 crop]
           'SRGGB8' : 640x480 [200.16 fps - (1000, 752)/1280x960 crop]
                      1640x1232 [81.07 fps - (0, 0)/3280x2464 crop]
                      1920x1080 [47.57 fps - (680, 692)/1920x1080 crop]
                      3280x2464 [21.19 fps - (0, 0)/3280x2464 crop]

parkjueun@pje030914:~ $ ~sudo sed -n '/^\[all\]/,$p' /boot/firmware/config.txt | cat -A
bash: ~sudo: 명령어를 찾을 수 없음
parkjueun@pje030914:~ $ dtoverlay -h imx219 | grep -A5 -B2 cam0
        media-controller        Configure use of Media Controller API for
                                configuring the sensor (default on)
        cam0                    Adopt the default configuration for CAM0 on a
                                Compute Module (CSI0, i2c_vc, and cam0_reg).
        vcm                     Configure a VCM focus drive on the sensor.
        4lane                   Enable 4 CSI2 lanes. This requires a Compute
                                Module (1, 3, 4, or 5) or Pi 5.

parkjueun@pje030914:~ $ ^C
parkjueun@pje030914:~ $ 

un@pje030914:~ $ ^C
parkjueun@pje030914:~ $ sudo sed -n '/^\[all\]/,$p' /boot/firmware/config.txt | cat -A
[all]$
dtoverlay=imx219,cam0$
dtoverlat=imx219$
$
parkjueun@pje030914:~ $ ^C


sudo sed -i 's/^dtoverlat=imx219$/dtoverlay=imx219/' /boot/firmware/config.txt
sudo sed -n '/^\[all\]/,$p' /boot/firmware/config.txt
