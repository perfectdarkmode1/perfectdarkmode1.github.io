Consoling in on Linux
Plug console cable in

find out what your serial line name is:

$ dmesg | grep -i FTDI

Open putty > change to serial > change the tty line name

Ex: /dev/ttyUSB0

Make sure your serial settings are correct

Press open > when terminal appears press enter