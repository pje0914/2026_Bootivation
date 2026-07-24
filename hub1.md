sed -i \
  -e 's/before = cv2.cvtColor(before_rgb, cv2.COLOR_RGB2BGR)/before = before_rgb/' \
  -e 's/after = cv2.cvtColor(after_rgb, cv2.COLOR_RGB2BGR)/after = after_rgb/' \
  ~/Bootivation/rpi_tray/dual_tray_position.py

  python3 ~/Bootivation/rpi_tray/dual_tray_position.py --layout 2x2
