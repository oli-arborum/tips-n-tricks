useful GNU/UNIX tools command lines
===================================

 * find newest file in current directory and all subdirectories
 
   ```
   find . -type f -printf '%T@ %p\n'| sort -n | tail -1| cut -f2--d" "
   ```
