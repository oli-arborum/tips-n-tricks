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
