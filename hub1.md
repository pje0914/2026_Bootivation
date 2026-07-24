mkdir -p ~/Bootivation/camera_test

rpicam-vid --camera 0 --nopreview -t 5000 --width 640 --height 480 \
  --framerate 30 -o ~/Bootivation/camera_test/before.h264 &

rpicam-vid --camera 1 --nopreview -t 5000 --width 640 --height 480 \
  --framerate 30 -o ~/Bootivation/camera_test/after.h264 &

wait
