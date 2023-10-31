# Blitz3
During the US holidays, the URL Shortener is expected to receive unexpected traffic spikes between 900 - 1,000 requests per second. The URL Shortener can handle a maximum of 700 requests per second on a single T.2 micro. There are 12 government-recognized holidays in a year. What can be added to the infrastructure to handle the 900 - 1,000 unexpected requests per second? 

In this Blitz, we deployed the URL shortener application from deployment 2 (https://github.com/Sameen-k/Deployment2.git).
The deployment folder was downloaded to the local machine and rezipped then uploaded to AWS when deploying on Elastic Beanstalk. 

## Blitz
A quality assurance engineer blitzes the infrastructure of deployment 2 with 700 requests using JMeter which are all successful
However when the engineer blitzes with 1,000 requests the infrastructure could not successfully handle every single request. So for instances like these where there may be an influx of requests due to a holiday or event, it's important to have countermeasures prepared to handle the increased load.

## Configuring an Auto-Scaling Group
An auto-scaling group is a feature that can be added to an infrastructure to improve resiliency through redundancy/scaling. Elastic Beanstalk can deploy an additional application environment when requests hit a certain threshold. In this case, the lower threshold was set to 600 and the upper threshold was set to 700. Once the number of requests made to the application exceeds 700, the auto-scaling group will launch another application instance. The same goes for when the number of requests falls below the threshold of 600, the auto-scaling group will then deactivate the second application instance.

## Optimization:
There are many additional configurations of an auto-scaling group that can be implemented based on need. In this case, the creation of an additional instance depends on the number of requests, however, it's important to note that the auto-scaling group takes some time to launch a second instance. This implies that a great increase in requests, while the second application instance is still launching, can cause user requests to time out before it's fully deployed. 
Considering that increased request loads that may happen during holidays and events are generally predictable there are auto-scaling policies that can be added to configurations to prevent this from happening. There are also auto-scaling schedules that can be implemented for specific times when there is a known increase of traffic.

## Diagram
![Blitz3 drawio (2)](https://github.com/Sameen-k/Blitz3/assets/128739962/4b12da7a-be6b-47f1-ab06-f8a9a08e8cc6)

