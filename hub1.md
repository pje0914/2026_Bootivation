sudo apt full-upgrade -y
sudo reboot

rpicam-hello --list-cameras

tr -d '\0' < /proc/device-tree/model; echo
grep -nE 'camera_auto_detect|dtoverlay=.*imx219' /boot/firmware/config.txt

sudo cp /boot/firmware/config.txt /boot/firmware/config.txt.bak
ls -l /boot/firmware/config.txt*
sudo nano /boot/firmware/config.txt
sudo reboot
-----------------------------------------------------------------------------------------
parkjueun@pje030914:~ $ rpicam-hello --list-cameras
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

parkjueun@pje030914:~ $ ^C
parkjueun@pje030914:~ $ 


# For more options and information see
# http://rptl.io/configtxt
# Some settings may impact device functionality. See link above for details

# Uncomment some or all of these to enable the optional hardware interfaces
#dtparam=i2c_arm=on
#dtparam=i2s=on
#dtparam=spi=on

# Enable audio (loads snd_bcm2835)
dtparam=audio=on

# Additional overlays and parameters are documented
# /boot/firmware/overlays/README

# Automatically load overlays for detected cameras
camera_auto_detect=0

# Automatically load overlays for detected DSI displays
display_auto_detect=1

# Automatically load initramfs files, if found
auto_initramfs=1

# Enable DRM VC4 V3D driver
dtoverlay=vc4-kms-v3d
max_framebuffers=2

# Don't have the firmware create an initial video= setting in cmdline.txt.
# Use the kernel's default instead.
disable_fw_kms_setup=1

# Run in 64-bit mode
arm_64bit=1

# Disable compensation for displays with overscan
disable_overscan=1

# Run as fast as firmware / board allows
arm_boost=1

[cm4]
# Enable host mode on the 2711 built-in XHCI USB controller.
# This line should be removed if the legacy DWC2 controller is required
# (e.g. for USB device mode) or if USB support is not required.
otg_mode=1

[cm5]
dtoverlay=dwc2,dr_mode=host

[pi5]
dtoverlay=nospi10

[all]
dtoverlay=imx219,cam0
dtoverlat=imx219,cam1



sudo dmesg | grep -iE 'imx219|rp1-cfe|i2c@80000|i2c@88000|failed|error'

arkjueun@pje030914:~ $ sudo dmesg | grep -iE 'imx219|rp1-cfe|i2c@80000|i2c@88000|failed|error'
[    0.029012] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[    0.029039] /axi/pcie@1000120000/rp1/csi@110000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[    0.029158] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[    0.029186] /axi/pcie@1000120000/rp1/csi@110000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[    0.579041] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[    0.579503] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[    0.579520] /axi/pcie@1000120000/rp1/csi@110000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[    3.115431] /axi/pcie@1000120000/rp1/csi@110000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[    3.115492] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[    3.294613] rp1-cfe 1f00110000.csi: DW dphy Host HW v1.20
[    3.294638] rp1-cfe 1f00110000.csi: PiSP FE HW v0.1
[    3.303281] rp1-cfe 1f00110000.csi: found subdevice /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[    3.681670] rp1-cfe 1f00110000.csi: Using sensor imx219 10-0010 for capture
[    3.684395] rp1-cfe 1f00110000.csi: Registered [rp1-cfe-csi2_ch0] node id 0 successfully as /dev/video0
[    3.685149] rp1-cfe 1f00110000.csi: Registered [rp1-cfe-embedded] node id 1 successfully as /dev/video1
[    3.685658] rp1-cfe 1f00110000.csi: Registered [rp1-cfe-csi2_ch2] node id 2 successfully as /dev/video2
[    3.686034] rp1-cfe 1f00110000.csi: Registered [rp1-cfe-csi2_ch3] node id 3 successfully as /dev/video3
[    3.686431] rp1-cfe 1f00110000.csi: Registered [rp1-cfe-fe_image0] node id 4 successfully as /dev/video4
[    3.687594] rp1-cfe 1f00110000.csi: Registered [rp1-cfe-fe_image1] node id 5 successfully as /dev/video5
[    3.702691] rp1-cfe 1f00110000.csi: Registered [rp1-cfe-fe_stats] node id 6 successfully as /dev/video6
[    3.703925] rp1-cfe 1f00110000.csi: Registered [rp1-cfe-fe_config] node id 7 successfully as /dev/video7
parkjueun@pje030914:~ $ 


