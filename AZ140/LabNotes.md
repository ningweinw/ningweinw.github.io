# Notes on AZ-140 Labs
1. Not every region can be used to create workspace, host pool and application group. For simplicity and avoiding region related errors, use one of the following regions throughout all labs: **eastus**, **eastus2**, **westus**, **westus2**, **centralus**.
2. In lab **Deploy host pools and hosts by using Azure Resource Manager templates**
    - At exercise 1, task 2, step 6, ensure **SystemData** field has value: `{}`
3. In lab **Configure Conditional Access policies for WVD (AD DS)**
    - If **az140-cl-vm11** does not appear in Azure AD's Devices list after 10 minutes, run the following command in the **Administrator: Windows PowerShell ISE** window on **az140-dc-vm11**
        > Start-ADSyncSyncCycle -PolicyType Initial
