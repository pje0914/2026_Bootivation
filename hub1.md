sudo apt update
sudo apt install -y espeak-ng

mkdir -p ~/Bootivation/rpi_tray/audio/core
mkdir -p ~/Bootivation/rpi_tray/audio/error

cat > ~/Bootivation/rpi_tray/build_wavs.sh <<'SH'
#!/usr/bin/env bash
set -euo pipefail

ROOT="$HOME/Bootivation/rpi_tray/audio"
CORE="$ROOT/core"
ERROR="$ROOT/error"

mkdir -p "$CORE" "$ERROR"

make_wav() {
    local output="$1"
    local text="$2"

    espeak-ng \
        -v ko \
        -s 145 \
        -p 45 \
        -a 170 \
        -w "$output" \
        "$text"

    echo "[CREATED] $output"
}

make_wav "$CORE/system_ready.wav" \
    "계산 트레이가 준비되었습니다."

make_wav "$CORE/place_before.wav" \
    "상품을 계산 전 트레이에 올려 주세요."

make_wav "$CORE/before_detected.wav" \
    "상품 인식이 완료되었습니다."

make_wav "$CORE/move_after.wav" \
    "결제가 확인되었습니다. 상품을 계산 후 트레이로 이동해 주세요."

make_wav "$CORE/tray_complete.wav" \
    "상품 확인이 완료되었습니다."

make_wav "$CORE/tray_mismatch.wav" \
    "상품 수량이 일치하지 않습니다. 다시 확인해 주세요."

make_wav "$CORE/unknown_product.wav" \
    "인식되지 않은 상품이 있습니다."

make_wav "$CORE/system_reset.wav" \
    "계산 트레이를 초기화합니다."

make_wav "$ERROR/camera_error.wav" \
    "카메라 연결 상태를 확인해 주세요."

make_wav "$ERROR/network_error.wav" \
    "통신 연결 상태를 확인해 주세요."

echo
echo "WAV 생성 완료"
SH


chmod +x ~/Bootivation/rpi_tray/build_wavs.sh
~/Bootivation/rpi_tray/build_wavs.sh


find ~/Bootivation/rpi_tray/audio -type f -name "*.wav" | sort


