# Security_Surveillance_System

Pre-requirements
Powershell 5
Sysmon (Downloaded, configured and installed by installer.py)
Python 3.6 (64-bit) - should work on Python 3.x
Tshark (Malware analysis only)
Various Python3 libraries (requirements.txt)
StoneEngine library (included, first time published, high level windows event log interface - Alpha state)
Supported system events
Some of the events are only supported in Malware Analysis Mode

Filesystem changes
Permitted network connections
PowerShell activity (detailed only with PowerShell 5)
Process creation
SMB activity
Scheduled tasks
Local accounts manipulations
Success/Failed logins
Drivers load
Raw disk access
Registry monitoring
Pipe events
Services
Audit log cleared
WMI monitoring of queries + WMI persistence
DNS requests capture (via Tshark)
Installation - Endpoint Detection Mode
For Malware analysis mode - refer to next section

STEPS:
<Download newest release>
cmd.exe (Run as admin)
pip3 install -U -r requirements.txt
python installer.py sysmon
  => Choose endpoint detection mode
python installer.py psaudit
python installer.py auditpol
python installer.py install
  => Choose endpoint detection mode
python installer.py exceptions
[Apply section] Installation - How to enable WMI audit?
Installation - Malware analysis Mode
For Endpoint detection mode - refer to previous section

STEPS:
<Download newest release>
cmd.exe (Run as admin)
pip3 install -U -r requirements.txt
python installer.py sysmon
  => Choose malware analysis mode
python installer.py psaudit
python installer.py auditpol
python installer.py install
  => Choose malware analysis mode
[Install tshark] https://www.wireshark.org/download.html // To default location
[Apply section] Installation - How to choose network interface for malware listening? // (currently only DNS)
[Apply section] Installation - How to enable WMI audit?
[Apply section] Installation - How to monitor specific directories?
Installation - How to enable WMI audit?
compmgmt.msc
Services and Applications -> WMI Control -> Properties
Security -> Security -> Advanced -> Auditing -> Add

Select principal: Everyone
Type: All
Show advanced permissions:
  Select all (Execute Methods ... Edit Security)
Why it's not in installer.py script? It's hard to do it programmatically

Installation - How to choose network interface for malware listening?
Edit C:\Program Files\Attack Monitor\config\attack_monitor.cfg

Change in section [feeder_network_tshark]: network_interface=PUT INTERFACE NAME HERE # without quotes

How to determine inteface name?
TShark is using name from Control Panel\Network and Internet\Network Connections (Change adapter settings) e.g. name: WiFi AC => Custom name defined by user e.g. name: Ethernet0

Installation - How to monitor specific directories?
Edit C:\Program Files\Attack Monitor\config\monitored_directories.json

For malware analysis it's recommended to monitor all events (except dir_modified) for directory C:\ with recursive flag enabled. Please add also additional directories if relevant.
