# **Using The SCOM Agent Tasks to Build a Business Service**
In this example I'll use the Standard Monitoring Framework SCOM agent tasks to create the registry keys and CSV values to create a Business Service based on the following table. This is a very simple example of what can be done, but the basic principal for creating the registry keys and CSV values is the same for all monitoring types, using the SCOM agent tasks.  

|Object|Monitoring Required|
|-|-|
|Frontend Servers|Include health of existing Windows Servers u92clu1/2|
|Database Engines|Include the health of existing SQL DBE u92sql3|
|RF Terminals|Ping monitor of RF terminal 1 (10.0.0.2)
|Broker|Monitor the WMS broker process (omiserver) on linux server u92rhel1 
|Team|WMS Support|
|Business Server|WMS|
|Environment|Production|

# Goal 

![Business Services Diagram View](./Screencaps/SCOM%20Task%20Deployment%20Example%20015.png)

# Steps

> The tasks are in optional MPs (Standard.Monitoring.Framework.Windows.Tasks and Standard.Monitoring.Framework.Linux.Tasks) because if your operator roles are not scoped correctly and health services not locked down they could be used to escalate an operators access to the monitored environment. Make sure you understand the risk before importing these MPs.

I'll start of by adding the existing object to the business service then I'll create the new custom ping and process monitoring.


To add the Windows Servers navigate to a view that displays Windows Computer objects. Select the Servers to be added and start the **SMF: Add Windows Server to Business Service** task.

![Add Server Task](./Screencaps/SCOM%20Task%20Deployment%20Example%20001.png)

Override the task parameters with the required details.

![Add Server Task Overrides](./Screencaps/SCOM%20Task%20Deployment%20Example%20002.png)

Confirm the override details and click Run. 
>Note we can run the task against multiple objects using the same override details.

![Add Server Task Confirm](./Screencaps/SCOM%20Task%20Deployment%20Example%20003.png)

To add the SQL Database Engine navigate to a view that displays SQL Database Engines objects. Select the SQL Database Engine Instance to be added and start the **SMF: Add SQL Database Engine to Business Service (Database Engine)** task.

![Add SQL DBE Task ](./Screencaps/SCOM%20Task%20Deployment%20Example%20004.png)

Override the task parameters with the required details. 
>Note because this task is targeted at SQL DBE instances the Instance Name is populated using the target detail. There is a version of this task that targets Windows Computers that requires the Instance Name to be manually populated.

![Add SQL Task Overrides](./Screencaps/SCOM%20Task%20Deployment%20Example%20005.png)

Confirm the override details and click Run. 

![Add SQL Task Confirm](./Screencaps/SCOM%20Task%20Deployment%20Example%20006.png)

To add a Ping monitor navigate to a view that shows the Windows Computer that will perform the ping test. In this case I'm using a Windows Server, but the same approach can be used to ping from a Unix/Linux server. Start the **SMF: Add Ping Monitor** task.

![Add Ping Task](./Screencaps/SCOM%20Task%20Deployment%20Example%20007.png)

Override the task parameters with the required details. 

![Add Ping Task Overrides](./Screencaps/SCOM%20Task%20Deployment%20Example%20008.png)

Confirm the override details and click Run. 

![Add Ping Task Confirm](./Screencaps/SCOM%20Task%20Deployment%20Example%20009.png)

To add a Unix/Linux Process monitor navigate to a view that shows the Linux Computer that runs the process to be monitored. Start the **SMF: Add Process Monitor** task.

![Add Process Task](./Screencaps/SCOM%20Task%20Deployment%20Example%20010.png)

Override the task parameters with the required details. 

![Add Process Task Overrides](./Screencaps/SCOM%20Task%20Deployment%20Example%20011.png)

Confirm the override details and click Run. 

![Add Process Task Confirm](./Screencaps/SCOM%20Task%20Deployment%20Example%20012.png)

Now that the Registry keys and CSV values have been created we can either wait for the discoveries to run (default is every 4 hours) or we can use the **SMF: Trigger Standard Monitoring Disocveries** task, that is targeted at Windows and Unix/Linux Computers

![Trigger Discocveries](./Screencaps/SCOM%20Task%20Deployment%20Example%20013.png)

Once the discoveries have run we will be able to see the newly created Business Service in the **Standard Monitoring Framework\All Business Services State View**

![All Business Services](./Screencaps/SCOM%20Task%20Deployment%20Example%20014.png)

Opening the Diagram View for the Business Service will show us the newly created monitoring objects as well as the relationships between existing objects and the new Business Service

![Business Services Diagram View](./Screencaps/SCOM%20Task%20Deployment%20Example%20015.png)

