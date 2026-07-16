pje0914@ParkJuEun:~/ssg_ssac_setup $   sudo grep -RniE \
'camera_auto_detect|dtoverlay=(imx219|imx708|ov5647|imx477|imx296)' \
/boot/firmware 2>/dev/null

/boot/firmware/overlays/README:2808:Load:   dtoverlay=imx219,<param>=<val>
/boot/firmware/overlays/README:2890:Load:   dtoverlay=imx296,<param>=<val>
/boot/firmware/overlays/README:3031:Load:   dtoverlay=imx477,<param>=<val>
/boot/firmware/overlays/README:3090:Load:   dtoverlay=imx708,<param>=<val>
/boot/firmware/overlays/README:3707:Load:   dtoverlay=ov5647,<param>=<val>
/boot/firmware/config.txt:2:camera_auto_detect=0
/boot/firmware/config.txt:5:dtoverlay=imx219,cam0
/boot/firmware/config.txt:6:dtoverlay=imx219,cam1
/boot/firmware/config.txt:23:camera_auto_detect=1
pje0914@ParkJuEun:~/ssg_ssac_setup $ sudo nl -ba /boot/firmware/config.txt | sed -n '1,120p'
     1	# 자동 감지를 0으로 바꿉니다
     2	camera_auto_detect=0
     3	
     4	# 파일 맨 아래에 아래 두 줄을 추가합니다 (IMX219 카메라 기준)
     5	dtoverlay=imx219,cam0
     6	dtoverlay=imx219,cam1
     7	# For more options and information see
     8	# http://rptl.io/configtxt
     9	# Some settings may impact device functionality. See link above for details
    10	
    11	# Uncomment some or all of these to enable the optional hardware interfaces
    12	#dtparam=i2c_arm=on
    13	#dtparam=i2s=on
    14	#dtparam=spi=on
    15	
    16	# Enable audio (loads snd_bcm2835)
    17	dtparam=audio=on
    18	
    19	# Additional overlays and parameters are documented
    20	# /boot/firmware/overlays/README
    21	
    22	# Automatically load overlays for detected cameras
    23	camera_auto_detect=1
    24	
    25	# Automatically load overlays for detected DSI displays
    26	display_auto_detect=1
    27	
    28	# Automatically load initramfs files, if found
    29	auto_initramfs=1
    30	
    31	# Enable DRM VC4 V3D driver
    32	dtoverlay=vc4-kms-v3d
    33	max_framebuffers=2
    34	
    35	# Don't have the firmware create an initial video= setting in cmdline.txt.
    36	# Use the kernel's default instead.
    37	disable_fw_kms_setup=1
    38	
    39	# Run in 64-bit mode
    40	arm_64bit=1
    41	
    42	# Disable compensation for displays with overscan
    43	disable_overscan=1
    44	
    45	# Run as fast as firmware / board allows
    46	arm_boost=1
    47	
    48	[cm4]
    49	# Enable host mode on the 2711 built-in XHCI USB controller.
    50	# This line should be removed if the legacy DWC2 controller is required
    51	# (e.g. for USB device mode) or if USB support is not required.
    52	otg_mode=1
    53	
    54	[cm5]
    55	dtoverlay=dwc2,dr_mode=host
    56	
    57	[all]
