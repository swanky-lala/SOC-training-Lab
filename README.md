# SOC-training-Lab
**SOC TRAINING LAB USING  MICROSOFT SENTINEL CLOUD SIEM**

**This mini-lab helps create a real-world attack scenario and remediation, Threat management, Threat hunting, Incidence response using Microsoft Sentinel SIEM.** 

**Setting Up Microsoft Sentinel Workspace**

The first thing to do is to create an Azure free Account, then create a sentinel workspace while selecting your subscription and also giving your tenant’s name. 
 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/b4b77710-dd94-4087-b90c-82fb2ff5a1a5">


The picture above shows how to create the sentinel workspace, next is deployment of the workspace. 

**Deploy the Sentinel Workspace**
   
<img width="826" alt="image" src="https://github.com/user-attachments/assets/4b48e1b3-bbba-4eb1-b92f-0bad4a0d9ec1">

 
After deployment, Select the workspace created and click add to  the Microsoft sentinel workspace has been created and added. The next step is to deploy the sentinel training lab. Here I am using Microsoft ingested data from the lab to perform all the SOC training throughout the lab.

**DEPLOYMENT OF SENTINEL TRAINING LAB SOLUTION**

First, Navigate to Azure HOME and on the general search pane, search for Microsoft sentinel training lab, then click on create and choose the same Resource group we previously created and same sentinel workspace to integrate the training lab to my existing workspace. That can be seen on the picture below. 

 <img width="826" alt="image" src="https://github.com/user-attachments/assets/61deb1ab-0947-46ab-a621-972c5ffe7165">

Once click Review + create the deployment starts and it can take almost 15 minutes 

 <img width="826" alt="image" src="https://github.com/user-attachments/assets/2715484c-fc9a-495e-81b3-413e79c908d0">

Here we have succefully deployed the ingested data and our sentinel lab is good to go. 

<img width="826" alt="image" src="https://github.com/user-attachments/assets/4eb2a4c9-7550-4d08-be52-13cd869252ca">

**Configuring Microsoft Sentinel Playbooks**

Next step is to configure Microsoft Sentinel playbook to allow it to access sentinel .
•	Seletc the Resource group
•	Select the azuresentinel-Get-GeoFromIpAndTagIncident 
•	Select General settings, then click Edit API connection and then Authorize Microsoft playbook on sentinel by selecting account you deployed the sentinel, save the authorization and that is all.
 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/1335b613-2e8c-4d14-b4e5-8668d1b0c9e4">

**Data connectors in Microsoft sentinel**

In this section, I will enable data connectors to ingest data that would be investigated in Microsoft sentinel. Firstly, I will configure/ enable Azure Activity Data connector 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/41c8227a-96c9-4e99-b7ed-179226909215">

Launch the activity Log, from the connector or content hub if not already installed, click on it and launch Azure Policy Assignment wizard  to configure it very well. 

<img width="826" alt="image" src="https://github.com/user-attachments/assets/1ea0d90a-6dba-4307-9b0d-a36563208b2b">

Then Select your subscription and resource group on scope, check the parameters and select the workspace and configure the effect. Then create and the Activitiy is now integrated in your Microsoft sentinel.

**Coonecting MS Defender**

 Let’s now connect Microsoft defender for Cloud to Microsoft Sentinel. 
From Connector Page, click on defender and select the subscription, then connect and the bidirectional connection of Azure defender has been connected. 
 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/bb6f200a-87d4-4344-bfed-848ce20b3314">

Threat intelligence connector using TAXII API is not currently working…. Will come back to it. 

**Analytics Rules for Anomaly Detection**

This rule is known as security detection rule for anomalies detecion. It is used to detect what anomaly is happening in the sentinel.
Steps :
1. Navigate to Analytic rule. 
2. Select the template section and see all the templates used to detect security anomalies.
You can also search for rule type and view/ select the rule you want to apply

<img width="826" alt="image" src="https://github.com/user-attachments/assets/eec5a832-c458-4129-ae24-5426eb3915ad">

**Custom Reule creation**
I can also create my own custom rule template to detect an attack.

1.	Click on create
2.	Select query rule
3.	The Mapping is refined based on the IP or resources you are using to create the rule

<img width="826" alt="image" src="https://github.com/user-attachments/assets/f4a2ee17-34e3-4ce2-8977-449b2535c680">

The sample  query I created above is run every 5 hours(can be set to minutes) to detects successful logon events (EventID 4624) outside of regular business hours (before 9 AM or after 6 PM). It extracts the hour from the logon timestamp and filters events accordingly. The result shows the logon time, computer, account, IP address, and hour of the event for analysis.

In the automated response, select the action that will happen, either notify the SOC team or run an automated playbook that will disable the affected account or whatever automation you prefer to set up. 

Once created, you can search the rule in the add filter pane and you will see the template. 
 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/999b335d-0595-426a-9cc5-b8c7efea9854">

You can also create Microsoft incident alert rule by just following these steps 

<img width="826" alt="image" src="https://github.com/user-attachments/assets/3678e6ac-3c67-49ba-b6a5-eb5c7e6e12e0">

 After adding the automated response, then click review and create. These are just samples of how incident rules are created and managed in Sentinel. 

<img width="826" alt="image" src="https://github.com/user-attachments/assets/9fac4498-caad-4f24-807c-69fff8d30ce6">

**Incident Investigation & Management**

How doe incident get investigate. After the Alerts has been generated, The SOC team or analyst can investigate the incident by going to the incident section  and selecting the incident to be investigated. I am going to investigate a sample incident below. 
1.	Select incident
2.	Click on the incident to be investigated
   
<img width="826" alt="image" src="https://github.com/user-attachments/assets/b6da016b-5ff3-4689-a7d1-5c003cc5bdad">

4.	Click on view full details to expand the incident
5.	Once opened, you can do the following 
a.	Assign incident to owner
b.	Change the status of the incident from either active/closed (after it has been investigated)
c.	Change the severity 
d.	Bookmark the incident for further reference 
e.	Investigate further 
f.	Opening the entities show whom the account is associated with in this incident is AdeleV@contoso.onMicrosoft.com. 
g.	Incident action is what to do to the affected account (disable by running playbook, create automation rule or even create team members to help investigate the incident).
 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/b10b09f6-a1a9-4486-8434-8458d9a954ee">

Let us investigate further. 

Selecting the investigate, it will map the account compromised or entity compromised and we can see what is connected, whom the incident is assigned to and also more insight from the investigation.
 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/b4134ce8-4831-4ac4-8d74-e9cb4ef8f131">

Once you click any of the geo IP data mapping, you can even dive dipper in running a playbook to remediate the account or select the account will give you full details of the account owner. After this, you can head back to the incident to update the status of the incident and document. 

Opening another incident that occurred multiple time can even show you more graphical evidence when accessing and looking at an incident. On the action beside the investigate, we can even add the incident to Threat intelligence.

<img width="826" alt="image" src="https://github.com/user-attachments/assets/aba0e851-56a8-4e62-80ea-ade901d30a73">

Simply clicking on alert will take you back to Log of where the incident originated and that would help and support in the investigation. It will help to check if the incident is correlated with other event.

<img width="826" alt="image" src="https://github.com/user-attachments/assets/a45c3fcf-fc5c-4414-b88d-16431fc3475e">

TAG
Also, you can add tag to the incident and know exactly where the incident is coming from, the region and know if you have to block the region it is coming from.

**Threat Hunting & MITRE Attack Process**

Threat hunting is when you search for a specific event that was not probably captured or alerted. This can also been done on Sentinel. Assuming we want to investigate a solarigate threat which has been handed over to us by our threat research team. We can use this approach below to tackle it. 

•	Navigate to Hunting 
•	Search for solrigate or the name of the threat and run the queries if found. 

<img width="826" alt="image" src="https://github.com/user-attachments/assets/f3f98b21-4bbb-4665-b255-b2b3f0308ef5">

We can also add the solarigate query to a live stream to see how it is working and and see the affected computers. 
After we have run the solorigate inventory query, the result is showing three (3 )account in which the compromise affected 3 host. Expanding on the result will give us more details about the solrigate. 
 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/d000f5ba-0b04-4656-b643-bb97a3aa8c00">

View result to see the affected Host and to bookmark it so we can see it in the hunting page where we will either assign to SOC team or anaylst. 
 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/67eadaad-0b7b-49b9-98b0-486632f1327f">

Click on Add to bookmark and give the necessary name you would remember or like to call it. After that, create the bookmark. 

<img width="826" alt="image" src="https://github.com/user-attachments/assets/47d61f28-1983-4d9a-b2db-701e17a47d48">

From the Hunting page, go to Bookmark, check the threat/host you bookmarked and the click to either add it to existing incident or a new incident where you will assign it to a SOC analyst or Security analyst for further Actions by either isolating the host or anything else to contain it.  

<img width="826" alt="image" src="https://github.com/user-attachments/assets/8f584e19-a7b6-4dc0-89c3-ecad13bcdd2d">

Here we have seen the bookmarked threat and the next is to create an incident using the threat and assign it to a SOC analyst team that will take care of it.
 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/16b0903b-f647-420d-bf71-7d2906434799">

Adding Indicator of Compromise IOC
After our investigation, we might want to add the ip address to threat intelligence as indicator of compromise. Then, when the IP I seen, it can be flagged malicious.
This can be done in different way but navigating to the incident we created above from the Threat hunting, then right click on the ip address of the host and add to TI. 
 
<img width="821" alt="image" src="https://github.com/user-attachments/assets/d8ba00f9-0971-4044-beab-a02eb5c477c0">

**Proactive Hunting process MITRE Attack**
I am using a MITRE attack T1098 attack from the MITRE website. In this threat hunting, I am going to hunt for that specific threat assuming it was announced or given to me by the CISO,or we got the intel from a MITRE website or blog release. To hunt for it follow the steps:

•	Navigate Hunting page, 
•	Click on filter and select tecniques then check T1098( account manipulation)
 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/e80b432d-7326-4b51-92cc-e3946e02643a">

Once applied, then check all the query, click on the run selected query and wait to see if it comes with any result. 
 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/54600a5f-6237-4824-b056-5023610c030d">

After the running of the selected query, we found out there are 5 result on  Adding credentials to legitimate account. From there, we can then expand it and view the result. From the result, you can bookmark it so that we will upgrade it to an incident and assign to an analyst that will take a very good look at it. 

Click the view result and run the query to give you all the account and event that has the particular threat we are hunting. From there, you can bookmark it and upgrade it to an incident just the same way we did in the above threat hunting documentation. 
 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/f8466ddc-535d-4664-a74f-383a3694746f">

Expanding one of the Host will even give you more details about the account manipulation and which account you need to actually investigate directly.  
 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/e6a12e98-06b1-476b-b616-b38c2f7f6a66">

When navigate to the bookmark, then you will see all the bookmarked threat and you can then upgrade it to incident.

<img width="826" alt="image" src="https://github.com/user-attachments/assets/23d3502a-9322-408e-9693-5bb89db63cc7">

**WATCHLIST**

Next is Adding a watch list: Assuming the CIO notified you that there will be a penetration testing on the network of your organization and provided the Ip address of the tools that would be used to conduct the test in a CSV file, how do you keep an eye on it. You can create a watchlist that will help you in checking and monitoring the activities that is happening particularly by that IP address in order not to raise false alarm. 

Steps 
1.	Select watchlist 
2.	Select Network Addresses 

<img width="826" alt="image" src="https://github.com/user-attachments/assets/d7dff24b-1142-42b5-a1f2-51285cfc5fbd">

3.	Create from Template and Now import the IP address 

<img width="826" alt="image" src="https://github.com/user-attachments/assets/71b1f83f-91fc-466f-b595-1794411bacfe">

Next, go to MyWatchlist and see the added watchlist from where you can watch the Logs for the IP. 
<img width="826" alt="image" src="https://github.com/user-attachments/assets/55cf2d45-a73d-43e6-b24f-3fa3afe32f35">


