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