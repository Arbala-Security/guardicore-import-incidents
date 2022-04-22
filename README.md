# Integrating Guardicore Incidents into Azure Sentinel 

Author: Accelerynt

For any technical questions, please contact info@accelerynt.com

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAccelerynt-Security%2FGuardicore-Import-Incidents%2Fmaster%2Fazuredeploy.json)
[![Deploy to Azure Gov](https://aka.ms/deploytoazuregovbutton)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAccelerynt-Security%2FGuardicore-Import-Incidents%2Fmaster%2Fazuredeploy.json)      

This playbook will give Microsoft Sentinel the ability to query your Guardicore Centra Cloud instance API to retrieve established incidents. The API query will be sent every 10 minutes. Incidents that have had their data copied to Microsoft Sentinel logs will be marked with the “Sentinel” tag in Guardicore. 

                                    
#
### Requirements

You will need the following items to enter in the playbook settings during deployment: 

* URL for your Guardicore instance. 

* A Username/Password that is a Local Administrator in your Guardicore environment. 

* The Azure Sentinel Workspace ID where you want the incidents logged. 

* The Primary or Secondary Key to your workspace. 

# 
### Setup

To retrieve the Guardicore instance URL needed for the deployment of this playbook, log into your account. Take note of the url, which will look like **https://cus-0000.cloud.guardicore.com** , where 0000 is your 4 digit customer number.

![GCURL](Images/GCURL.png)

#
### Deployment                                                                                                         
                                                                                                        
To configure and deploy this playbook:

Open your browser and ensure you are logged into your Azure Sentinel workspace. In separate tab, open the link to our playbook on the Arbala Security GitHub Repository:

https://github.com/Accelerynt-Security/Guardicore-Import-Incidents

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAccelerynt-Security%2FGuardicore-Import-Incidents%2Fmaster%2Fazuredeploy.json)
[![Deploy to Azure Gov](https://aka.ms/deploytoazuregovbutton)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAccelerynt-Security%2FGuardicore-Import-Incidents%2Fmaster%2Fazuredeploy.json)      

Click the “**Deploy to Azure**” button at the bottom and it will bring you to the custom deployment template.

In the **Project Details** section:

* Select the “**Subscription**” and “**Resource Group**” from the dropdown boxes you would like the playbook deployed to.  

In the **Instance Details** section:  

* **Playbook Name**: This can be left as “Guardicore-Import-Incidents” or you may change it.  

* **GCURL**: Enter your Guardicore tenant URL here. It must look like thr following: **https://cus-0000.cloud.guardicore.com** 

Please ensure there is no **/** after the .com. 


* **GC Username**: Replace text with username of the Guardicore Admin account you want to use. 

* **GC Password**: Replace text with password of the Guardicore Admin account you want to use. 

Towards the bottom, click on “**Review + create**”. 

![template](Images/template.png)

Once the resources have validated, click on "**Create**".

The resources should take around a minute to deploy. Once the deployment is complete, you can expand the "**Deployment details**" section to view them.
Click the one corresponding to the Logic App.

![playbookclick](Images/playbookclick.png)

Click on the “**Edit**” button. This will bring us into the Logic Apps Designer.

![editbutton](Images/editbutton.png)

Click on the bottom bar labeled “**For each Guardicore incident**”. 

![Logicapp1](Images/Logicapp1.png)

Click on the bar labeled “**If no Sentinel tag was found**”. 

![Logicapp2](Images/Logicapp2.png)

Click on “**Connections**”. This uses a connection created during the deployment of this playbook. Before the playbook can be run, this connection will either need to be authorized in this step, or an existing authorized connection may be alternatively selected.

![Logicapp3](Images/Logicapp3.png)

To validate the connection created for this playbook, expand the "**Connections**" step and click the exclamation point icon next to the name matching the playbook.

![Logicapp4](Images/Logicapp4.png)

In the **Connection Name** put GCIncidents. The next fields are **Workspace Key** (Primary or Secondary Key) and **Workspace ID**. Follow the instructions at the bottom of this page to find those values. Once you have them, copy and paste them into their respective fields. Now click the update button.  

![Logicapp5](Images/Logicapp5.png)

You should see the that the “Send Data” box has updated and displays “Connected to GCIncidents.” Click the X to close the Logic App Designer. There is no need to click a save button.  

![Logicapp6](Images/Logicapp6.png)

Depending on how many and how frequently you have incidents created in Guardicore, it could take a few minutes or several hours for the logs to show up Sentinel. You can view the incident logs by returning to your Azure Sentinel workspace and clicking on “Logs.” You should have a new custom log called “GCIncidents_CL” – type that into your query window and click run. Adjust the time range, as necessary. Each line returned contains the details for each individual incident returned from the Guardicore API. 

![final](Images/final.png)

## Finding your Azure Sentinel Workspace ID and Primary/Secondary Key 

To find your Workspace ID and Primary/Secondary key, start by clicking on “Settings” from the Azure Sentinel workspace you want the incidents sent to. Then click on “Workspace Settings” under the Azure Search Bar. 

![settings1](Images/settings1.png)

Click on “Advanced Settings”. 

![settings2](Images/settings2.png)


Next, click on “Connected Sources” and then “Windows Servers” to display your Workspace ID and either Primary or Secondary key. 

![settings3](Images/settings3.png)

For any technical questions, please contact info@arbalasystems.com.
