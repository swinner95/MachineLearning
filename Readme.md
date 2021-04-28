# Introduction
- This directory contains all that you need for onboarding your Deeprank model to AML. 
 
# Getting Started
- ## Permissions/SG needed to join
     Get your SG added to 
     1. AML resource group [bing-cr-prd](https://ms.portal.azure.com/#@72f988bf-86f1-41af-91ab-2d7cd011db47/resource/subscriptions/6560575d-fa06-4e7d-95fb-f962e74efd7a/resourceGroups/bing-cr-prd/overview)  
       - (Skip if you're already a part of modelfunteam@microsoft.com or aml-ds@microsoft.com)
     2. AML Workspace [bing-cr-aml-prd](https://ms.portal.azure.com/#@72f988bf-86f1-41af-91ab-2d7cd011db47/resource/subscriptions/6560575d-fa06-4e7d-95fb-f962e74efd7a/resourceGroups/bing-cr-prd/providers/Microsoft.MachineLearningServices/workspaces/bing-cr-aml-prd/overview).
       - (Skip if you're already a part of modelfunteam@microsoft.com or aml-ds@microsoft.com)
     3. Relevance ADLS group [relevance-c09_RWX](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupDetailsMenuBlade/Overview/groupId/eb2a3428-71c0-4751-9194-715007f36d74)
       - (Skip if you're already a part of aml-ds@microsoft.com or relevance-users@microsoft.com)

## What different AML scenarios are supported, how to switch between AML and ITP
### Scope

### Regular training

### Distributed training


### Hyperparam optimization


### PRS

### Using the Jupyter notebook to submit runs to AML
Start exploring deeprank/pagerec.ipynb Jupyter Notebook to submit AML pipelines.

### Using Aether to submit runs to AML/ITP 
#### Training
In Aether, by replacing your ITP training subgraph with only one Deeprank AML ITP training module, you can continue to submit to ITP cluster and/or AML compute
and get all the added benefits of AML. 

- The Deeprank AML ITP module takes only two parameters **stepConfigFile** and the **workspaceConfigFile** which submits to AML.
- You can edit the **overrideparams** parameter to overwride any parameters instead of editing these parameters in the config file. You can add parameters
as dictionary values for example {batch_size: 10}. 
- You can also add run tags in the **tags** parameter.  

Current Training Module submitted to ITP 




Benefits:
*	Improved experiment tracking 
*	Automated hyperparameter tuning
*	Increased resource utilization (AML Compute + existing ITP compute)
*	Replace long commands with configs and overridable params



#### Inferencing 

Benefits:
*	Increased resource utilization (AML Compute+existing ITP)
*	Automatic retries and non-redundant code/modules for batch inferencing
*	AEther graph for inferencing simplified by 100x

# How to do interactive debugging
[Coming soon]
# How to view metrics dashboard
[Coming soon]

# Contacts
Contact Aashna Garg (aagarg@microsoft.com), Shané Winner (shwinne@microsoft.com) for any questions/feedback.

Contacts for respective teams issues with: 

ADLS issues:
ComponentSDK issues:
Sweep issues:
PRS issues:

# Resources 
Link to documentation 

