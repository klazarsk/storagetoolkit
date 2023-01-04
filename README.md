# storagetoolkit
Kim's storage toolkit

Hi friends! You may recall that top disk consumer report I wrote a few years ago and maintained ever since - it was poorly-coded as it grew organically, tacking on each feature as I needed to gather info to shove into a ticket. Since I primarily used it at a certain hosting company whose ticketing system supported bbcode, it was hard-coded for bbcode markup. 



I've since rewritten the utility and incorporated html and ansi formatting as well as bbcode, with ansi format being the default. I've also added command line options including timeouts, omitting metadata, and ability to skip each of the reports to save time. 



It can be tremendously helpful as a training tool for junior sysadmins as well as for routine troubleshooting of disk usage on production servers. If you want to run it on enormous filesystems, I recommend leveraging the command line switches to turn off reports you do not care about and running it in a screen or tmux session - or alternatively you can set a timeout so each report will die after the specified time (it can take days to run on mounts with an enormous number of files). 



For now I'm releasing only the one utility, with more to come... eventually.

topdiskconsumer  -- Top Disk Consumer Report [version 0.1]


This script reports on the top disk consumers to help identify where cleanup is required.


Usage:


topdiskconsumer
When executed with no arguments, the script will identify the mount point 
containing the current working directory,then execute the report starting 
from the mount point, identifying and listing the top 20 largest files, the 
top 20 largest directories, and then the top 20 largest files aged over 30 
days.

Command line arguments:

	-f --format [format]
	Format headings with the addition of bold markup for use in ticketing system. 
Valid options:
		html - format headings with html bold tags
		bbcode - format headings with bbcode bold tags
		ansi - [DEFAULT] format headings with ansi bold tags (for terminals and richtext. This help screen always in ANSI format.)

	-n --number [number]
		Report top [number] largest files for each report section [default=20]

	-t --timeout [duration] set a timeout for each section of the report. For 
example, 60 (default time unit is seconds so this would timeout after 60 seconds),30s (for a 30 second timeout), 15m (timeout after 15 minutes), 2h (timeout after
2 hours). Accepts same values as _timeout_ command. Please note that specifying a timeout will result in incomplete and likely inaccurate and misleading results.
	-o --skipold skip report of files aged over 30 days 

	-d --skipdir skip report of largest directories

	-m --skipmeta omit metadata such as reserve blocks, start and end time, duration, etc.

	-u --skipunlinked skip report of open handles to deleted files

	-f --skipfiles skip report of largest files

