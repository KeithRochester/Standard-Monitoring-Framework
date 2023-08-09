* [Windows Service](.//Windows%20Service%20Monitor.md)
  * Service is running… recovery to restart automatically if required
* [Windows Scheduled Tasks](.//Windows%20Task%20Monitor.md)
  * Is the Task enabled
  * Last result
  * Run duration
  * Time since last run
* [OLEDB Connections and Queries (Windows Watcher)](.//Windows%20OLEDB%20Monitor.md)
  * Connection is successful
  * Value in the specified row/column of the result set is within thresholds
  * Supports Windows and Local Authentication
* [URL (Windows Watcher)](.//Windows%20URL%20Monitor.md)
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
* [Remote Certificate (Windows Watcher)](.//Windows%20Remote%20Certificate%20Monitor.md)
  * CN Valid
  * CA Trusted
  * Certificate Expired
  * Certificate Expiring
* Windows Event Log
  * [Repeated](.//Windows%20Event%20Log%20Repeated%20Event%20Monitor.md)
  * [Missing](.//Windows%20Event%20Log%20Missing%20Event%20Monitor.md)
  * [Event reset](.//Windows%20Event%20Log%20Event%20Reset%20Monitor.md)
  * [Time reset](.//Windows%20Event%20Log%20Time%20Reset%20Monitor.md)
* Windows Files
  * [Count of files older/younger than threshold above or below threshold](.//Windows%20File%20Age%20Count%20Monitor.md)
  * [Count of files smaller/larger than threshold above or below threshold](.//Windows%20File%20Size%20Count%20Monitor.md)
  * [Count of files above or below threshold](.//Windows%20File%20Count%20Monitor.md)
* Windows Folder
  * [Count folders older/younger than threshold above or below threshold](.//Windows%20Folder%20Age%20Count%20Monitor.md)
* Linux Log File
  * [Regex is matched in file(s) time reset (tracks previously read lines)](.//Linux%20Time%20Reset%20Log%20File%20Monitor.md)
* [Linux Process](.//Linux%20Process%20Monitor.md)
  * Count of process instances within thresholds
  * Percent CPU busy time is below threshold
  * Used Memory KB is below threshold
* TCP Port (Remote/Local)
  * [Linux Watcher](.//Linux%20Port%20Monitor.md)
  * [Windows Watcher](.//Windows%20Port%20Monitor.md)
* ICMP Ping (Remote/Local)
  * [Linux Watcher](.//Linux%20Ping%20Monitor.md)
  * [Windows Watcher](.//Windows%20Ping%20Monitor.md)
* [Windows Command – monitor the output of any command](.//Windows%20Command%20Monitor.md)
  * Returncode
  * Regular expression match stdout
  * Stdout is between thresholds
* [Linux Command – monitor the output of any command](.//Linux%20Command%20Monitor.md)
  * Returncode
  * Regular expression match stdout
  * Stdout is between thresholds