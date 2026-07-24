cat > ~/Bootivation/rpi_tray/test_wavs.sh <<'SH'
#!/usr/bin/env bash
set -euo pipefail

ROOT="$HOME/Bootivation/rpi_tray/audio"

find "$ROOT" -type f -name "*.wav" | sort | while read -r file
do
    echo "[PLAY] $file"
    pw-play "$file"
    sleep 0.5
done
SH

chmod +x ~/Bootivation/rpi_tray/test_wavs.sh
~/Bootivation/rpi_tray/test_wavs.sh



-------------------------------------------------------
cat > ~/Bootivation/rpi_tray/audio/audio_manifest.json <<'JSON'
{
  "SYSTEM_READY": "core/system_ready.wav",
  "PLACE_BEFORE": "core/place_before.wav",
  "BEFORE_DETECTED": "core/before_detected.wav",
  "MOVE_AFTER": "core/move_after.wav",
  "TRAY_COMPLETE": "core/tray_complete.wav",
  "TRAY_MISMATCH": "core/tray_mismatch.wav",
  "UNKNOWN_PRODUCT": "core/unknown_product.wav",
  "SYSTEM_RESET": "core/system_reset.wav",
  "CAMERA_ERROR": "error/camera_error.wav",
  "NETWORK_ERROR": "error/network_error.wav"
}
JSON


------------------------------------------------

play_audio("MOVE_AFTER")
play_audio("TRAY_COMPLETE")

