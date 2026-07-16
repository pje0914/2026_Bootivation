// step1: raspberry pi check board
mkdir -p ~/ssg_ssac_setup
cd ~/ssg_ssac_setup

{
  echo "===== OS ====="
  cat /etc/os-release

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

// step2: cam0, cam1 tx/rx check
rpicam-hello --list-cameras | tee cameras.txt
libcamera-hello --list-cameras

// step3: cam picture each other
cd ~/ssg_ssac_setup

rpicam-jpeg \
  --camera 0 \
  --nopreview \
  --timeout 3000 \
  --width 1280 \
  --height 720 \
  --autofocus-mode continuous \
  --output cam0.jpg

rpicam-jpeg \
  --camera 1 \
  --nopreview \
  --timeout 3000 \
  --width 1280 \
  --height 720 \
  --autofocus-mode continuous \
  --output cam1.jpg

  ls -lh cam0.jpg cam1.jpg


  step4: cam0, cam1 check
  rpicam-jpeg \
  --camera 0 \
  --nopreview \
  --timeout 1500 \
  --width 1280 \
  --height 720 \
  --output map_cam0.jpg
