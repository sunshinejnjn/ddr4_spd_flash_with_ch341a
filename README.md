# ddr4_spd_flash_with_ch341a
have a $2 ch341a and wanna flash/backup ddr4 spd with it? you can take a look at this.

what you have to do:
1. take a look at if your dimm/sodimm can be flashed.
2. connect your ddr4 to ch341a
3. read and backup each spd page (low 256 bytes and/or high 256 bytes)
4. modify it with any hex editor or replace some part (like the timming settings) with the program
5. recalculate crc with the program.
6. make sure your ram stick is at the right page
7. flash certain page back to spd
8. try the ram in system.

details:
1. take a look at if your dimm/sodimm can be flashed. you can use thaipoon freeware edition's write test function to rule out some situations. if thaipoon reports "OK". then everything is fine. if thaipoon reports something's wrong with bios write protection, you may still be able to flash it but we can't be certain until we tested it with our programmer (ch341a).

2. you'll need a few pins to read and write to the eeprom chip. they are scl, sda, sa0, vss and vcc.
you'll be able to find the pins if you have a datasheet of any dimm/sodimm. for how to connect them to your ch341a, you have a few choices:
a. for dimm, buy a socket for spd flashing. for so-dimm, you will find those so-dimm to dimm converters (make sure you are buying the ddr4 version) very handful. you can have a socket or a converter for very little price as low as $3. you can then solder the pins from the socket or the auxilary off board spd chip on the convertor to connect them to ch341a.
b. if you have a uncotted dimm, you'll find those over cross wholes very hadful to connect a copper wire to without soldering. connect them with this method has been n work correctly
c. you may be able to unsolder the spd eeprom chip or connect its pins to ch341a directly.

3. use AsProgrammer. proceed as follows:
a. set device to ch341a, select chip 24c02 to read the first page. back it up!
b. set address bits to 01101100, and press "read" again;
c. set the address back to 0110000, and "read" again for the 2nd page
d. set address bits to 0110111, and press "read" again for the second page;
e. set address bits to 1010000, and press "read" again for the second page, back it up!
f. set address bits to 1010110, and press "read" again to set the eeprom bakc to its first page;

4. any hex editor can do the job. 
use an hex editor on the dumped file
run the program update_crc and lod the file

5. you can always use the buildin function replace(hex_string, FILEID), it will update the crc.l

6. "read" the ic to check if you ram is at the right page. 
set address bits to 0110111, and press "read" again for the second page;
if you need to write to the other page, set address bits to 1010000, and press "read" again for the second page

7. select modified file (for the certain page), and click write. you'll see changes are made after "write"

8. Enjoy. if anything goes wrong, you can always flash back the old backup.


