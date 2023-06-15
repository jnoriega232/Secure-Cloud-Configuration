# Securing The Cloud Configuration

## We will mitigate risks by focusing on the following areas: 

<div>

### Objectives: 

- Regulatory Compliance (NIST 800-53, PCI DSS, CIS) and MDC Recommendations

- Azure Private Link & Firewall for Resources

- Run SECURE Environment for 24 Hours and Capture Analytics

### Environments and Technologies Used:

- Microsoft Azure
- Microsoft Sentinel
- Microsoft Cloud Defender

### Operating Systems Used:

- VM Windows 10 PRO (21H2)
- VM Linux Ubuntu 20.12

We still have a major problem with  Malicious NSG Inbound Flow. Now we will increase our hardening methodology and observe the changes in 24 hours. 

#### Regulatory Compliance (NIST 800-53, PCI DSS, CIS) and MDC Recommendations 
<details close>

<div>

</summary>

Reminder: Check your Subscription’s Cost Analysis

#### Regulatory Compliance (NIST 800-53, PCI DSS, CIS) and MDC Recommendations

### Actions and Observations<b>

- Presently, the situation can be described as follows: 

<p align="center">
<img src="https://i.imgur.com/ovREihI.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

- Navigate to the "Recommendations" section and strive to achieve a secure score of 100%

<p align="center">
<img src="https://i.imgur.com/9wCQsQL.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

- Currently, my secure score is at 65%. Follow the recommended remediation steps provided by Azure to improve the score. 

- I will commence by implementing advanced DDos protection measures, while exercising discretion in revealing all details. Nonetheless, please take your time as Azure effortlessly guides you to the comprehensive spectrum of resources. 

<p align="center">
<img src="https://i.imgur.com/9YMSB33.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

<p align="center">
<img src="https://i.imgur.com/IGI5X3q.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

- In our upcoming laboratory session, we will thoroughly delve into crucial recommendations for fortifying our environment's security. Additionally, an upcoming project will exemplify the attainment of a near-perfect or 100% score. A thought-provoking query will be posed: "Is having a lab that achieves 100% security the ultimate security measure?"

- Let us now step into the conclusive phase of the Cloud SOC Projects.

<details close>

<div>

</summary>

### Azure Private Link & Firewall for Resources

![image](https://user-images.githubusercontent.com/109401839/235408787-7acc45e8-904f-4bfb-b4ec-7c6668f4453f.png)

### Goals for this lab:

- Conduct a comprehensive assessment of MDC Regulatory Compliance, ensuring both its availability and successful implementation.
- NIST 800-53 (Ref)
- We will proceed with the implementation of SC-7.

1. Establish Azure Private Link and Firewall configurations for your Azure Key Vault Instance.
> Please ensure that you utilize the identical region and Virtual Network (VNet) as the remaining virtual machines (VMs) in your environment. 

<p align="center">
<img src="https://i.imgur.com/woYCdmV.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

1a. Within the Firewalls settings, we will deactivate public access. 
> Enable the exemption of trusted Microsoft services from this firewall's restrictions. 

- When you enable the Key Vault Firewall, you will have the option to permit trusted Microsoft services to bypass it. However, it is important to note that the trusted services list does not encompass every Azure service. For instance, Azure DevOps is not included in the trusted services list. This does not imply that services outside the trusted services list are untrusted or insecure. The trusted services list specifically includes services where Microsoft has full control over the code running on those services. Since users can write custom code in Azure services like Azure DevOps, Microsoft does not offer a blanket approval option for such services. Moreover, the inclusion of a service in the trusted services list does not guarantee its applicability in all scenarios.

1b. Set up the configuration for Private Endpoint connections.

- We will proceed with the creation of a private endpoint for our Azure Key Vault, following the steps outlined below.

<p align="center">
<img src="https://i.imgur.com/lpmq6cc.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

<p align="center">
<img src="https://i.imgur.com/DaMlUur.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

<p align="center">
<img src="https://i.imgur.com/xmtzXNq.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

<p align="center">
<img src="https://i.imgur.com/aSBARrS.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

<p align="center">
<img src="https://i.imgur.com/GUClCiI.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>
	
2. Set up the configuration of Azure Private Link and Firewall for your instance of Azure Storage Account.

2a. Deactivate public access and configure the endpoint for your Azure Storage Account instance. Repeat the aforementioned steps. 

<p align="center">
<img src="https://i.imgur.com/Q3w7BQ2.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

<p align="center">
<img src="https://i.imgur.com/CCxbRzb.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

2b. This process involves adjusting settings both in the network tab and the Settings -> Configuration section, specifically by disabling the "Allow Blob public access" option.

<p align="center">
<img src="https://i.imgur.com/SLQ6j4D.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

> The DNS system will allocate a private IP address, and all resources will be resolved to this specific IP.

3. Engage in the observation of Network Watcher Topology.

<p align="center">
<img src="https://i.imgur.com/e9q43EV.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

4. Examine the topology to observe the presence of private endpoints for both the Key Vault and Storage Account.

5. Access the "windows-vm" and verify the IP addresses assigned to your Key Vault and Storage Account instances.

5a. My keyvault address, ```akv-cyber-lab02.vault.azure.net``` 

<p align="center">
<img src="https://i.imgur.com/dEw0a3e.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

- We can observe that the resolution is occurring successfully with a private IP address, indicating that our endpoint is functioning properly. This validation is not solely based on the IP address itself, but rather on the fact that it resolves to a private IP address within our designated subnet range. In the event that the resolution was not successful, we would need to troubleshoot the issue.

- Now, let's attempt the same procedure on our own host computer instead of the virtual machines. 

<p align="center">
<img src="https://i.imgur.com/7x5XG7G.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

- We can successfully resolve it, revealing a public IP address; however, it is imperative to note that we do not possess accessibility to it. This distinction carries significant weight as my home computer is not connected to the Virtual Network (VNET) where the keyvault is situated. 

5b. The address of the storage account is represented as , ```https://sacyberlabb01.blob.core.windows.net/``` which is derived from the Blob service. As you may recall, we recently disabled this access to sever the connection between our services and the public web.

<p align="center">
<img src="https://i.imgur.com/NhX8NjS.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

- Let's carry out this process on our host computer:

<p align="center">
<img src="https://i.imgur.com/1v9UZyE.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

- Now, let's verify the functionality of the endpoint by executing this on the Azure computer:

<p align="center">
<img src="https://i.imgur.com/O0x3eaf.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p

- Within our virtual machine (VM), we can observe that it resolves to a private IP address, indicating that it is in the same Virtual Network (VNet) as our storage account and private endpoint.

6. Generate a Network Security Group (NSG) and associate it with the respective subnet.

- After successfully creating the Network Security Group (NSG) – I designated mine as nsg-subnet – navigate to the Virtual Networks section, access the desired Virtual Network (VNet), proceed to the Subnets tab, select the default subnet, and then add the NSG-Subnet to the NSG configuration. Remember to save the changes. 

 <p align="center">
<img src="https://i.imgur.com/Omlab24.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>
<p align="center">
<img src="https://i.imgur.com/LqGpxfo.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

6a. Let us revisit the Network Watcher Topology for a comprehensive review.

<p align="center">
<img src="https://i.imgur.com/kLzbaPe.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p

7. NIST 800-53: SC-7 [Boundary Protection] 

- By accomplishing the aforementioned steps, we have successfully fulfilled a significant portion of NIST 800-53: SC-7 [Boundary Protection] requirements. As a result, our Secure Score has escalated from 65% to 75%.

![vivaldi_kFYxmPzqwK](https://user-images.githubusercontent.com/109401839/235415879-fe17a567-1987-4afa-ad16-b4da996d0303.png)

- Please be aware that certain updates in Azure may take a few moments to reflect. To verify the status of everything, including regulatory compliance, navigate to the Regulatory Compliance section of Defender for Cloud. This will provide an overview of the current status. 

![vivaldi_gPgHNLFsaR](https://user-images.githubusercontent.com/109401839/235416092-7e1021be-6600-4fa7-8b6f-b6fc62b36858.png)

- Considering that everything is functioning as expected, there is no immediate cause for concern. However, please note that updates may take a short while to fully propagate. Now, let's allow a 24-hour timeframe to elapse in order to capture the relevant statistics. 

### Troubleshooting Approaches:

> If the displayed IP addresses are of a private nature, it indicates that the resources have likely been effectively integrated into a private Virtual Network (VNet).

> Conversely, the presence of a public IP address suggests that either the propagation process is still underway or there is a configuration discrepancy.

> Potential underlying causes for this situation could include the presence of resources and virtual machines (VMs) in separate Virtual Networks or encountering misconfigurations within the environment.

> Rest assured that for the remainder of the lab, resolving this particular issue is not imperative, as our primary objective is to secure the overall environment.

> However, if you are inclined to address the matter, you can consider attempting to delete and recreate the Private Endpoints or adjust related configurations to establish a fresh setup.

<details close>

<div>

</summary>

<div>

### Run SECURE Environment for 24 Hours and Capture Analytics

After 24 Hours of Locking - Down Environment: 

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 0 (-100%)
| Syslog                   | 0 (-100%)
| SecurityAlert            | 0 (-100%)
| SecurityIncident         | 0 (-100%)
| AzureNetworkAnalytics_CL | 0 (-100%)

![vivaldi_2ebSstcfdc](https://user-images.githubusercontent.com/109401839/235537587-a0c39f9c-3bea-4859-a736-80899a8ae56c.png)

![Linux SSH Auth Failure](https://user-images.githubusercontent.com/109401839/235539282-d6f0bfa4-0514-4288-b358-7ffa241b8f04.png)

![MySQL Authentication Failures](https://user-images.githubusercontent.com/109401839/235539283-b15bec27-f34e-405a-83f6-e4fa3ca38fd9.png)

![nsg-malicious-allowed-in](https://user-images.githubusercontent.com/109401839/235552956-1a1f4144-27a7-426a-bc1a-2970a6852d36.png)

![Windows RDP   SMB Authentication Failure](https://user-images.githubusercontent.com/109401839/235539287-8d7d8428-1d08-4ea4-8da0-fa8770a54aa3.png)

![vivaldi_IrVtpebi10](https://user-images.githubusercontent.com/109401839/235539351-10369664-4b30-4b7a-a220-00bdb7f83596.png)

<div>

Well, this series of projects in Microsoft Azure is finally at its conclusion.

Over time there will be updates and cleaning up. 

However, whoever is viewing this. 

I hope  you learned a lot because I have learned a lot. 

I started this project April 9th, 2023 and completed it May 1st, 2023.
Overall it took roughly two weeks to complete everything. 
Handling personal matters, took time away from this project.

Next project, which is optional, will be a Business Data Analysis project of project. 

![vivaldi_ZZiizg1fZY](https://user-images.githubusercontent.com/109401839/235540432-04a309b3-70db-4885-a61f-f7a14a2f16b2.png)

Thank you.
