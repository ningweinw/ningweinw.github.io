# Notes on AZ-140 Labs
1. Not every region can be used to create workspace, host pool and application group. For simplicity and avoiding region related errors, use one of the following regions throughout all labs: **eastus**, **eastus2**, **westus**, **westus2**, **centralus**.
2. At the end of lab **Deploy host pools and hosts by using Azure Resource Manager templates**, delete resources with the following steps:
    - In Azure portal, select **Azure Virtual Desktop** service, select **Host pools** blade, select **az140-23-hp2**, select **Session hosts** blade, select all hosts and click **Remove**
    - Delete resource group **az140-23-RG**
3. At the end of lab **Deploy and manage host pools and hosts by using PowerShell**, delete resources with the following steps:
    - In Azure portal, select **Azure Virtual Desktop** service, select **Host pools** blade, select **az140-24-hp3**, select **Session hosts** blade, select all hosts and click **Remove**
    - Delete resource group **az140-24-RG**
4. In lab **Configure Conditional Access policies for WVD (AD DS)**
    - If the **Start-ADSyncSyncCycle** command throws *...not recognized...* error, run the following command first:
        > Import-Module -Name "C:\Program Files\Microsoft Azure AD Sync\Bin\ADSync"
    - If **az140-cl-vm11** does not appear in Azure AD's Devices list after 10 minutes, run the following command in the **Administrator: Windows PowerShell ISE** window on **az140-dc-vm11**
        > Start-ADSyncSyncCycle -PolicyType Initial
