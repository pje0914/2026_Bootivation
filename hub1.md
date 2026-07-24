mkdir -p ~/Bootivation/camera_test

rpicam-vid --camera 0 --nopreview -t 5000 --width 640 --height 480 \
  --framerate 30 -o ~/Bootivation/camera_test/before.h264 &

rpicam-vid --camera 1 --nopreview -t 5000 --width 640 --height 480 \
  --framerate 30 -o ~/Bootivation/camera_test/after.h264 &

wait

ls -lh ~/Bootivation/camera_test


tivation/camera_test/after.h264
parkjueun@pje030914:~ $ 
ls -lh ~/Bootivation/camera_test
합계 1.7M
-rw-rw-r-- 1 parkjueun parkjueun 800K  7월 24일  12:06 after.h264
-rw-rw-r-- 1 parkjueun parkjueun 866K  7월 24일  12:06 before.h264
parkjueun@pje030914:~ $ ^C
parkjueun@pje030914:~ $ 
