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
