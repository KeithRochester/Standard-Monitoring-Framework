# **Introduction to the Standard Monitoring Framework (SMF)**

For a while now, I’ve been helping customers implement standardised monitoring in various guises. These management packs help demonstrate the principle. They can be used as a starting point for implementing your own standard monitoring. The MPs have been put together in my personal lab which means they have had limited testing, they should work in your environment, but I can’t be 100% certain for all the supported Unix/Linux distros. Solaris taught me not to assume what works on RHEL works everywhere. ☹ 

## **History**

The idea for the SMF came from the great work that people like Russ Slaten and Tyson Paul have done on creating monitoring from configuration files. They both have created MPs that monitor ‘stuff’ by reading/discovering configuration from files. I liked the work they had done, to allow the easy creation of port and URL monitoring without having to use authoring tools, so much I decided to try and apply the same principle to as much monitoring as possible. 

## Goals

* Set of standardise monitors that target discovered objects
* Configuration of monitoring stored as properties of objects
* SCOM objects discovered based on registry keys on Windows and CSVs on Unix/Linux
* Move monitoring configuration out of SCOM making it easier for application SMEs to ‘own’ their monitoring
* Reduce the complexity and time to deploy monitoring
* Monitoring configuration becomes part of the application configuration and owned/deployed by application SMEs
* Monitoring is added to a Business Service for dashboarding/reporting
* Alerts have owner set based on object property (Can be disabled/delayed to avoid conflict with other alert routing processes)
* Business Service health state can be manually set (Allows dashboards to be red/amber if an incident is occurring that we don't currently **yet** have monitoring for)
  
## An example Windows Service monitoring

Instead of an application SME getting in touch with the SCOM SME (me) and asking for a new Windows Service monitor to be authored and implemented for a new service they have created. Even with Kevin Holman’s fragments this takes some time and as it’s a new or updated MP, I’m bound to fat finger something and it’ll need testing/fixing. 
With the SMF, the SME creates a set of registry keys on the servers where the service needs to be monitored describing which Windows service to monitor, when to monitor it, what priority/severity the alerts should be, the team that alerts should be routed to, and which business service the Windows service is part of. SCOM discoveries run and discovery the Windows Service to be monitored along with it’s configuration, starts monitoring it, and adds it to the required business service (and discovers the business service). Zero requirement for the SCOM SME to be involved. 
If creating registry keys and CSVs sounds like too much work for your application SMEs then to help get started I’ve created SCOM agent tasks that create the keys and CSVs with overridden information. But I really try to push the ownership to the SMEs. The less work I have to do the better! 

**_DANGER WILL ROBINSON_**

> The tasks are in optional MPs (Standard.Monitoring.Framework.Windows.Tasks and Standard.Monitoring.Framework.Linux.Tasks) because if your operator roles are not scoped correctly and health services not locked down they could be used to escalate an operators access to the monitored environment. Make sure you understand the risk before importing these MPs.
>
>**Don’t give operators access to run the tasks on servers if they aren’t administrators of the servers already, otherwise they could use the tasks to give themselves admin access. Consider auditing task execution.**  

## Common Properties

All SMF monitored objects have these common base properties. 
* Business Service – Business Service the object is part of.
* Component – Component the object is part of i.e. back end servers. Components are contained by Business Services and health rolls up. 
* Environment – Environment that the object is part of.
* Team – Team that alerts will be routed to.
* Frequency – How often to run the monitoring.
* Schedule Start Time – Time to start monitoring i.e. 00:00 or 09:00 etc...
* Schedule End Time – Time to stop monitoring i.e. 23:59 or 17:00 etc...
* Schedule Days – Bitmask for the days of the week to run monitoring i.e. 127 or 7 days 62 for Monday to Friday.
  * Sunday = 1
  * Monday = 2
  * Tuesday = 4
  * Wednesday = 8
  * Thursday = 16
  * Friday = 32
  * Saturday = 64
* Match Count – How many consecutive unhealthy samples needed before it’s unhealthy.
* Severity – Severity of alerts generated and health state of monitor.
* Priority – Priority of alerts generated.
* Description – description of monitoring, will be included in alert description.
* Documentation – Link to documentation, link will be included in alert description.

## What can be monitored right now

(I am open to suggestions to be added)
* [Windows Service](.//Documentation//Monitoring%20Types/Windows%20Service%20Monitor.md)
  * Service is running… recovery to restart automatically if required
* [Windows Scheduled Tasks](.//Documentation//Monitoring%20Types/Windows%20Task%20Monitor.md)
  * Is the Task enabled
  * Last result
  * Run duration
  * Time since last run
* [OLEDB Connections and Queries (Windows Watcher)](.//Documentation//Monitoring%20Types/Windows%20OLEDB%20Monitor.md)
  * Connection is successful
  * Value in the specified row/column of the result set is within thresholds
  * Supports Windows and Local Authentication
* [URL (Windows Watcher)](.//Documentation//Monitoring%20Types/Windows%20URL%20Monitor.md)
  * CA Trusted
  * Certificate Expired
  * Certificate Expiring
  * Certificate Invalid
  * Content
  * DNS Resolution
  * Error Code
  * Reachable
  * Response Time
  * Status Code
* [Remote Certificate (Windows Watcher)](.//Documentation//Monitoring%20Types/Windows%20Remote%20Certificate%20Monitor.md)
  * CN Valid
  * CA Trusted
  * Certificate Expired
  * Certificate Expiring
* Windows Event Log
  * [Repeated](.//Documentation//Monitoring%20Types/Windows%20Event%20Log%20Repeated%20Event%20Monitor.md)
  * [Missing](.//Documentation//Monitoring%20Types/Windows%20Event%20Log%20Missing%20Event%20Monitor.md)
  * [Event reset](.//Documentation//Monitoring%20Types/Windows%20Event%20Log%20Event%20Reset%20Monitor.md)
  * [Time reset](.//Documentation//Monitoring%20Types/Windows%20Event%20Log%20Time%20Reset%20Monitor.md)
* Windows Files
  * [Count of files older/younger than threshold above or below threshold](.//Documentation//Monitoring%20Types/Windows%20File%20Age%20Count%20Monitor.md)
  * [Count of files smaller/larger than threshold above or below threshold](.//Documentation//Monitoring%20Types/Windows%20File%20Size%20Count%20Monitor.md)
  * [Count of files above or below threshold](.//Documentation//Monitoring%20Types/Windows%20File%20Count%20Monitor.md)
* Windows Folder
  * [Count folders older/younger than threshold above or below threshold](.//Documentation//Monitoring%20Types/Windows%20Folder%20Age%20Count%20Monitor.md)
* Linux Log File
  * [Regex is matched in file(s) time reset (tracks previously read lines)](.//Documentation//Monitoring%20Types/Linux%20Time%20Reset%20Log%20File%20Monitor.md)
* [Linux Process](.//Documentation//Monitoring%20Types/Linux%20Process%20Monitor.md)
  * Count of process instances within thresholds
  * Percent CPU busy time is below threshold
  * Used Memory KB is below threshold
* TCP Port (Remote/Local)
  * [Linux Watcher](.//Documentation//Monitoring%20Types/Linux%20Port%20Monitor.md)
  * [Windows Watcher](.//Documentation//Monitoring%20Types/Windows%20Port%20Monitor.md)
  * ICMP Ping (Remote/Local)
  * [Linux Watcher](.//Documentation//Monitoring%20Types/Linux%20Ping%20Monitor.md)
  * [Windows Watcher](.//Documentation//Monitoring%20Types/Windows%20Ping%20Monitor.md)
* [Windows Command – monitor the output of any command](.//Documentation/Monitoring%20Types/Windows%20Command%20Monitor.md)
  * Returncode
  * Regular expression match stdout
  * Stdout is between thresholds
* [Linux Command – monitor the output of any command](.//Documentation/Monitoring%20Types/Linux%20Command%20Monitor.md)
  * Returncode
  * Regular expression match stdout
  * Stdout is between thresholds

Those last two are really powerful and are used like Swiss Army Knives for monitoring. Invariably application SMEs will have admin scripts or executables that we can use to monitor health. By not embedding them into SCOM MPs we can leave the maintenance of them to the application SMEs. Less work for the SCOM SME! 😊

## Other Existing Monitoring i.e. Microsoft SQL, Windows/Linux OS, Windows Clusters etc…

By setting the required registry keys and CSV entries it’s possible to include the health of other objects in the health of SMF business services. At the moment I’ve got discoveries for: 
* Windows Server OS - [Example Reg Key](.///Documentation/Example%20Files/WindowsServer.reg)
* Linux OS - [Example CSV](.///Documentation/Example%20Files/linuxcommand.csv)
* Health Service Watcher - [Example Reg Key](.///Documentation/Example%20Files/WindowsHealthServiceWatcher.reg)
* Microsoft SQL on Windows Database Engine - [Example Reg Key](.///Documentation/Example%20Files/WindowsHealthServiceWatcher.reg)
* Microsoft SQL on Windows Database - [Example Reg Key](.///Documentation/Example%20Files/WindowsHealthServiceWatcher.reg)
* Windows Cluster - [Example Reg Key](.//Documentation/Example%20Files/WindowsHealthServiceWatcher.reg)
* Windows Cluster Resource Group - [Example Reg Key](.//Documentation/Example%20Files/WindowsHealthServiceWatcher.reg)
* Any Object - Requires the ObjectId of the object making it slightly more complex to add - ###Guide Coming Soon##
  * [Example Reg Key](.//Documentation/Example%20Files/WindowsGenericObject.reg)
  * [Example CSV](.//Documentation/Example%20Files/linuxgenericobject.csv)

  
When I get time I’ll add other common objects such as IIS servers, websites, application pools etc...  

## What does it look like

The screen capture below shows the diagram view for a simple Business Service created using the SMF.

![Business Services Diagram View](.//Documentation/Screencaps/Example%20Business%20Service.png)

If you have SquaredUp (and you really should) I've created some [dashboards and perspectives](Documentation/SquaredUp/SquaredUp.md).

## What’s Next

Any suggestions/feedback gratefully received or if you want to help improve/fix the MPs get in touch. 

Thanks 
Keith

