useful audio command lines
==========================

* Copy two mono WAV into one stereo WAV:

  ```
  CopyAudio left.wav right.wav -S "FL FR" stereo.wav
  ```
  
* extract raw audio from AV container (e.g. flv, works also for AVI, MP4, M4V, ...):

  ```
  ffmpeg -i input.flv -vn -acodec copy output.mp3
  ```
  (Note that we assume here that the audio format in the container *is* MP3!)
  
* identify audio codec in AV container:

  ```
  mplayer -frames 0 -identify input.flv 2>/dev/null | awk -F= '/ID_AUDIO_CODEC/ {print $2}'
  ```

* convert 24 bit (or whatever) WAV into 16 bit WAV:

  ```
  sox input.wav -b 16 output.wav rate -v
  ```
