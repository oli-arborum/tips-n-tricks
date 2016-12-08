useful document command lines (e.g. ps, pdf, LaTeX, ...)
========================================================

 * convert ps to pdf, force A4 paper format:
 
   ```
   ps2pdf -sPAPERSIZE=a4 input.ps
   ```

 * separate an A4 landscape page PDF containing two A5 portait pages side by side into a 2-page PDF:
 
   ```
   gs -o 1.pdf -sDEVICE=pdfwrite -g4210x5950 -c "<</PageOffset [0 0]>> setpagedevice" -f input.pdf
   gs -o 2.pdf -sDEVICE=pdfwrite -g4210x5950 -c "<</PageOffset [-421 0]>> setpagedevice" -f input.pdf
   pdftk A=1.pdf B=2.pdf shuffle A B output output.pdf verbose
   ```
   or alternatively
   ```
   mutool poster -x 2 input.pdf output.pdf
   ```
   
