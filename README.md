gqrx-scan
================

Control GRQX to scan frequencies or from channels using a CSV file.

Scan mode operations:

 * --start 28400000                Start at frequency 28.400
 * --end 28410000                  Stop at frequency 28.410
 * --mode USB                      Scan in USB demodulation

File mode options:

  * --channels 19,20,30             Scan channels 19, 20, and 30
  * --channels 19-30                Scan channels 19 through 30
  * --pattern "FRS|GMR|^145"        Scan channels named FRS or GMR or frequencies starting with 145
  * --showall                       Show all channels even if skipped
  * --dumpchannels                  Show all channels, do not tune any

General scan or file options:

  * --pause 2                       Wait 2 seconds between frequencies/channels
  * --step 250                      Step by 250mhz in frequency scanning mode
  * --exclude 28.401e6,28.410e6     Exclude frequency 28 401 and 28 410

Signal detection options:

  * --delaylevel=-30                Delay scanning if a signal of -30 or better is heard
  * --delaytime 10                  Delay scanning for 10s when a signal is detected
  * --record                        Record when signal is detected
  * --stop                          Stop scanning until the enter key is hit
  * --wait                          Stop scanning until the channel is clear
  * --levelstop=0                   Do not pause to listen for signal

Bookmarks file

The CSV file that can be used for scanning pre-set channels is the same format
as the gqrx-remote project (https://github.com/marmelo/gqrx-remote) uses, without
any headers, with the columns being HZ,MODE,Name

The CSV file path is defined in the file and should be updated for where your
file is located.

Example:

28101000,CW,10m CW<br>
28400000,USB,10m Calling<br>
446000000,FM,440 Simplex<br>
144200000,LSB,2m SSB Calling<br>

There are other options in the file which can be modified to set them as defaults
but almost all can be specified on the command line.

Example usage scenarios..

  * Scan entire CSV file with a pause of 2s between channels
    * gqrx-scan --type file --pause 2

  * Scan lines 40 through 60 in the file
    * gqrx-scan --type file --channels 40-60

  * Scan lines 19, 20, and 30 in the file, recording when a signal is detected
    * gqrx-scan --type file --channels 19,20,30 --record

  * Scan FRS, GMRS, and all 145, 146, and 147 frequency channels
    * gqrx-scan --type file --pattern "FRS|GMR|14[5|6|7]"

  * Scan 28.400 to 28.410 in CW mode, pausing for a signal level of -30 for 10s
   * gqrx-scan --type scan --start 28400000 --end 28410000 --mode CW --delaylevel=-30 --delaytime 10
   * Available modes: AM FM WFM WFM_ST LSB USB CW CWL CWU

Dependencies:

GQRX 2.3 or greater with Remote Control enabled

Perl modules:
  * Net::Telnet
  * Time::HiRes
  * Getopt::Long



[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/khaytsus/gqrx-scan/trend.png)](https://bitdeli.com/free "Bitdeli Badge")
