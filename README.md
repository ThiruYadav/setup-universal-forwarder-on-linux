# setup-universal-forwarder-on-linux
Configure a Splunk Forwarder on Linux (Debian and ubundu)

Step 1: Download Splunk Universal Forwarder
http://www.splunk.com/download/universalforwarder
(.deb file and 64bit package if applicable)

Step 2: Install Forwarder
Command: sudo dpkg –i /path/filename.deb
sudo apt-get install –f
Agree the licence for splunk forwarder

Step 3: Enable boot-start/init script
Command: /opt/splunkforwarder/bin/splunk enable boot-start

Step 4: Configure Forwarder connection to Index Server
Command: /opt/splunkforwarder/bin/splunk add forward-server host.domain:9997 
(Where host.domain is the fully qualified address or IP of the index and 9997 is the receiving port you create on the Indexer)

Step 5: Enter username and password
Default : Username: admin 
Password: changeme

Step 6: Test Forwarder connection
Command: /opt/splunkforwarder/bin/splunk list forward-server
(Lists the active and inactive forwards of splunk forwarder)

Step 7: Add Data
Command: /opt/splunkforwarder/bin/splunk add monitor /path/ -index main -sourcetype name 
(Where /path/ is the path to application logs on the host that you want to bring into Splunk, and the name you want to associate with that type of data)
This will create a file: inputs.conf in /opt/splunkforwarder/etc/apps/ splunkforwarder/default/

   Or edit
input.conf (/opt/splunkforwarder/etc/apps/ splunkforwarder/default/)
[monitor:///path/] 
sourcetype = syslog
index = default
disabled = false
(Where /path/ is the path of the .log file on the host)
Output.conf (/opt/splunkforwarder/etc/system/local /)
[tcpout]
defaultGroup=syslog_index
disabled = false
[tcpout:syslog_index]
server=splunkserver:9997
[tcpout-server :// splunkserver:9997 ]

