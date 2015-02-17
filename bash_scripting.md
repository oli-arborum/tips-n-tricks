useful commands and command sequences for bash scripting
========================================================

 * execute a command for every line of an input file:
 
   ```
   exec < $FILE
   while read LINE
   do
     do_something_with $LINE
   done
   ```
   
   alternatively:

   ```
   while read -r LINE
   do
     do_something_with $LINE
   done < $FILE
   ```

 * get the directory where the script is stored in:
 
   ```
   DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"
   ```
   
   or more completely (taking into account symlinks):
   
   ```
    SOURCE="${BASH_SOURCE[0]}"
    while [ -h "$SOURCE" ]; do # resolve $SOURCE until the file is no longer a symlink
      DIR="$( cd -P "$( dirname "$SOURCE" )" && pwd )"
      SOURCE="$(readlink "$SOURCE")"
      [[ $SOURCE != /* ]] && SOURCE="$DIR/$SOURCE" # if $SOURCE was a relative symlink, we need to resolve it relative to the path where the symlink file was located
    done
    DIR="$( cd -P "$( dirname "$SOURCE" )" && pwd )"
   ```
   
   credits: http://stackoverflow.com/questions/59895/can-a-bash-script-tell-what-directory-its-stored-in
   
 * extract everything from $VAR after last ".": `${VAR##*.}`

 * extract everything from $VAR before first ":": `${VAR%%:*}`
 
 * extract everything from $VAR after first ":": `${VAR#*:}`
 
 * remove every occurance of "-" from $VAR: `$VAR=${VAR//-/}`
 
 * apply regular expression on $VAR and access 1st ()-group:
 
   ```
   [[ $VAR =~ ([0-9]{4}-[0-9]{2}-[0-9]{2}) ]]
   $DATE=${BASH_REMATCH}[1]
   ```

 * do date calculations (e.g. one day later, assuming $DATE is in a format understandable by `date` command):
 
   ```
   ONE_DAY_LATER=$((`date -d $DATE +%s` + 24*60*60))
   ONE_DAY_LATER=$(date -d @$ONE_DAY_LATER +%Y-%m-%d)
   ```

  (or much simpler:)
   ```
   ONE_DAY_LATER=$(date -d "+1 day" +%Y-%m-%d)
   ```
