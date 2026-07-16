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
