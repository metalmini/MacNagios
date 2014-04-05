MacNagios
=========

Nagios status bar monitoring tool for MacOS X

Installation - Client
=====================

* Download the binary, links below.
* Unzip it and copy/move the application to your Applications folder.
* Create a macnagios-config.plist file in either your home directory or in /etc/
* Example config file:

		<?xml version="1.0" encoding="UTF-8"?>
		<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
		<plist version="1.0">
		<dict>
		
			<key>NotifyOnChange</key> <!-- should we send messages to the notification center -->
			<true/>
		
			<key>NotifyWithSound</key> <!-- should our messages also include a sound? if NotifyOnChange is false, this will do nothing -->
			<true/>
		
			<key>SkipIfNotificationsDisabled</key> <!-- if true, then services which have notifications disabled are skipped and not considered -->
			<true/>
		
			<key>CheckFrequencySeconds</key> <!-- how many seconds to wait between checks - don't make this too fast, you might hurt yourself -->
			<integer>30</integer>
		
			<key>Servers</key>
			<array>
		
			<!-- point this at your nagios setup - see other instructions for how to get statusJson.php -->
			<dict>
				<key>Name</key>
				<string>Example1</string> <!-- what's in a name -->
				<key>URL</key>
				<string>http://example.com/nagios/statusJson.php</string> <!-- this is where the real data comes from, as JSON -->
				<key>AdminURL</key>
				<string>http://admin.edit.firechrome.org/nagios/</string> <!-- this is where you go when you click for more info about the status -->
				<key>Username</key> <!-- authentication data - comment this and the 2 next lines out if you don't need it (i.e. you are restricting by IP) -->
				<string>nagios</string>
				<key>Password</key>
				<string>secret</string>
			</dict>
 			
			<!-- you can specify as many nagios instance as you like, list each out here as a dict 
			<dict>
				<key>Name</key>
				<string>Example2</string>
				<key>URL</key>
				<string>http://example2.example.com/nagios/cgi-bin/statusJson.php</string>
				<key>AdminURL</key>
				<string>http://example2.example.com/nagios/</string>
				<key>Username</key>
				<string>nagios</string>
				<key>Password</key>
				<string>secret</string>
			</dict>
			-->
		
			</array>
		
		</dict>
		</plist>


Note that you'll need to add the statusJson.php file on the Nagios server, see below.

Server Setup
============

For status information, MacNagios uses statusJson.php: https://github.com/lizell/php-nagios-json

Installation is really simple:

* Find the folder that has your nagios index.php in it (generally something like /usr/share/nagios/) and download a copy of statusJson.php, like so:

		curl 'https://raw.githubusercontent.com/lizell/php-nagios-json/master/statusJson.php' > statusJson.php

* Edit the top of statusJson.php to have the correct path to your Nagios status.dat file


Downloads
=========
(MacOS X 10.9+ 64-bit)

v0.1 - https://docs.google.com/file/d/0B8eMv4SjaIClSzNuS1REV3dnR3c (File -> Download)

FAQ
===

Since I'm writing this this document as I'm first releasing the software, the total number of questions I've received is zero.  With a static frequency of zero for all questions, the only thing that made sense was to list whatever came to mind, in random order:

### Are you Scottish?
No.  But Scotland is cool.

Credits
=======
MacNagios was written by Brad Peabody.  Inspired by NagiosDock (http://nagiosdock.sourceforge.net/), I needed something more up to date that just made it simple for me to get the feedback on multiple nagios instances easily from my Mac workstation.
