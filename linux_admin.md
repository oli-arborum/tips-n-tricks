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

 * Docker clean-up:

   ```
   # Remove exited containers
   /usr/bin/docker ps -a -q -f status=exited | xargs --no-run-if-empty docker rm -v
   
   # Remove dangling images
   /usr/bin/docker images -f "dangling=true" -q | xargs --no-run-if-empty docker rmi
   
   # Remove unused images
   /usr/bin/docker images | awk '/ago/  { print $3}' | xargs --no-run-if-empty docker rmi
   
   # Remove dangling volumes
   /usr/bin/docker volume ls -qf dangling=true | xargs --no-run-if-empty docker volume rm
   ```
