# Cyber_Deception-Tools_and_Techniques

## Disclaimer!

**<span style="color:red"> All lab materials and content performed in this lab are provided by CMU and its Students, specifically CMU's Applied Information Assurance (AIA) course taught at the INI. I give all credit to the INI AIA students and CMU for the environment, content, and setup of this lab, such was not done by my own hands.</span>**

## Starting Point/Setup

This lab topology involves a compromised server that is connected to 2 decoy machines (DM1 and DM2) and 1 monitoring machine.
- The compromised server is running Kali Linux
- Both Decoy Servers are running Ubuntu
- The Monitoring Server is running Ubuntu with ELK Stack

The present scenario involves an attacker breaching a hypothetical organization, compromising one of its machines, and seeking to propagate to other machines on the network. However, the current organization already has security measures in place to thwart such attempts and deceive the attacker. The following walkthrough details various cyber deception tools and techniques that an organization can use to defend against cyber attacks.

## Deception Part 1

*Started Filebeat on both decoy devices to begin recording and sending logs to the monitoring system*

![EEG Band Discovery](/assets/FileBeatStart.png)


*Started Port Spoofer on Decoy 2 to create fake ports*

![EEG Band Discovery](/assets/PortSpoofingStart.png)


*As the attacker, I ran an Nmap scan to see what other devices were available to move to. The below shows available machines aswell as generated fake ports by Portsspoofer (although the attacker does not now)*

![EEG Band Discovery](/assets/AttackerSpoofedNmapScan.png)


*Conducted an nmap probe scan to understand more about the machine shown in the above image. (As an attacker digs deeper into each port they will realize that results are different from the initial scan aswell as other identifiers that hint to this machine being difficult to exploit)*

![EEG Band Discovery](/assets/NmapProbeSV.png)


*While this is occurring, on the Monitor side, a Security analyst will receive an alert indicating a port scanning attack and can take the necessary security procedures to isolate the machine and address the security breach*

![EEG Band Discovery](/assets/PortScanAttackLogs.png)

## Deception Part 2

*Started Cowerie, an SSH honeypot, on Decoy 2*

![EEG Band Discovery](/assets/CowrieSetup.png)



*As the attacker, Ive realized that the ports in the previous machines may have been spoofed and decide to run another port scan to find another machine. As shown below the new machine has an SSH server as the attacker I attempt to ssh into the server*
![EEG Band Discovery](/assets/SuspectedSpoofAttackerNewScan.png)


*Frustrated with attempting different passwords, I as the attacker decide to run a brute force script of common SSH passwords to try and get into the machine. It looks like I found a successful password.*

![EEG Band Discovery](/assets/BruteForcePasswordScript.png)


*The attacker tries the password and can finally SSH into the server*

![EEG Band Discovery](/assets/BruteForcePasswordSuccessful.png)



*Exploring the new server I discover a secret file containing an email server admin portal endpoint*

![EEG Band Discovery](/assets/AttackerFoundSecretFile.png)


*While the attacker believes they have found something useful, little do they know that they have already alerted Security personnel. On the Monitoring side, a Security analyst will receive an alert indicating an SSH bruteforce attack and can take the necessary security procedures to isolate the machine and address the security breach*

![EEG Band Discovery](/assets/CowrieSSHAttackLogs.png)

## Deception 3


*Started SpringBoot a JAVA based API*

![EEG Band Discovery](/assets/StartSpringBoot.png)



*Started Django web framework*

![EEG Band Discovery](/assets/StartDjangoHoneyPot.png)



*Carrying on from the previous section, I as the attacker decide to investigate further into the URL I found, and test to see if it actually works.The curl command proves the email server is legit*

![EEG Band Discovery](/assets/TestEmailServer.png)


*It appears that the endpoint is available and accessible, however, the attacker needs a password to log in, I try a few passwords to no avail*

![EEG Band Discovery](/assets/EmailEndpoint.png)


*While the attacker is doing this on the Monitoring side, a Security analyst will receive an alert indicating an unauthorized email entry login to the dummy email server. At this point they can take the necessary security procedures to isolate the machine and address the security breach. But, lets continue on to see what the attacker does*

![EEG Band Discovery](/assets/UnauthorizedEmailEntryLog.png)

## Deception 4

*Spidertrap started on decoy machine 2 to create a set of fake web pages*
![EEG Band Discovery](/assets/StartSpiderTrap.png)


*Unsuccessful with login in attempts to the email/login endpoint. I as the attacker attempt to use gobuster, a brute-force directory enumeration tool to find different endpoints on the email server. However, as shown below there seems to be a bunch of strange paths, it seems that Gobuster is not providing authentic results*

![EEG Band Discovery](/assets/GobusterFailure.png)


*On the Monitoring side, a Security analyst will receive an alert from the attacker doing this that indicates a directory enumeration attack and can take the necessary security procedures to isolate the machine and address the security breach*

![EEG Band Discovery](/assets/DirectoryEnumerationLogs.png)


## Summary
Within this Lab, I illustrated the use of various deception techniques and tools (e.g. Cowrie, Spidertrap, and Portspoofer) that can be used as a means to delay attackers and give Security professionals time to discover and analyze security breaches/alerts. There are many other tools and techniques that can be implemented depending on an organization's functions and internal architecture. Hopefully, this lab can provide examples to others of means by which they can implement similar cyber deception tools and techniques in their own cyber environment.
  
