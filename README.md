# Reference architecture for setting up monitoring on AWS Site-To-Site VPN connection

The solution creats a monitoring setup for your AWS Site-To-Site VPN connection and helps diagnose AWS Site - to - Site VPN issues by notifying you when an error occurs in your VPN and is logged to designated CloudWatch log group. 

You can read the Blog: Setting up of AWS Site-to-Site VPN automated monitoring solution for deployment steps and more information
## Table of Content

1. [Overview](#overview-required)
2. [Prerequisites](#prerequisites-required)
3. [Deployment Steps](#deployment-steps-required)
4. [Cleanup](#cleanup-required)


## Overview

 The solution sends a notification whenever an error is found in CloudWatch log group of your VPN along with a resolution recommendation. The notification has resolution steps that you can perform to rectify the errors. This solution creates a subscription filter on your CloudWatch log group and subscribes a Lambda function to it. The subscription filter has filter pattern to errors mentioned in https://docs.aws.amazon.com/vpn/latest/s2svpn/log-contents.html You need to have CloudWatch logging enabled on your VPN connection before you run this automation. If there are other VPN connetions also logging to the same log group you mentioned in parameter of this automation then, those VPN Connections will be automatically monitored.  The automation notifies the error as soon as the mentioned error is discovered in VPN CloudWatch log group. The VPN errors can come periodically untill they are rectified, you can specify "NotificationFrequency" parameter to get notified at a frequency of your choice untill the error is fixed by user. 
  Please refer below links for pricing related to resources : 
1) Lambda pricing : https://aws.amazon.com/lambda/pricing/
2) CloudWatch pricing :  https://aws.amazon.com/cloudwatch/pricing/ 
3) DynamoDB pricing : https://aws.amazon.com/dynamodb/pricing/

![](/resources/setup-vpn-monitoring-architecture-diagram.jpg)

## Prerequisites

AWS Site-To-Site VPN Connection must have logging enabled on it. 
Enable Site-To-Site VPN Logs : https://docs.aws.amazon.com/vpn/latest/s2svpn/monitoring-logs.html#enable-logs

## Deployment Steps

1. Download [vpn-tunnel-monitoring.yaml](templates/vpn-tunnel-monitoring.yaml) AWS CloudFormation template from the source folder or clone the repo using the command: 


2. Sign in AWS Console and open [CloudFormation console](https://us-east-1.console.aws.amazon.com/cloudformation/home)

3. Select “Create Stack” and then select “With new resources (standard)”

4. In the “Specify template” option, select “Upload a template file”. Select “Choose file” and select the above saved CloudFormation template.

5. Give the stack a name, for example: VPN monitoring on CloudWatch log group \<CloudWatch log group name\>. Select “Next” until the confirmation page.

6. **Acknowledge** the checkbox in bottom left. And Click Submit

7. Wait for the stack to complete its deployment. It will take a few minutes.




## Cleanup

- Delete the AWS CloudFormation Stack deployed, and all the resources will be deleted.

## Notices

*Customers are responsible for making their own independent assessment of the information in this Guidance. This Guidance: (a) is for informational purposes only, (b) represents AWS current product offerings and practices, which are subject to change without notice, and (c) does not create any commitments or assurances from AWS and its affiliates, suppliers or licensors. AWS products or services are provided “as is” without warranties, representations, or conditions of any kind, whether express or implied. AWS responsibilities and liabilities to its customers are controlled by AWS agreements, and this Guidance is not part of, nor does it modify, any agreement between AWS and its customers.*


