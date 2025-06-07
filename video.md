useful video conversion command lines
=====================================

* convert video e.g. from MTS container to MP4 copying video stream and re-encoding (AC3) audio stream to AAC:
  ```
  ffmpeg -i input.MTS -c:v copy -c:a aac_at -b:a 128k output.mp4
  ```
  ("aac_at" uses according to https://trac.ffmpeg.org/wiki/Encode/AAC FFMPEG's highest-quality AAC
  encoder and only available on macOS, otherwise use "libfdk_aac" or just "aac")
