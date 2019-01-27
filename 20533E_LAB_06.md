# Module 6: Planning and implementing Azure Storage
# Lab A: Planning and implementing Azure Storage
  
### Scenario
  
 The IT department at A. Datum Corporation uses an asset management application to track IT assets such as computer hardware and peripherals. The application stores images of asset types and invoices for asset purchases As part of A. Datum's evaluation of Azure, you need to test migration of these images and invoice documents to Azure storage. A. Datum also wants to evaluate Azure File storage for providing SMB 3.0 shared access to invoices. Currently, corporate file servers host this content. 

### Objectives
  
 After completing this lab, you will be able to:

- Creating and configuring Azure Storage.

- Use Azure file storage.


### Lab Setup
  
 Estimated Time: 50 minutes

 Virtual machine: **20533E-MIA-CL1**

- User name: **Student**

- Password: **Pa55w.rd**

 Before starting this lab, ensure that you have performed the "Preparing the environment" demonstration tasks at the beginning of the first lesson in this module and that the setup script has completed.

## Exercise 1: Creating and configuring Azure Storage
  
### Scenario
  
A. Datum currently stores images for IT assets on the on-premises file servers. As part of your Azure evaluation, you want to test storing these images as blobs in Azure storage so that a new Azure-based version of the asset management application can easily access them.

The main tasks for this exercise are as follows:

1. Create a storage account

2. Install AzCopy 

3. Use AzCopy to upload blobs

#### Task 1: Create a storage account
  
1. Ensure that you are signed in to the MIA-CL1 virtual machine as **Student** with the password **Pa55w.rd** and that the setup script that you ran in the "Preparing the environment" demonstration has completed.

2. Use Internet Explorer to sign in to the Azure portal by using the Microsoft account that is the Service Administrator or a Co-Administrator of your Azure subscription.

3. Create a new storage account with the following settings:

  - Subscription: the name of your Azure subscription
  
  - Resource group: ensure that **Create new** is selected and, in the textbox below, type **20533E0602-LabRG**.
  
  - Name: a valid, unique name consisting of between 3 and 24 lower case characters or digits

  - Performance: **Standard**
  
  - Account kind: **Storage (general purpose v1)**

  - Location: the same Azure region that you chose when running the provisioning script at the beginning of this module

  - Replication: **Locally-redundant storage (LRS)**

  - Secure transfer required: **Disabled**

  - Allow access from: **All networks**
  
  - Hierarchical namespace: **Disabled**

4. After the storage account is provisioned, create a blob container named **asset-images** with private access.


#### Task 2: Install AzCopy
  
1. Download and install AzCopy from [**http://aka.ms/AzCopy**](http://aka.ms/AzCopy). Note that this page also includes documentation and examples for using AzCopy.

2. Start Windows PowerShell ISE as Administrator.

3. In the console pane of Windows PowerShell ISE, change the current directory by running:
 
```
Set-Location -Path 'C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy'
```

4. Test the installation by running the following command at a command prompt:

```
.\AzCopy /?
```

5. Keep the Windows PowerShell ISE window open for the next task.


#### Task 3: Use AzCopy to upload blobs

1. In the Windows PowerShell ISE window, type the following in the script pane:

```
.\AzCopy.exe /Dest:https://<storage-account-name>.blob.core.windows.net/asset-images /destkey:<access-key> /Source:F:\Labfiles\Lab06\Starter\asset-images
```

2. In the Azure portal, copy the name of the Storage account you created earlier in this exercise. 

3. In the script pane of the Windows PowerShell ISE, replace the ***\<storage-account-name\>*** entry with the storage account name you copied from the Azure portal.

4. In the Azure portal, copy the first access key of the Storage account. 

5. In the script pane of the Windows PowerShell ISE, replace the ***\<access-key\>*** entry with the storage account key you copied from the Azure portal.

6. Execute the command in the script pane and wait for the command to complete. Review the file transfer information.

7. In the Azure portal, navigate to the **asset-images** container blade and verify that the container contains six blobs.

> **Result**: At the end of this exercise, you should have created a new Azure storage account with a container named **asset-images** and copied files from your local computer to that container by using the **AzCopy** utility.





#### Task 4: Remove the lab environment

1. On MIA-CL1, close all open windows without saving any files.

2. Start **Windows PowerShell** as Administrator and, from the **Administrator: Windows PowerShell** window, run **Remove-20533EEnvironment**.

3. When prompted, sign in by using the Microsoft account that is the Service Administrator of your Azure subscription.

4. If you have multiple Azure subscriptions, select the one you want the script to target.

5. If prompted, specify the current lab number.

6. When prompted for confirmation, type **y**.

7. Start Microsoft Edge, browse to the Azure portal, and sign in by using the Microsoft account that is the Service Administrator of your Azure subscription.

8. In the Azure portal, reset the dashboard to the default state. 

9. Close all open windows.


> **Result**: At the end of this exercise, you should have created an Azure storage account file share named **assets** that contains a folder named **invoices** with copies of invoice documents. You should have also mapped a drive from an Azure VM to the Azure storage account file share.


**Question** 
The asset management application stores images of hardware components as blobs and invoices as files. If the application also needed to search the location of each asset by using an asset type, a unique asset number, and a text description of the location, what storage options should you consider?


©2016 Microsoft Corporation. All rights reserved.

The text in this document is available under the [Creative Commons Attribution 3.0 License](https://creativecommons.org/licenses/by/3.0/legalcode "Creative Commons Attribution 3.0 License"), additional terms may apply.  All other content contained in this document (including, without limitation, trademarks, logos, images, etc.) are **not** included within the Creative Commons license grant.  This document does not provide you with any legal rights to any intellectual property in any Microsoft product. You may copy and use this document for your internal, reference purposes.

This document is provided "as-is." Information and views expressed in this document, including URL and other Internet Web site references, may change without notice. You bear the risk of using it. Some examples are for illustration only and are fictitious. No real association is intended or inferred. Microsoft makes no warranties, express or implied, with respect to the information provided here.
