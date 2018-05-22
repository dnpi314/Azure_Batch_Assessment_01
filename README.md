## Azure Batch Assessment 1This code sample is for use with the Azure Batch Assessment 01 scenario. [Assessment Scenario 01](https://azure.microsoft.com/documentation/articles/batch-dotnet-get-started/).

The solution includes two projects - *DotNetTutorial* and *TaskApplication* - that together demonstrate a common Batch application workflow. While the code in the solution does not demonstrate every feature of the Batch service, it is intended to act as a primer for basic Batch concepts and features such as pools, nodes, jobs, and tasks, as well as demonstrate interaction between Batch and the Azure Storage service.

The *DotNetTutorial* code sample is a Visual Studio 2015 solution consisting of two projects: **DotNetTutorial** and **TaskApplication**.

- **DotNetTutorial** is the client application that interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines). DotNetTutorial runs on your local workstation.

- **TaskApplication** is the executable that runs on compute nodes in Azure to perform the actual work. In the sample, `TaskApplication.exe` parses the text in a file downloaded from Azure Storage (the input file), and produces a text file (the output file) that contains a list of the top three words appearing in the input file. After creating the output file, TaskApplication then uploads the file to Azure Storage, making it available to the client application for download. TaskApplication runs in parallel on multiple compute nodes in the Batch service.

The following diagram illustrates the primary operations performed by the client application, *DotNetTutorial*, and the application that is executed by the tasks, *TaskApplication*. This basic workflow is typical of many compute solutions created with Batch, and while it does not demonstrate every feature available in the Batch service, nearly every Batch scenario will include similar processes.

![Batch example workflow][1]<br/>

**1.** Create blob **containers** in Azure Storage<br/>
**2.** Upload task application and input files to containers<br/>
**3.** Create Batch **pool**<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Pool **StartTask** downloads task binary (TaskApplication) to nodes as they join the pool<br/>
**4.** Create Batch **job**<br/>
**5.** Add **tasks** to job<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** The tasks are scheduled to execute on nodes<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;**5b.** Each task downloads its input data from Azure Storage, then begins execution<br/>
**6.** Monitor tasks<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** As tasks complete, they upload their output data to Azure Storage<br/>
**7.** Download task output from Storage

[dotnet_getstarted]: http://azure.microsoft.com/documentation/articles/batch-dotnet-get-started/
[1]: batch_workflow_sm.png "Batch solution workflow (full diagram)"

Lab Name: AzureBatch.L200.Troubleshooting.4

Introduction
This is a Level 200 lab for the Troubleshooting in Azure App Service.
Deployment Instructions
1.	First, create a Batch and storage account using the following guidance: https://docs.microsoft.com/en-us/azure/batch/quick-create-portal#create-a-batch-account. NOTE: they both must be within the same resourceGroup
2.	Once you have created the accounts above. Please download the code sample here: https://github.com/Walter-B-Jr/Azure_Batch_Assessment_01 
3.	Open the code sample in VS and make the following required changes:
a.	Open “Program.cs” under DotNetTutorial application. 
b.	Proceed to enter the credentials generated for both your Batch and storage account in the relevant fields:
i.	BatchAccountName
ii.	BatchAccountKey
iii.	BatchAccountUrl
iv.	StorageAccountName
v.	StorageAccountKey
vi.	You can name your PoolID and JobID however you desire.

 

Resources Created
This lab involves the following resources.
-	A Resource Group (preferable)
-	A Batch Account (required)
-	A Storage Account (required)

Scenario
In this lab, you will run the Batch Job. This Job’s Task should fail. 
Your Goal
Your goal is to identify the Task failure using our internal tools. (i.e. confirmation of failure using our internal tools). To confirm, you will be required to take a snapshot of the failure identified in KUSTO and Azure Batch Diagnostics tool. The goal is to use our internal tools to identify the Task failure. These images should include timestamps and the failure status.
Proof of Solution
1.	Provide a screen capture of KUSTO:  once you have found the error, highlighting the relevant indicators of the Task failure. KUSTO download:

Redmond mirror	 http://kusto-us/ke/Kusto.Explorer.application
ILDC mirror	 http://kusto/ke/Kusto.Explorer.aapplication 

2.	Provide a screen capture of the AzureBatchDiagnostics: https://azurebatchdiagnostics.azurewebsites.net/. Once you have found the error. Again, highlight the relevant indicators of the Task failure
3.	Bonus: Explain what the next steps in troubleshooting should be.
