#Packaging

## Introduction
This document intended to help [**RPi-Monitor**](http://rpi-experiences.blogspot.fr/)'s package maintainer to know what to install and where.

## Version
This document describe file organisation for **Version 2.8**

## Dependencies
**rpimonitord** is a perl script which require the following perl modules to work:

 * librrds-perl
 * libhttp-daemon-perl
 * libjson-perl
 * libipc-sharelite-perl
 * libfile-which-perl
 * aptitude (required by script checking upgradable packages)

## Installation

###Programs

* /usr/bin/rpimonitord : *Daemon extracting data from the system and embedding the web application server - The help page is used to generate manpage*
* /etc/cron.d/rpimonitor : *daily extraction the status of package update updating the file updatestatus.txt*
* /etc/init.d/rpimonitor : *sysVinit startup script*

**Note**:

* **upstart** and **systemd** script are also avialable in the repository

###Configuration

* /etc/rpimonitor/daemon.conf : *configuration of rpimonitord daemon*
* /etc/rpimonitor/data.conf : *(symlink to template/<distribution>.conf) configuration of default data to be extracted and presented*
* /etc/rpimonitor/\*.conf : *all other *.conf file will be parsed to look for data to be monitored*
* /etc/rpimonitor/template/\*.conf : *data configuration template customized for different distribution and additionnal examples*

Some configuration files are provided for different distribution (raspbian, xbian, ...).
These files are stored into the subdirectory /etc/rpimonitor/templates/.
For supported distribution, the post installation script of package creates a link, data.conf, pointing to the configuration files dedicated to the distribution.

** Note: **
The template directory is also containing some templates that can be used as example to customize configuration.

###Manpages

* /usr/share/man/man5/rpimonitord.conf.5.gz : *Manpage for rpimonitor and data extraction configuration*
* /usr/share/man/man1/rpimonitord.1.gz: *Manpage for rpimonitord command line usage*

###Web Interface

* /usr/share/rpimonitor/web : *Directory containing html*
* /usr/share/rpimonitor/web/js: *Directory containing javascripts*
* /usr/share/rpimonitor/web/css: *Directory containing style*
* /usr/share/rpimonitor/web/img: *Directory containing images*

**Note:**

When **RPi-Monitor** is configured to not use the internal server, the json are written on the disk into the web root directory /usr/share/rpimonitor/web

###Scripts

* /usr/share/rpimonitor/scripts/updatePackagesStatus.pl: *Script periodically executed to update /var/lib/rpimonitor/updatestatus.txt*

###Data

* /var/lib/rpimonitor/web/stat : *Directory containing \*.rrd*
* /var/lib/rpimonitor/updatestatus.txt: *Current status of packages update*
