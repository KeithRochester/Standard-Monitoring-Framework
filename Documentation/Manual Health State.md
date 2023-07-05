# **Business Service and Business Service Component Manual Health State**

## Summary

Sometimes it is necessary to manually set the health state of a Business Service or a component of a Business Service. Typically, this happens when we become aware of a service impacting failure that is not yet being monitored by SCOM. In this situation it undermines confidence in monitoring having dashboards/reports displaying a healthy state. 
Business Services and components have a manual health state monitor targeted at them. The health state is updated using agent tasks. 
>Note it is not possible to set the state of a Business Service or a component to a healthier state than any objects it contains. For example, if a ping monitor is already setting the state of a component to warning we can’t manually set it to healthy. We can only set it to critical. 

## Scenario

We have been made aware of a service impacting issue with the WMS frontend servers that is not being detected by SCOM. We are going to set the status of the frontend servers component of the WMS Business Service to a critical state

## Goal

![Business Services Diagram View](./Screencaps/SCOM%20Manual%20Health%20State%20Example%20004.png)

## Steps

Start by navigating to a view that shows the frontend servers component. The easiest way to find the object is to use the diagram view for the Business Service. Click on the **SMF: Set Component State to Critical** task. 

![Business Services Diagram View](./Screencaps/SCOM%20Manual%20Health%20State%20Example%20001.png)

Override the message parameter with an appropriate message and click run. The message will be included in the health state change data and in the alert description (by default alerts are generated with the same severity as the monitor state. You can override the severity or if alerts are generated at all if needed).

![Manual Health State Task](./Screencaps/SCOM%20Manual%20Health%20State%20Example%20002.png)

The health state of the component and Business Service will be updated and an alert is generated (optional).

![Manual Health State Alert](./Screencaps/SCOM%20Manual%20Health%20State%20Example%20003.png)

![Business Services Diagram View](./Screencaps/SCOM%20Manual%20Health%20State%20Example%20004.png)

## Setting the Component Back to Healthy

Start by navigating to a view that shows the frontend servers component. The easiest way to find the object is to use the diagram view for the Business Service. Click on the **SMF: Set Component State to Healthy** task. 
![Business Services Diagram View](./Screencaps/SCOM%20Manual%20Health%20State%20Example%20005.png)

Override the message parameter with an appropriate message and click run. The message will be included in the health state change data.

![Manual Health State Task](./Screencaps/SCOM%20Manual%20Health%20State%20Example%20006.png)

The health state of the component and Business Service will be updated.
![Business Services Diagram View](./Screencaps/SCOM%20Manual%20Health%20State%20Example%20007.png)
