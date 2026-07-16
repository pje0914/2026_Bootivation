  echo
  echo "===== BOARD MODEL ====="
  tr -d '\0' < /proc/device-tree/model
  echo

  echo
  echo "===== KERNEL ====="
  uname -a

  echo
  echo "===== CAMERA COMMAND ====="
  command -v rpicam-hello || command -v libcamera-hello || true

  echo
  echo "===== POWER / THROTTLE ====="
  vcgencmd get_throttled 2>/dev/null || true
} | tee system_info.txt
===== OS =====
PRETTY_NAME="Debian GNU/Linux 13 (trixie)"
NAME="Debian GNU/Linux"
VERSION_ID="13"
VERSION="13 (trixie)"
VERSION_CODENAME=trixie
DEBIAN_VERSION_FULL=13.3
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"

===== BOARD MODEL =====
Raspberry Pi 5 Model B Rev 1.0

===== KERNEL =====
Linux ParkJuEun 6.12.62+rpt-rpi-2712 #1 SMP PREEMPT Debian 1:6.12.62-1+rpt1 (2025-12-18) aarch64 GNU/Linux

===== CAMERA COMMAND =====
/usr/bin/rpicam-hello

===== POWER / THROTTLE =====
throttled=0x0
pje0914@ParkJuEun:~/ssg_ssac_setup $ rpicam-hello --version
rpicam-apps build: v1.11.0 18-12-2025 (13:45:58)
rpicam-apps capabilites: egl:1 qt:1 drm:1 libav:1
libcamera build: v0.6.0+rpt20251202
pje0914@ParkJuEun:~/ssg_ssac_setup $ grep -nE \
  'camera_auto_detect|dtoverlay=.*imx708' \
  /boot/firmware/config.txt
2:camera_auto_detect=0
23:camera_auto_detect=1
pje0914@ParkJuEun:~/ssg_ssac_setup $ sudo dmesg -T | \
grep -iE 'imx708|camera|csi|i2c|pisp|unicam|rp1' | \
tail -n 150
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/i2c@80000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@128000
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/csi@110000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/csi@128000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@80000/imx219@10
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/i2c@80000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@128000
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/csi@110000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/csi@128000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@80000/imx219@10
[Thu Jul 16 16:33:07 2026] SCSI subsystem initialized
[Thu Jul 16 16:33:07 2026] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 247)
[Thu Jul 16 16:33:07 2026] Loading iSCSI transport class v2.0-870.
[Thu Jul 16 16:33:08 2026] rp1 0002:01:00.0: bar0 len 0x4000, start 0x1f00410000, end 0x1f00413fff, flags, 0x40200
[Thu Jul 16 16:33:08 2026] rp1 0002:01:00.0: bar1 len 0x400000, start 0x1f00000000, end 0x1f003fffff, flags, 0x40200
[Thu Jul 16 16:33:08 2026] rp1 0002:01:00.0: enabling device (0000 -> 0002)
[Thu Jul 16 16:33:08 2026] rp1 0002:01:00.0: chip_id 0x20001927
[Thu Jul 16 16:33:08 2026] /axi/pcie@1000120000/rp1/i2c@80000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@128000
[Thu Jul 16 16:33:08 2026] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[Thu Jul 16 16:33:08 2026] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[Thu Jul 16 16:33:08 2026] /axi/pcie@1000120000/rp1/csi@110000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[Thu Jul 16 16:33:08 2026] /axi/pcie@1000120000/rp1/i2c@80000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@128000
[Thu Jul 16 16:33:08 2026] /axi/pcie@1000120000/rp1/csi@128000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@80000/imx219@10
[Thu Jul 16 16:33:08 2026] genirq: irq_chip rp1_irq_chip did not update eff. affinity mask of irq 100
[Thu Jul 16 16:33:16 2026] i2c_dev: i2c /dev entries driver
[Thu Jul 16 16:33:19 2026] rp1-firmware rp1_firmware: RP1 Firmware version eb39cfd516f8c90628aa9d91f52370aade5d0a55
[Thu Jul 16 16:33:19 2026] /axi/pcie@1000120000/rp1/csi@128000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@80000/imx219@10
[Thu Jul 16 16:33:19 2026] /axi/pcie@1000120000/rp1/i2c@80000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@128000
[Thu Jul 16 16:33:19 2026] /axi/pcie@1000120000/rp1/csi@110000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[Thu Jul 16 16:33:19 2026] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[Thu Jul 16 16:33:19 2026] rp1-pio 1f00178000.pio: Created instance as pio0
[Thu Jul 16 16:33:19 2026] brcmstb-i2c 107d508200.i2c:  @97500hz registered in interrupt mode
[Thu Jul 16 16:33:19 2026] brcmstb-i2c 107d508280.i2c:  @97500hz registered in interrupt mode
[Thu Jul 16 16:33:20 2026] pispbe 1000880000.pisp_be: bcm2712_iommu_of_xlate: MMU 1000005100.iommu
[Thu Jul 16 16:33:20 2026] pispbe 1000880000.pisp_be: bcm2712_iommu_probe_device: MMU 1000005100.iommu
[Thu Jul 16 16:33:20 2026] pispbe 1000880000.pisp_be: bcm2712_iommu_device_group: MMU 1000005100.iommu
[Thu Jul 16 16:33:20 2026] pispbe 1000880000.pisp_be: Adding to iommu group 0
[Thu Jul 16 16:33:20 2026] pispbe 1000880000.pisp_be: bcm2712_iommu_attach_dev: MMU 1000005100.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: bcm2712_iommu_of_xlate: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: bcm2712_iommu_probe_device: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: bcm2712_iommu_device_group: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: Adding to iommu group 2
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: bcm2712_iommu_attach_dev: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: DW dphy Host HW v1.20
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: PiSP FE HW v0.1
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: found subdevice /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: bcm2712_iommu_of_xlate: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: bcm2712_iommu_probe_device: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: bcm2712_iommu_device_group: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: Adding to iommu group 2
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: bcm2712_iommu_attach_dev: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: DW dphy Host HW v1.20
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: PiSP FE HW v0.1
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: found subdevice /axi/pcie@1000120000/rp1/i2c@80000/imx219@10
[Thu Jul 16 16:33:21 2026] imx708 11-001a: camera module ID 0x0302
[Thu Jul 16 16:33:21 2026] imx708 11-001a: ctrl(id:0x9f0902,val:0x232aaf80) is not handled
[Thu Jul 16 16:33:21 2026] imx708 11-001a: ctrl(id:0x9e0902,val:0x2b20) is not handled
[Thu Jul 16 16:33:21 2026] imx708 10-001a: camera module ID 0x0302
[Thu Jul 16 16:33:21 2026] imx708 10-001a: ctrl(id:0x9f0902,val:0x232aaf80) is not handled
[Thu Jul 16 16:33:21 2026] imx708 10-001a: ctrl(id:0x9e0902,val:0x2b20) is not handled
pje0914@ParkJuEun:~/ssg_ssac_setup $ 
ls -l /dev/media* /dev/video* 2>/dev/null
crw-rw----+ 1 root video 510,  0 Jul 16 16:33 /dev/media0
crw-rw----+ 1 root video 510,  1 Jul 16 16:33 /dev/media1
crw-rw----+ 1 root video 510,  2 Jul 16 16:33 /dev/media2
crw-rw----+ 1 root video 510,  3 Jul 16 16:33 /dev/media3
crw-rw----+ 1 root video 510,  4 Jul 16 16:33 /dev/media4
crw-rw----+ 1 root video  81, 16 Jul 16 16:33 /dev/video19
crw-rw----+ 1 root video  81,  0 Jul 16 16:33 /dev/video20
crw-rw----+ 1 root video  81,  1 Jul 16 16:33 /dev/video21
crw-rw----+ 1 root video  81,  2 Jul 16 16:33 /dev/video22
crw-rw----+ 1 root video  81,  3 Jul 16 16:33 /dev/video23
crw-rw----+ 1 root video  81,  4 Jul 16 16:33 /dev/video24
crw-rw----+ 1 root video  81,  5 Jul 16 16:33 /dev/video25
crw-rw----+ 1 root video  81,  6 Jul 16 16:33 /dev/video26
crw-rw----+ 1 root video  81,  7 Jul 16 16:33 /dev/video27
crw-rw----+ 1 root video  81,  8 Jul 16 16:33 /dev/video28
crw-rw----+ 1 root video  81,  9 Jul 16 16:33 /dev/video29
crw-rw----+ 1 root video  81, 10 Jul 16 16:33 /dev/video30
crw-rw----+ 1 root video  81, 11 Jul 16 16:33 /dev/video31
crw-rw----+ 1 root video  81, 12 Jul 16 16:33 /dev/video32
crw-rw----+ 1 root video  81, 13 Jul 16 16:33 /dev/video33
crw-rw----+ 1 root video  81, 14 Jul 16 16:33 /dev/video34
crw-rw----+ 1 root video  81, 15 Jul 16 16:33 /dev/video35
pje0914@ParkJuEun:~/ssg_ssac_setup $ ^C
pje0914@ParkJuEun:~/ssg_ssac_setup $ 

// debug cam set before -> imx 219 set cam 00. 01
pje0914@ParkJuEun:~/ssg_ssac_setup $ rpicam-hello --version
rpicam-apps build: v1.11.0 18-12-2025 (13:45:58)
rpicam-apps capabilites: egl:1 qt:1 drm:1 libav:1
libcamera build: v0.6.0+rpt20251202
pje0914@ParkJuEun:~/ssg_ssac_setup $ grep -nE \
  'camera_auto_detect|dtoverlay=.*imx708' \
  /boot/firmware/config.txt
2:camera_auto_detect=0
23:camera_auto_detect=1
pje0914@ParkJuEun:~/ssg_ssac_setup $ sudo dmesg -T | \
grep -iE 'imx708|camera|csi|i2c|pisp|unicam|rp1' | \
tail -n 150
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/i2c@80000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@128000
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/csi@110000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/csi@128000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@80000/imx219@10
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/i2c@80000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@128000
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/csi@110000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[Thu Jul 16 16:33:07 2026] /axi/pcie@1000120000/rp1/csi@128000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@80000/imx219@10
[Thu Jul 16 16:33:07 2026] SCSI subsystem initialized
[Thu Jul 16 16:33:07 2026] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 247)
[Thu Jul 16 16:33:07 2026] Loading iSCSI transport class v2.0-870.
[Thu Jul 16 16:33:08 2026] rp1 0002:01:00.0: bar0 len 0x4000, start 0x1f00410000, end 0x1f00413fff, flags, 0x40200
[Thu Jul 16 16:33:08 2026] rp1 0002:01:00.0: bar1 len 0x400000, start 0x1f00000000, end 0x1f003fffff, flags, 0x40200
[Thu Jul 16 16:33:08 2026] rp1 0002:01:00.0: enabling device (0000 -> 0002)
[Thu Jul 16 16:33:08 2026] rp1 0002:01:00.0: chip_id 0x20001927
[Thu Jul 16 16:33:08 2026] /axi/pcie@1000120000/rp1/i2c@80000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@128000
[Thu Jul 16 16:33:08 2026] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[Thu Jul 16 16:33:08 2026] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[Thu Jul 16 16:33:08 2026] /axi/pcie@1000120000/rp1/csi@110000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[Thu Jul 16 16:33:08 2026] /axi/pcie@1000120000/rp1/i2c@80000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@128000
[Thu Jul 16 16:33:08 2026] /axi/pcie@1000120000/rp1/csi@128000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@80000/imx219@10
[Thu Jul 16 16:33:08 2026] genirq: irq_chip rp1_irq_chip did not update eff. affinity mask of irq 100
[Thu Jul 16 16:33:16 2026] i2c_dev: i2c /dev entries driver
[Thu Jul 16 16:33:19 2026] rp1-firmware rp1_firmware: RP1 Firmware version eb39cfd516f8c90628aa9d91f52370aade5d0a55
[Thu Jul 16 16:33:19 2026] /axi/pcie@1000120000/rp1/csi@128000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@80000/imx219@10
[Thu Jul 16 16:33:19 2026] /axi/pcie@1000120000/rp1/i2c@80000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@128000
[Thu Jul 16 16:33:19 2026] /axi/pcie@1000120000/rp1/csi@110000: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[Thu Jul 16 16:33:19 2026] /axi/pcie@1000120000/rp1/i2c@88000/imx219@10: Fixed dependency cycle(s) with /axi/pcie@1000120000/rp1/csi@110000
[Thu Jul 16 16:33:19 2026] rp1-pio 1f00178000.pio: Created instance as pio0
[Thu Jul 16 16:33:19 2026] brcmstb-i2c 107d508200.i2c:  @97500hz registered in interrupt mode
[Thu Jul 16 16:33:19 2026] brcmstb-i2c 107d508280.i2c:  @97500hz registered in interrupt mode
[Thu Jul 16 16:33:20 2026] pispbe 1000880000.pisp_be: bcm2712_iommu_of_xlate: MMU 1000005100.iommu
[Thu Jul 16 16:33:20 2026] pispbe 1000880000.pisp_be: bcm2712_iommu_probe_device: MMU 1000005100.iommu
[Thu Jul 16 16:33:20 2026] pispbe 1000880000.pisp_be: bcm2712_iommu_device_group: MMU 1000005100.iommu
[Thu Jul 16 16:33:20 2026] pispbe 1000880000.pisp_be: Adding to iommu group 0
[Thu Jul 16 16:33:20 2026] pispbe 1000880000.pisp_be: bcm2712_iommu_attach_dev: MMU 1000005100.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: bcm2712_iommu_of_xlate: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: bcm2712_iommu_probe_device: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: bcm2712_iommu_device_group: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: Adding to iommu group 2
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: bcm2712_iommu_attach_dev: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: DW dphy Host HW v1.20
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: PiSP FE HW v0.1
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00110000.csi: found subdevice /axi/pcie@1000120000/rp1/i2c@88000/imx219@10
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: bcm2712_iommu_of_xlate: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: bcm2712_iommu_probe_device: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: bcm2712_iommu_device_group: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: Adding to iommu group 2
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: bcm2712_iommu_attach_dev: MMU 1000005280.iommu
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: DW dphy Host HW v1.20
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: PiSP FE HW v0.1
[Thu Jul 16 16:33:20 2026] rp1-cfe 1f00128000.csi: found subdevice /axi/pcie@1000120000/rp1/i2c@80000/imx219@10
[Thu Jul 16 16:33:21 2026] imx708 11-001a: camera module ID 0x0302
[Thu Jul 16 16:33:21 2026] imx708 11-001a: ctrl(id:0x9f0902,val:0x232aaf80) is not handled
[Thu Jul 16 16:33:21 2026] imx708 11-001a: ctrl(id:0x9e0902,val:0x2b20) is not handled
[Thu Jul 16 16:33:21 2026] imx708 10-001a: camera module ID 0x0302
[Thu Jul 16 16:33:21 2026] imx708 10-001a: ctrl(id:0x9f0902,val:0x232aaf80) is not handled
[Thu Jul 16 16:33:21 2026] imx708 10-001a: ctrl(id:0x9e0902,val:0x2b20) is not handled
pje0914@ParkJuEun:~/ssg_ssac_setup $ 
ls -l /dev/media* /dev/video* 2>/dev/null
crw-rw----+ 1 root video 510,  0 Jul 16 16:33 /dev/media0
crw-rw----+ 1 root video 510,  1 Jul 16 16:33 /dev/media1
crw-rw----+ 1 root video 510,  2 Jul 16 16:33 /dev/media2
crw-rw----+ 1 root video 510,  3 Jul 16 16:33 /dev/media3
crw-rw----+ 1 root video 510,  4 Jul 16 16:33 /dev/media4
crw-rw----+ 1 root video  81, 16 Jul 16 16:33 /dev/video19
crw-rw----+ 1 root video  81,  0 Jul 16 16:33 /dev/video20
crw-rw----+ 1 root video  81,  1 Jul 16 16:33 /dev/video21
crw-rw----+ 1 root video  81,  2 Jul 16 16:33 /dev/video22
crw-rw----+ 1 root video  81,  3 Jul 16 16:33 /dev/video23
crw-rw----+ 1 root video  81,  4 Jul 16 16:33 /dev/video24
crw-rw----+ 1 root video  81,  5 Jul 16 16:33 /dev/video25
crw-rw----+ 1 root video  81,  6 Jul 16 16:33 /dev/video26
crw-rw----+ 1 root video  81,  7 Jul 16 16:33 /dev/video27
crw-rw----+ 1 root video  81,  8 Jul 16 16:33 /dev/video28
crw-rw----+ 1 root video  81,  9 Jul 16 16:33 /dev/video29
crw-rw----+ 1 root video  81, 10 Jul 16 16:33 /dev/video30
crw-rw----+ 1 root video  81, 11 Jul 16 16:33 /dev/video31
crw-rw----+ 1 root video  81, 12 Jul 16 16:33 /dev/video32
crw-rw----+ 1 root video  81, 13 Jul 16 16:33 /dev/video33
crw-rw----+ 1 root video  81, 14 Jul 16 16:33 /dev/video34
crw-rw----+ 1 root video  81, 15 Jul 16 16:33 /dev/video35
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
pje0914@ParkJuEun:~/ssg_ssac_setup $ 
sudo cp -a \
  /boot/firmware/config.txt \
  /boot/firmware/config.txt.bak.$(date +%Y%m%d-%H%M%S)
pje0914@ParkJuEun:~/ssg_ssac_setup $   ls -lh /boot/firmware/config.txt*
-rwxr-xr-x 1 root root 1.5K Jan 29 15:16 /boot/firmware/config.txt
-rwxr-xr-x 1 root root 1.5K Jan 29 15:16 /boot/firmware/config.txt.bak.20260716-165832
pje0914@ParkJuEun:~/ssg_ssac_setup $ 



