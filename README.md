# **Introduction to the Standard Monitoring Framework (SMF)**
For a while now I’ve been helping customers implement standardised monitoring in various guises. These management packs help demonstrate the principle. They can be used as a starting point for implementing your own standard monitoring. The MPs have been put together in my spare time which means they have had limited testing, they should work in your environment, but I can’t be 100% certain for all the supported Unix/Linux distros. Solaris taught me not to assume what works on RHEL works everywhere ☹ 
# **History**
The idea for the SMF came from the great work that people like Russ Slaten and Tyson Paul have done on creating monitoring from configuration files. They both have created MPs that monitor ‘stuff’ by reading/discovering configuration from files. I liked the work they had done, to allow the easy creation of port and URL monitoring without having to use authoring tools, so much I decided to try and apply the same principle to as much monitoring as possible. 

# Goals
* Set of standardise monitors that target discovered objects
* Configuration of monitoring stored as properties of objects
* SCOM objects discovered based on registry keys on Windows and CSVs on Unix/Linux
* Move monitoring configuration out of SCOM making it easier for application SMEs to ‘own’ their monitoring
* Reduce the complexity and time to deploy monitoring
* Monitoring configuration becomes part of the application configuration and owned/deployed by application SMEs
* Monitoring is added to a Business Service for dashboarding/reporting
* Alerts have owner set based on object property (Can be disabled/delayed to avoid conflict with other alert routing processes)
* Business Service health state can be manually set (Allows dashboards to be red/amber if an incident is occuring that we don't currently have monitoring for)
  
# An example Windows Service monitoring
Instead of an application SME getting in touch with the SCOM SME (me) and asking for a new Windows Service monitor to be authored and implemented for a new service they have created. Even with Kevin Holman’s fragments this takes some time and as it’s a new or updated MP, I’m bound to fat finger something and it’ll need testing/fixing. 
With the SMF, the SME creates a set of registry keys on the servers where the service needs to be monitored describing which Windows service to monitor, when to monitor it, what priority/severity the alerts should be, the team that alerts should be routed to, and which business service the Windows service is part of. SCOM discoveries run and discovery the Windows Service to be monitored along with it’s configuration, starts monitoring it, and adds it to the required business service (and discovers the business service). Zero requirement for the SCOM SME to be involved. 
If creating registry keys and CSVs sounds like too much work for your application SMEs then to help get started I’ve created SCOM agent tasks that create the keys and CSVs with overridden information. But I really try to push the ownership to the SMEs. The less work I have to do the better! 

**_DANGER WILL ROBINSON_**

> The tasks are in optional MPs (Standard.Monitoring.Framework.Windows.Tasks and Standard.Monitoring.Framework.Linux.Tasks) because if your operator roles are not scoped correctly and health services not locked down they could be used to escalate an operators access to the monitored environment. Make sure you understand the risk before importing these MPs.

# _Common Properties_
All SMF monitored objects have these common base properties. 
* Business Service –Business Service the object is part of
* Component – Component the object is part of i.e. back end servers. Components are contained by Business Services and health rolls up. 
* Environment –  Environment that the object is part of
* Team – Team that alerts will be routed to
* Frequency – How often to run the monitoring
* Schedule Start Time – Time to start monitoring i.e. 00:00 or 09:00 etc…
* Schedule End Time – Time to stop monitoring i.e. 23:59 or 17:00
* Schedule Days – bitmask for the days of the week to run monitoring i.e. 127 or 7 days 62 for Monday to Friday
  * Sunday = 1
  * Monday = 2
  * Tuesday = 4
  * Wednesday = 8
  * Thursday = 16
  * Friday = 32
  * Saturday = 64
* Match Count – How many consecutive unhealthy samples needed before it’s unhealthy
* Severity – Severity of alerts generated and health state of monitor
* Priority – Priority of alerts generated
* Description – description of monitoring, will be included in alert description
* Documentation – Link to documentation, link will be included in alert description
# What can be monitored right now
(I have a list of other monitoring to add and am open to suggestions to be added)
* Windows Service 
  * Service is running… recovery to start if automatically if required
* Windows Scheduled Tasks
  * Is the Task enabled
  * Last result
  * Run duration
  * Time since last run
* OLEDB Connections and Queries (Windows Watcher)
  * Connection is successful
  * Value in the specified row/column of the result set is within thresholds
  * Supports Windows and Local Authentication
* URL (Windows Watcher)
  * CA Trusted
  * Certificate Expired
  * Certiifcate Expiring
  * Certificate Invalid
  * Content
  * DNS Resolution
  * Error Code
  * Reachable
  * Response Time
  * Status Code
* Remote Certificate (Windows Watcher)
  * CN Valid
  * CA Trusted
  * Certifcate Expired
  * Certifcate Expiring
* Windows Event Log
  * Repeated
  * Missing
  * Event reset
  * Time reset
* Windows Files
  * Count of files older/younger than threshold above or below threshold
  * Count of files smaller/larger than threshold above or below threshold
  * Count of files above or below threshold
* Windows Folder
  * Count folders older/younger than threshold above or below threshold
* Linux Log File
  * Regex is matched in file(s) time reset (tracks previously read lines)
* Linux Process
  * Count of process instances within thresholds
  * Percent CPU busy time is below threshold
  * Used Memory KB is below threshold
* Port (Linux Watcher)
  * Connection to port remote or local
* Windows Command – monitor any Windows command
  * Returncode
  * Regular expression match stdout
  * Stdout is between thresholds
* Linux Command
  * Returncode
  * Regular expression match stdout
  * Stdout is between thresholds

Those last two are really powerful and are used like Swiss Army Knives for monitoring.
# Other Existing Monitoring i.e. Microsoft SQL, Windows/Linux OS, Windows Clusters etc…
By setting the required registry keys and CSV entries it’s possible to include the health of other objects in the health of SMF business services. At the moment I’ve got discoveries for 
* Windows Server OS
* Linux OS
* Health Service Watcher
* Microsoft SQL on Windows Database Engine
* Microsoft SQL on Windows Database
* Windows Cluster
* Windows Cluster Resource Group
* Any Object - Requires the ObjectId of the object making it slightly more complex to add
  
When I get time I’ll add other common objects such as IIS servers, websites, application pools etc...  
# What does it look like
I’ll add some screenshots from the SCOM console and I’m creating a dashboard/perspective pack for SquaredUp
# What’s Next
Create some example registry keys and CSVs, create a quick start guide, and then start to work through the features and improvements back log…. 

Any suggestions/feedback gratefully received or if you want to help improve/fix the MPs get in touch. 

Thanks 
Keith

