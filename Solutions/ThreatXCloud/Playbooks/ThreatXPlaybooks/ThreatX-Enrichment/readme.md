# ThreatX-enrichment Info Playbook
 ## Summary
 When a new Azure Sentinel incident is created, this playbook gets triggered and performs below actions
 1. Fetches the list of Ip's from incident entites .
 2. Make the APi call to get the latest threat information/details from cloud console and update the same incidents comments with result.


### Prerequisites 
1. ThreatX-WAFCustomConnector needs to be deployed prior to the deployment of this playbook under the same subscription.
2. API key. To get API Key, login into your ThreatX cloud instance dashboard and navigate to Settings --> API Key --> Add API Key.

### Deployment instructions 
1. Deploy the playbook by clicking on "Deploy to Azure" button. This will take you to deploying an ARM Template wizard.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FSolutions%2FThreatXCloud%2FPlaybooks%2FThreatXPlaybooks%2FThreatX-encrichment%2Fazuredeploy.json)
[![Deploy to Azure Gov](https://aka.ms/deploytoazuregovbutton)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FSolutions%2FThreatXCloud%2FPlaybooks%2F%2FThreatXPlaybooks%2FThreatX-encrichment%2Fazuredeploy.json)

2. Fill in the required paramteres:
    * Playbook Name: Enter the playbook name here (Ex: ThreatX-enrichment)
    * Custom Connector Name: Enter the ThreatX custom connector name here (Ex: ThreatX-WAFCustomConnector)
    * Key vault name : Your key vault name where you want the secrets to be stored (api_key).
    * Threatx Key name : Name of your secret key 
    * Threatx Key : Your threatx secret api key 

### Post-Deployment instructions 
#### a. Authorize connections
Once deployment is complete, you will need to authorize each connection.
1.	Click the Azure Sentinel connection resource
2.	Click edit API connection
3.	Click Authorize
4.	Sign in
5.	Click Save
6.	Repeat steps for ThreatX Api  Connection (For authorizing the ThreatX API connection, API Key needs to be provided)

#### b. Configurations in Sentinel
1. In Azure sentinel analytical rules should be configured to trigger an incident with risky URL or IP Address. 
2. Configure the automation rules to trigger this playbook , mapping of IP and URL entities is necessary

#### c. Assign Playbook Microsoft Sentinel Responder Role
1. Select the Playbook (Logic App) resource
2. Click on Identity Blade
3. Choose Systen assigned tab
4. Click on Azure role assignments
5. Click on Add role assignments
6. Select Scope - Resource group
7. Select Subscription - where Playbook has been created
8. Select Resource group - where Playbook has been created
9. Select Role - Microsoft Sentinel Responder
10. Click Save (It takes 3-5 minutes to show the added role.)

#  References
 - [Threatx support documentation](https://support.threatx.com/hc)
