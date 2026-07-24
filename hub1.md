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


sudo apt install -y python3-picamera2 python3-opencv python3-numpy python3-zmq

mkdir -p ~/Bootivation/rpi_tray ~/Bootivation/camera_test

cat > ~/Bootivation/rpi_tray/dual_camera_smoke.py <<'PY'
from pathlib import Path
import time

import cv2
from picamera2 import Picamera2


OUT_DIR = Path.home() / "Bootivation" / "camera_test"
OUT_DIR.mkdir(parents=True, exist_ok=True)

cam_before = Picamera2(0)  # 계산 전
cam_after = Picamera2(1)   # 계산 후

cameras = [cam_before, cam_after]

try:
    for camera in cameras:
        config = camera.create_video_configuration(
            main={"size": (640, 480), "format": "RGB888"},
            controls={"FrameRate": 30},
            buffer_count=4,
        )
        camera.configure(config)

    cam_before.start()
    cam_after.start()
    time.sleep(2)

    before_frame = cam_before.capture_array()
    after_frame = cam_after.capture_array()

    before_path = OUT_DIR / "python_before.jpg"
    after_path = OUT_DIR / "python_after.jpg"

    before_ok = cv2.imwrite(str(before_path), before_frame)
    after_ok = cv2.imwrite(str(after_path), after_frame)

    print(f"BEFORE camera=0 shape={before_frame.shape} saved={before_ok}")
    print(f"AFTER  camera=1 shape={after_frame.shape} saved={after_ok}")
    print(f"output: {OUT_DIR}")

    if not before_ok or not after_ok:
        raise RuntimeError("이미지 저장에 실패했습니다.")

finally:
    for camera in cameras:
        try:
            camera.stop()
        except Exception:
            pass
        camera.close()
PY

python3 ~/Bootivation/rpi_tray/dual_camera_smoke.py


ls -lh ~/Bootivation/camera_test/python_*.jpg

parkjueun@pje030914:~ $ 
ls -lh ~/Bootivation/camera_test/python_*.jpg
-rw-rw-r-- 1 parkjueun parkjueun 35K  7월 24일  12:11 /home/parkjueun/Bootivation/camera_test/python_after.jpg
-rw-rw-r-- 1 parkjueun parkjueun 37K  7월 24일  12:11 /home/parkjueun/Bootivation/camera_test/python_before.jpg
parkjueun@pje030914:~ $ 


