# SOC-training-Lab
SOC TRAINING LAB USING  MICROSOFT SENTINEL CLOUD SIEM

This is a mini Sentinel SIEM lab that is used to create a real world attack and how to remediate it. 

The first thing to do is to create an Azure free Account, then create a sentinel workspace while selecting your subscription and also giving your tenant’s name. 
 
<img width="351" alt="image" src="https://github.com/user-attachments/assets/72b55fe8-e5e8-4399-85f2-dae6ffc16816">

The picture above shows how to create the sentinel workspace, next is deployment of the workspace. 
<img width="442" alt="image" src="https://github.com/user-attachments/assets/3d9ed7b2-f785-4729-af2a-ee5f708de75a">

 
After deployment, Select the workspace created and click add to  the Microsoft sentinel workspace has been created and added. The next step is to deploy the sentinel training lab. Here I am using Microsoft ingested data from the lab to perform all the SOC training throughout the lab.

DEPLOYMENT OF SENTINEL TRAINING LAB SOLUTION

First, Navigate to Azure HOME and on the general search pane, search for Microsoft sentinel training lab, the click on create and choose the same Resource group we previously created and same sentinel workspace to integrate the training lab to my existing workspace. That can be seen on the picture below. 

 <img width="473" alt="image" src="https://github.com/user-attachments/assets/99ec7258-b842-4905-8bf0-3ee82f686687">


Once click Review + create the deployment starts and it can take almost 15 minutes 

 <img width="548" alt="image" src="https://github.com/user-attachments/assets/4804cdc2-578a-4d08-8457-fed08a5909dd">

Here we have succefully deployed the ingested data and our sentinel lab is good to go. 

 <img width="279" alt="image" src="https://github.com/user-attachments/assets/6176c982-3abe-4ab3-9b73-8bf8a1ee69a1">

Next step is to configure Microsoft Sentinel playbook to allow it to access sentinel .
•	Seletc the Resource group
•	Select the azuresentinel-Get-GeoFromIpAndTagIncident 
•	Select General settings, then click Edit API connection and then Authorize Microsoft playbook on sentinel by selecting account you deployed the sentinel, save the authorization and that is all.
 

<img width="522" alt="image" src="https://github.com/user-attachments/assets/396db592-ca7b-4db2-bf8d-5b89c244b141">


Data connectors in Microsoft sentinel
In this section, I will enable data connectors to ingest data that would be investigated in Microsoft sentinel. Firstly, I will configure/ enable Azure Activity Data connector 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/36dae3ad-82e6-4bf9-bed5-9eced5a5e870">

Launch the activity Log, from the connector or content hub if not already installed, click on it and launch Azure Policy Assignment wizard  to configure it very well. 
  <img width="457" alt="image" src="https://github.com/user-attachments/assets/5554d210-5c5c-4fa7-b36a-ae1c3b54667a">


Then Select your subscription and resource group on scope, check the parameters and select the workspace and configure the effect. Then create and the Activitiy is now integrated in your Microsoft sentinel.

 Let’s now connect Microsoft defender for Cloud to Microsoft Sentinel. 
From Connector Page, click on defender and select the subscription, then connect and the bidirectional connection of Azure defender has been connected. 
 
<img width="473" alt="image" src="https://github.com/user-attachments/assets/b0d4ac89-c833-42c9-b658-2041fd1001d9">

Threat intelligence connector using TAXII API is not currently working…. Will come back to it. 

**Analytic Rule **
This rule is known as security detection. It is used to detect what anomaly is happening in the sentinel.
Steps :
Navigate to Analytic rule. 
Select the template section and see all the templates used to detect security anomalies.
You can also search for rule type and view/ select the rule you want to apply

 <img width="489" alt="image" src="https://github.com/user-attachments/assets/147536c9-3f86-4ce8-9bb1-845841858c0b">

I can also create my own custom rule template to detect an attack.

1.	Click on create
2.	Select query rule
3.	The Mapping is refined based on your 

<img width="491" alt="image" src="https://github.com/user-attachments/assets/9452c464-d0f8-43ae-b1c8-d3279824229d">

 
The sample  query I created above is run every 5 hours(can be set to minutes) to detects successful logon events (EventID 4624) outside of regular business hours (before 9 AM or after 6 PM). It extracts the hour from the logon timestamp and filters events accordingly. The result shows the logon time, computer, account, IP address, and hour of the event for analysis.

In the automated response, select the action that will happen, either notify the SOC team or run an automated playbook that will disable the affected account or whatever automation you prefer to set up. 

Once created, you can search the rule in the add filter pane and you will see the template. 
 
<img width="233" alt="image" src="https://github.com/user-attachments/assets/addd9bfe-36f1-4296-ae62-6816aa8f258c">

You can also create Microsoft incident alert rule by just following these steps 

<img width="299" alt="image" src="https://github.com/user-attachments/assets/b5957756-761d-43f4-afbc-e1167207e3af">


 
 After adding the automated response, then click review and create. These are just samples of how incident rules are created and managed in Sentinel. 
 <img width="223" alt="image" src="https://github.com/user-attachments/assets/08668ff8-b250-4e62-bb56-3ec04f0eeb17">



Incident Investigation and Incident management 
How doe incident get investigate. After the Alerts has been generated, The SOC team or analyst can investigate the incident by going to the incident section  and selecting the incident to be investigated. I am going to investigate a sample incident below. 
1.	Select incident
2.	Click on the incident to be investigated 
<img width="259" alt="image" src="https://github.com/user-attachments/assets/9d555e5d-f2ec-431f-9883-1e51eb8abc07">

 

3.	Click on view full details to expand the incident
4.	Once opened, you can do the following 
a.	Assign incident to owner
b.	Change the status of the incident from either active/closed (after it has been investigated)
c.	Change the severity 
d.	Bookmark the incident for further reference 
e.	Investigate further 
f.	Opening the entities show whom the account is associated with in this incident is AdeleV@contoso.onMicrosoft.com. 
g.	Incident action is what to do to the affected account (disable by running playbook, create automation rule or even create team members to help investigate the incident).
 
<img width="468" alt="image" src="https://github.com/user-attachments/assets/0e7c6385-62c0-4c4f-9652-1b9432e2aee9">

Let us investigate further. 

Selecting the investigate, it will map the account compromised or entity compromised and we can see what is connected, whom the incident is assigned to and also more insight from the investigation.
 
<img width="468" alt="image" src="https://github.com/user-attachments/assets/32027472-5895-4466-b8d2-bd34870db796">

Once you click any of the geo IP data mapping, you can even dive dipper in running a playbook to remediate the account or select the account will give you full details of the account owner. After this, you can head back to the incident to update the status of the incident and document. 

Opening another incident that occurred multiple time can even show you more graphical evidence when accessing and looking at an incident. On the action beside the investigate, we can even add the incident to Threat intelligence.
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/71849a01-0086-486d-8beb-78aef890cbc6">

Simply clicking on alert will take you back to Log of where the incident originated and that would help and support in the investigation. It will help to check if the incident is correlated with other event.

 
<img width="400" alt="image" src="https://github.com/user-attachments/assets/ef042113-9a9c-4c60-b91a-206ba82c4849">


TAG
Also, you can add tag to the incident and know exactly where the incident is coming from, the region and know if you have to block the region it is coming from.

Threat Hunting 

Threat hunting is when you search for a specific event that was not probably captured or alerted. This can also been done on Sentinel. Assuming we want to investigate a solarigate threat which has been handed over to us by our threat research team. We can use this approach below to tackle it. 

•	Navigate to Hunting 
•	Search for solrigate or the name of the threat and run the queries if found. 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/87c1ed3e-21fa-477a-8784-eaca3213a3ad">


We can also add the solarigate query to a live stream to see how it is working and and see the affected computers. 
After we have run the solorigate inventory query, the result is showing three (3 )account in which the compromise affected 3 host. Expanding on the result will give us more details about the solrigate. 
 
<img width="468" alt="image" src="https://github.com/user-attachments/assets/bc899859-f089-4b7f-80f0-f9708dd484b5">

View result to see the affected Host and to bookmark it so we can see it in the hunting page where we will either assign to SOC team or anaylst. 
 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/e18c8dd1-582c-4d85-b6e1-5d7113c2d2fb">

Click on Add to bookmark and give the necessary name you would remember or like to call it. After that, create the bookmark. 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/8cf35e9d-715a-4702-8d0e-468a19246a06">


From the Hunting page, go to Bookmark, check the threat/host you bookmarked and the click to either add it to existing incident or a new incident where you will assign it to a SOC analyst or Security analyst for further Actions by either isolating the host or anything else to contain it.  
<img width="468" alt="image" src="https://github.com/user-attachments/assets/73e51ab7-9c4c-47e1-946f-2627c4ee346b">

 
Here we have seen the bookmarked threat and the next is to create an incident using the threat and assign it to a SOC analyst team that will take care of it.
 
<img width="231" alt="image" src="https://github.com/user-attachments/assets/e041212e-756a-4988-8d41-2f15383f14ac">


Adding Indicator of Compromise IOC
After our investigation, we might want to add the ip address to threat intelligence as indicator of compromise. Then, when the IP I seen, it can be flagged malicious.
This can be done in different way but navigating to the incident we created above from the Threat hunting, then right click on the ip address of the host and add to TI. 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/2bf7b06c-a7fe-47ca-b33d-52f7c9382509">


Proactive Hunting process MITRE Attack
I am using a MITRE attack T1098 attack from the MITRE website. In this threat hunting, I am going to hunt for that specific threat assuming it was announced, and we got the intel from a MITRE website or blog release. To hunt for it follow the steps:

•	Navigate Hunting page, 
•	Click on filter and select tecniques then check T1098( account manipulation)
 
<img width="468" alt="image" src="https://github.com/user-attachments/assets/a03047a7-6548-4fa4-b092-96ae81c29ed3">

Once applied, then check all the query, click on the run selected query and wait to see if it comes with any result. 
 
<img width="468" alt="image" src="https://github.com/user-attachments/assets/cc78540d-8ea5-4d39-90d5-3c8b93c96d51">

After the running of the selected query, we found out there are 5 result on  Adding credentials to legitimate account. From there, we can then expand it and view the result. From the result, you can bookmark it so that we will upgrade it to an incident and assign to an analyst that will take a very good look at it. 

Click the view result and run the query to give you all the account and event that has the particular threat we are hunting. From there, you can bookmark it and upgrade it to an incident just the same way we did in the above threat hunting documentation. 
 
<img width="468" alt="image" src="https://github.com/user-attachments/assets/3ea78906-8bb5-4324-8b97-acd903f768cd">

Expanding one of the Host will even give you more details about the account manipulation and which account you need to actually investigate directly.  
 
<img width="468" alt="image" src="https://github.com/user-attachments/assets/acf999bb-f3c0-4531-9f35-f48dcca5c4e1">

When navigate to the bookmark, then you will see all the bookmarked threat and you can then upgrade it to incident.
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/6e646a6f-6b35-4026-9bf5-e8a671bfa49b">


WATCHLIST

Next is Adding a watch list: Assuming the CIO notified you that there will be a penetration testing on the network of your organization and provided the Ip address of the tools that would be used to conduct the test in a CSV file, how do you keep an eye on it. You can create a watchlist that will help you in checking and monitoring the activities that is happening particularly by that IP address in order not to raise false alarm. 

Steps 
1.	Select watchlist 
2.	Select Network Addresses 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/0930d618-1c18-4e6b-afa5-07bd0fa44288">

3.	Create from Template and Now import the IP address 

 <img width="327" alt="image" src="https://github.com/user-attachments/assets/d8ef870f-b35b-4a18-91c6-230613f6b9ec">


Next, go to Watchlist and see the added watchlist from where you can watch the Logs for the IP. 
 <img width="272" alt="image" src="https://github.com/user-attachments/assets/98545968-c3cf-4668-9d27-22289cd812d6">

