mkdir -p ~/Bootivation/rpi_tray ~/Bootivation/camera_test

cat > ~/Bootivation/rpi_tray/dual_live_position.py <<'PY'
from __future__ import annotations

import time
from datetime import datetime
from pathlib import Path

import cv2
import numpy as np
from picamera2 import Picamera2


WIDTH = 640
HEIGHT = 480
FPS = 30

SAVE_DIR = Path.home() / "Bootivation" / "camera_test"
SAVE_DIR.mkdir(parents=True, exist_ok=True)


def draw_guide(frame: np.ndarray, title: str, show_grid: bool) -> np.ndarray:
    image = frame.copy()
    h, w = image.shape[:2]

    cv2.putText(
        image,
        title,
        (15, 30),
        cv2.FONT_HERSHEY_SIMPLEX,
        0.8,
        (0, 255, 255),
        2,
        cv2.LINE_AA,
    )

    if not show_grid:
        return image

    # 상품이 화면 가장자리에 붙지 않도록 7% 여백
    margin_x = int(w * 0.07)
    margin_y = int(h * 0.09)

    left = margin_x
    right = w - margin_x
    top = margin_y
    bottom = h - margin_y

    # 전체 안전 영역
    cv2.rectangle(
        image,
        (left, top),
        (right, bottom),
        (0, 255, 0),
        2,
    )

    # A/B/C 3개 구역
    for column in range(1, 3):
        x = left + ((right - left) * column // 3)
        cv2.line(
            image,
            (x, top),
            (x, bottom),
            (255, 255, 0),
            2,
        )

    # 구역별 상품 5개 배치 기준
    for row in range(1, 5):
        y = top + ((bottom - top) * row // 5)
        cv2.line(
            image,
            (left, y),
            (right, y),
            (255, 255, 0),
            1,
        )

    zone_width = (right - left) // 3

    for index, name in enumerate(("A", "B", "C")):
        x = left + zone_width * index + zone_width // 2 - 10
        cv2.putText(
            image,
            name,
            (x, top + 25),
            cv2.FONT_HERSHEY_SIMPLEX,
            0.8,
            (0, 255, 255),
            2,
            cv2.LINE_AA,
        )

    # 화면 중심 확인용 십자선
    center_x = w // 2
    center_y = h // 2

    cv2.line(
        image,
        (center_x - 15, center_y),
        (center_x + 15, center_y),
        (0, 0, 255),
        2,
    )
    cv2.line(
        image,
        (center_x, center_y - 15),
        (center_x, center_y + 15),
        (0, 0, 255),
        2,
    )

    return image


def configure_camera(index: int) -> Picamera2:
    camera = Picamera2(index)

    config = camera.create_video_configuration(
        main={
            "size": (WIDTH, HEIGHT),
            "format": "RGB888",
        },
        controls={
            "FrameRate": FPS,
        },
        buffer_count=4,
    )

    camera.configure(config)
    return camera


def main() -> None:
    cam_before = configure_camera(0)
    cam_after = configure_camera(1)

    show_grid = True
    last_time = time.perf_counter()
    displayed_fps = 0.0

    try:
        cam_before.start()
        cam_after.start()

        # 자동 노출·화이트밸런스 안정화
        time.sleep(2.0)

        cv2.namedWindow("Bootivation Dual Camera", cv2.WINDOW_NORMAL)
        cv2.resizeWindow("Bootivation Dual Camera", 1280, 520)

        print("camera 0 = BEFORE")
        print("camera 1 = AFTER")
        print("Q/ESC : 종료")
        print("G     : 가이드 표시 전환")
        print("S     : 현재 화면 저장")

        while True:
            before_rgb = cam_before.capture_array()
            after_rgb = cam_after.capture_array()

            before = cv2.cvtColor(before_rgb, cv2.COLOR_RGB2BGR)
            after = cv2.cvtColor(after_rgb, cv2.COLOR_RGB2BGR)

            before_display = draw_guide(
                before,
                "CAM 0 - BEFORE",
                show_grid,
            )
            after_display = draw_guide(
                after,
                "CAM 1 - AFTER",
                show_grid,
            )

            now = time.perf_counter()
            elapsed = now - last_time

            if elapsed > 0:
                current_fps = 1.0 / elapsed
                displayed_fps = displayed_fps * 0.9 + current_fps * 0.1

            last_time = now

            combined = np.hstack((before_display, after_display))

            cv2.putText(
                combined,
                f"FPS {displayed_fps:.1f} | G:grid  S:save  Q:quit",
                (15, combined.shape[0] - 15),
                cv2.FONT_HERSHEY_SIMPLEX,
                0.6,
                (255, 255, 255),
                2,
                cv2.LINE_AA,
            )

            cv2.imshow("Bootivation Dual Camera", combined)

            key = cv2.waitKey(1) & 0xFF

            if key in (ord("q"), 27):
                break

            if key == ord("g"):
                show_grid = not show_grid

            if key == ord("s"):
                timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")

                before_path = SAVE_DIR / f"position_{timestamp}_before.jpg"
                after_path = SAVE_DIR / f"position_{timestamp}_after.jpg"
                combined_path = SAVE_DIR / f"position_{timestamp}_combined.jpg"

                cv2.imwrite(str(before_path), before)
                cv2.imwrite(str(after_path), after)
                cv2.imwrite(str(combined_path), combined)

                print(f"[SAVED] {before_path}")
                print(f"[SAVED] {after_path}")
                print(f"[SAVED] {combined_path}")

    finally:
        try:
            cam_before.stop()
        except Exception:
            pass

        try:
            cam_after.stop()
        except Exception:
            pass

        cam_before.close()
        cam_after.close()
        cv2.destroyAllWindows()


if __name__ == "__main__":
    main()
PY

python3 ~/Bootivation/rpi_tray/dual_live_position.py
