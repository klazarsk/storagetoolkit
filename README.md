# Kims Storage Toolkit

## Documentation

This is a draft of the documentation; among further refinements will be documentation updates. This is simply a copy and paste of the help screen:

topdiskconsumer  -- Top Disk Consumer Report [version 0.6]

This script reports on the top disk consumers to help identify where cleanup is required.

## Usage

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
		 hosting the specified directory and run from that mount point. Mutually 
		 exclusive with the -A | --alt-root option.
		

	-A --alt-root - treat the specified directory as an alternate root; in other words
		 report the top disk consumers from the specified point, deeper; do not check for
		 the actual mount point. Musually exclusive with --path option. This option is very 
		 when used in combination of a bind mount of / if you suspect mounts are hiding large
		 disk consumers from view.		

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

	-v --version display the version number then exit.

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

P1 defects:
- [ ] largest deleted open files: Does not work on Ubuntu 20: listing open file handles doesn't work on Ubuntu (am currently in Dallas for Red Hat tech exchange will review issue on my Ubuntu VMs week starting Feb 05). Cause: lsof distributed with Ubuntu displays different format by default. Plan to reimplement test on RHEL, Ubuntu, and (OpenSUSE) Tumbleweed. Previously tested on RHEL and older release of Tumbleweed and originally developed one-liner on Tumbleweed. 


# Red Hat Sysadmin blog

https://www.redhat.com/sysadmin/free-storage-space-linux

# Important Note:

Re: automated cleanup 

I hear your requests and suggestions, and while I agree in principle, I've seen too many junior admins mis-
apply "swiss army knife" tools resulting in storage disasters, including completely kicking storage out from
under live databases on production servers.

## Update: 

After discussion with a colleague and mulling it over, as a solution to mitigate risk but also allow cleanup, I've decided provide a config file spec to allow for automated cleanup while seeking to avert gross mis-use of the utility by junior administrators. This will allow for usage of the script in financial institutions hosted at companies where support are restricted to "read-only" actions while also enabling automated cleanup on workstations and dev/staging/preprod environments.

ETA: by end of 2Q2023

# Roadmap 

Coming March 2023
