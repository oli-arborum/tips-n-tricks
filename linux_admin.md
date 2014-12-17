useful GNU/Linux command lines for system administration
========================================================

 * save partition table to file
 
   ```
   sudo sfdisk -d /dev/sda > sda.mpt
   ```
   
 * restore partition table from file (dangerous!)
 
   ```
   sudo sfdisk /dev/sda < sda.mpt
   ```

 * save MBR to file:

   ```
   sudo dd if=/dev/sda of=sda.mbr bs=446 count=1 
   ```
