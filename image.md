useful command lines for image modification
===========================================

* remove all GPS metadata from JPEG:

  ```
  exiftool -gps:all= -xmp:geotag= image.jpg
  ```
  
  *Note that this only removes GPS metadata from EXIF and XMP.
  GPS metadata may be present in other metadata containers inside the file!*
  
