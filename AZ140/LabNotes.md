# Notes on AZ-140 Labs
1. Not every region can be used to create workspace, host pool and application group. For simplicity and avoiding region related errors, use one of the following regions throughout all labs: **eastus**, **eastus2**, **westus**, **westus2**, **centralus**.
2. At the end of lab **Deploy host pools and hosts by using Azure Resource Manager templates**, delete resources with the following steps:
    - In Azure portal, select **Azure Virtual Desktop** service, select **Host pools** blade, select **az140-23-hp2**, select **Session hosts** blade, select all hosts and click **Remove**
    - Delete resource group **az140-23-RG**
3. At the end of lab **Deploy and manage host pools and hosts by using PowerShell**, delete resources with the following steps:
    - In Azure portal, select **Azure Virtual Desktop** service, select **Host pools** blade, select **az140-24-hp3**, select **Session hosts** blade, select all hosts and click **Remove**
    - Delete resource group **az140-24-RG**
