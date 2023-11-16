# OMA-DM-Synchelper-for-Low-End-Hardware
This little tool can be used to increase MDM synchronization reliability on low-end hardware

# What is this for?
On low end hardware that has only 4 GB ram available the Intune synchronization process can get stale due to the fact the RAM/CPU usage is prioritized to be used by other apps.
This can result in the behavior that the device does only synchronize correctly if it is not used by the user and this often to the fact that the device does not synchronize for weeks/month.

# How does that happen?
The OMA-DM synchronization process (omadmclient.exe) runs by default with "below normal" priority. Therefore other apps are prefered by Windows when it comes to the allocation of ressources. On low end hardware this can lead to the problem that the omadmclient.exe does not run reliable anymore and often is not able to finish a synchronisation process.

# How can we mitigate this?
This is what this tool is for: This tool increases the process priority of the omadmclient.exe if no successfull synchronisation took place within a certain timeframe. It can also be configured to always increase the process priority. With the increase of process priority the omadmclient.exe runs much more reliable and synchronisation is more often successfull.

# How do the tool work?
Easy: You just run the MSI using a Win32 Apps (or MSI LoB). The MSI takes two command line arguments:
ACCEPTEDDELAY=12 DESIREDPRIORITY=AboveNormal
ACCEPTEDDELAY: The timeframe during which a sychronization has to be occured before the process priority is increased.
DESIREDPRIORITY: The new priority of the omadmclient.exe (High, AboveNormal, Normal, BelowNormal, Low).
