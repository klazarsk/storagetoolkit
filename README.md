# Kims Storage Toolkits

## Documentation

This is a draft of the documentation; among further refinements will be documentation updates. This is simply a copy and paste of the help screen:

topdiskconsumer  -- Top Disk Consumer Report [version 0.4]

This script reports on the top disk consumers to help identify where cleanup is required.

## Usage

topdiskconsumer
When executed with no arguments, the script will identify the mount point 
containing the current working directory,then execute the report starting 
from the mount point, identifying and listing the top 20 largest files, the 
top 20 largest directories, and then the top 20 largest files aged over 30 
days.

```
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
		 ansi - [DEFAULT] format headings with ansi bold tags {for terminals and
		 richtext. This help screen always in ANSI format.}

	-p --path [path] explicitly set path to run from (it will identify the mount
		 hosting the specified directory and run from that mount point.

	-l --limit [number]
		 Report limited to top [number] largest files for each report section [default=20]

	-t --timeout [duration] set a timeout for each section of the report. For
		 example, 60 default time unit is seconds so this would timeout after 60 seconds,
		 30s (for a 30 second timeout), 15m (timeout after 15 minutes), 2h (timeout after
		2 hours). Accepts same values as _timeout_ command. Please note that specifying a
		 timeout will result in incomplete and likely inaccurate and misleading results.

   	-o --skipold skip report of files aged over 30 days

	-d --skipdir skip report of largest directories

	-m --skipmeta omit metadata such as reserve blocks, start and end time, duration, etc.

	-u --skipunlinked skip report of open handles to deleted files

	-f --skipfiles skip report of largest files

	-t --temp [directory] Specify an an alternate temp directory when /tmp is too full for temp
		 files to allow report generation.

Please note: the Top [number] Directories report module includes the "total" size. This is intentional.
This script can only access files that you have access to; either use sudo or root
to execute it. You could alternatively chmod the script with suid rights, but that may be a
security risk in finance, medical, and government environments by revealing confidential
filenames to unprivileged users. Choose to suid with care.

```

## _topdiskconsumer_ Known Issues/todo list
- [ ] getopts offers better argument processing
- [ ] needs a man page
- [ ] needs an rpm (will do this after writing the man pages)


# Red Hat Sysadmin blog

https://www.redhat.com/sysadmin/free-storage-space-linux

# Important Note:

It's been suggested that this tool be enhanced to clean up .local/cache and other temp file locations.

I hear your requests and suggestions, and while I agree in principle, I've seen too many junior admins mis-
apply "swiss army knife" tools resulting in storage disasters, including completely kicking storage out from
under live databases on production servers.

This tool is not intended to be an analog to the proprietary tool "ccleaner"

I'm intending this tool to be used as a read-only tool for aid in diagnosing issues, and with the suggestion
of enabling the suid bit, it would be a mistake to allow to go ahead and assume it is safe to clean anything,
even if it is just "/tmp' and '/home/*/./cache' and '/home/*/.local'; there are numerous security concerns,
risk of interrupting production services, or depending on silly user tricks, completely destroying a system.

As such this tool will remain a read-only diagnostic aid to guide cleanup, per the UNIX principle of one tool
one job.
