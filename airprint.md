AirPrint Server on Ubuntu Linux with CUPS and AVAHI daemon
==========================================================

(based on http://linuxwin.com/cups-airprint-on-raspberry-pi/)

Prerequisites
-------------
You have a running CUPS installation and are able to print locally.

I tried these instructions on a Ubuntu 18.04 LTS machine with an ancient HP Color LaserJet CP1215.
If you are using a different distribution you may need to adapt the commands.

Install packages
----------------
    apt install cups-pdf python-cups python-lxml

You need python-cups and python-lxml for the airprint-generate.py script.

Make CUPS server available from network
---------------------------------------
We do not expose the CUPS admin pages to the network, but only make the CUPS server itself
listen on requests not only on localhost.

Modify `/etc/cups/cupsd.conf` (diff shown):

    16c16,17
    < Listen localhost:631
    ---
    > ## commented out for AirPrint support
    > #Listen localhost:631
    17a19,20
    > ## needed for AirPrint support
    > Port 631
    31a35,36
    >   ## needed for AirPrint support:
    >   Allow @local

Generate AVAHI Service file for shared printer
----------------------------------------------
Get the airprint-generate Python script from https://github.com/tjfontaine/airprint-generate:

     wget https://raw.github.com/tjfontaine/airprint-generate/master/airprint-generate.py

Generate Service file for your printer:

     python airprint-generate.py

It creates a file for each printer in the current directory.

In case you have a color printer, add the following directive to the generated respective file:

     <txt-record>Color=T</txt-record>

This makes the preview on the iDevice displayed in color, not grey-scaled.

Now copy all created AHAVI Service files to `/etc/avahi/services`. (In case you have only one printer it is just one file.)

    sudo cp AirPrint*.service /etc/avahi/services/

Add some MIME types to CUPS configuration
-----------------------------------------

    sudo su
    echo "image/urf application/vnd.cups-postscript 66 pdftops" > /usr/share/cups/mime/local.convs
    echo "image/urf urf (0,UNIRAST)" > /usr/share/cups/mime/apple.types
    echo "image/urf application/pdf 100 pdftoraster" > /usr/share/cups/mime/apple.convs

Restart services
----------------

    sudo service cups restart
    sudo service avahi-daemon restart
    
Now the printer(s) should be announced via AVAHI (Bonjour) and appear on you iDevice when opening the print dialog.

For debugging you can use the GUI tool *avahi-discover* that shows all AVAHI announcements in the network
(installable with `apt install avahi-discover`).
