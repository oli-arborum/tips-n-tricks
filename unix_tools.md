useful GNU/UNIX tools command lines
===================================

 * find newest file in current directory and all subdirectories
 
   ```
   find . -type f -printf '%T@ %p\n'| sort -n | tail -1 | cut -f2--d" "
   ```

 * extract everything from line $FROM to line $TO from a text file

   ```
   awk "NR>=${FROM} && NR<=${TO}" < input_file.txt
   ```
