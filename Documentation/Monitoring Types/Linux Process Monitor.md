﻿
# Linux Process Monitor

Linux Process Monitor. 

Can monitor:

* Number of instances of a process is within range
* Used Memory KBytes is below threshold
* Percent Busy Time is below threshold

Metrics that can be collected for dashboards/reports:

* Instance Count
* Used Memory KBytes
* Percent Busy Time 

## Adding Monitoring

To add a Linux Process Monitor...

* Create/update **/etc/opt/smf/scom/discovery/linuxprocess** on the agent that will execute the command. [Example CSV](../Example%20Files/linuxprocess.csv)
* Use the **SMF: Add Process Monitor** task.

## Linux Process Properties 

|Property|Description|
|-|-|
|Process Name|Name of the process to be monitored|
|Arguments Filter Expression|Arguments filter to use to identify the process to be monitored(Optional)|
|Minimum Instances|Minimum number of process instances|
|Maximum Instance|Maximum number of process instances|
|Monitor Percent Busy Time|Controls if the percent busy time for the process should be monitored|
|Collect Percent Busy Time|Controls if the percent busy time for the process should be collected for reporting/dashboards|
|Monitor Used Memory KBytes|Controls if the Used Memory KBytes for the process should be monitored|
|Maximum Percent Busy Time|Maximum Percent Busy Time|
|Maximum Used Memory KBytes|Maximum Used Memory KBytes|
|Collect Used Memory KBytes|Controls if the Used Memory KBytes for the process should be collected for reporting/dashboards|
|Monitor Instance Count|Controls if the instance count for the process should be monitored|
|Collect Instance Count|Controls if the instance count for the process should be collected for reporting/dashboards|

## General Properties

|Property|Description|
|-|-|
|Business Service|The name of the business service that the monitoring is part of|
|Environment|Which lifecycle environment does the business service belong to. E.g. Production, UAT, DEV, etc...|
|Business Service Team|Team that owns the business service|
|Component Name|Name of the logical group that the object belongs to. Used to group similar objects together. E.g. Backend server objects in a Backend Server Component Group|
|Frequency|Frequency in seconds that the monitoring will run|
|Match Count|The number of consecutive samples that must occur before the monitor is unhealthy|
|Schedule Start Time|Time of day that monitoring will run from e.g. 00:00, 08:00, etc...|
|Schedule End Time|Time of day that monitoring will stop running e.g. 23:59, 17:00, etc...|
|Schedule Days|Bit mask for the days of the week that monitoring should run<br>Sunday = 1<br>  Monday = 2 <br>Tuesday = 4<br>Wednesday = 8<br>Thursday = 16<br>Friday = 32<br>Saturday = 64<br><br>Sunday to Saturday = 127<br>Monday to Friday = 62.|
|Description|Description of the object being monitored. This text is included in the alert body|
|Severity|Severity or alerts and state on dashboards. Critical or Warning|
|Priority|Priority that alerts will be assigned. High, Medium, or Low|
|Documentation|Link to documentation. Will be referenced in alerts|
|Object Team|The name of the team that will be responsible for resolving alerts generated by the monitoring|
