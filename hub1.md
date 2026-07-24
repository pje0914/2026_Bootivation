mkdir -p ~/Bootivation/camera_check

rpicam-jpeg --camera 0 --timeout 1500 --width 640 --height 480 \
  --output ~/Bootivation/camera_check/cam0.jpg

  rpicam-jpeg --camera 1 --timeout 1500 --width 640 --height 480 \
  --output ~/Bootivation/camera_check/cam1.jpg
