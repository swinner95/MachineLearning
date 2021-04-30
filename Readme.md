# Introduction
- This directory contains the documentation and configuration files needed to help oboard your Deeprank model to AML. 
 
# Getting Started

## Permissions
 Please ensure you join the "aml-deeprank" Security Group on [idweb](https://idweb/). 
 
 ## AML Scenarios Supported 
* Scope
* Regular training
* Distributed training
* PRS 
* Hyperparameter optimization

## Three approaches to submit jobs to AML

### 1. Run AML Pipeline From DevBox (CLI)
For information on the installation and job submission please see [here](https://msasg.visualstudio.com/Bing_and_IPG/_git/deeprank?path=%2Fdeeprank%2FREADME.md&version=GBmaster&_a=preview&anchor=run-aml-pipeline-from-devbox-(work-in-progress))

  
### 2. Jupyter Notebook 
Steps: 

1. Setup compute instance - 
2. Open Jupyter Lab
3. Create a new notebook or git clone the deeprank repo 
4. Run the notebook **aml-deeprank.ipynb**


1. All the deeprank supported models can be found in the [deeprank/configs folder](https://msasg.visualstudio.com/Bing_and_IPG/_git/deeprank?path=%2Fdeeprank%2Fconfigs&version=GBmaster)
2. For every model deeprank supports, there is a separate json file for each type of job submission (regular training, distributed training, sweep or PRS job) in the **aml** folder for that model.  eg. [deepranl/configs/meb/qr_embedding_bag_nested/aml/regular_job_adls_mount.json](https://msasg.visualstudio.com/Bing_and_IPG/_git/deeprank?path=%2Fdeeprank%2Fconfigs%2Fmeb%2Fqr_embedding_nested%2Faml%2Fdistributed_job_adls_direct.json&version=GBmaster)
3. You will need to customize the json file and make changes to the input paths, output paths and/or user command. This json is used to submit a [regular training job](https://msasg.visualstudio.com/Bing_and_IPG/_git/deeprank?path=%2Fdeeprank%2Fcomponents%2Fregular_job%2Fcuda10.1&version=GBmaster), [distributed training job](https://msasg.visualstudio.com/Bing_and_IPG/_git/deeprank?path=%2Fdeeprank%2Fcomponents%2Fdistributed_job%2Fcuda10.1&version=GBmaster), [inferencing job (PRS)](https://msasg.visualstudio.com/Bing_and_IPG/_git/deeprank?path=%2Fdeeprank%2Fcomponents%2Finference_job&version=GBmaster), sweep or scope jobs to AML.  Ensure to reference the input paths in the **user_command**.

### 3. Aether Path (Work in Progress) 
There will be a new Aether module that you can use to specify your input and output paths simarly to what was done in approach #2. The AML module will have a command parameter and 10 input paths as parameters so that you can reference the input paths in the command. 

[Aashna to provide screenshot] 

### Using the Jupyter notebook to submit runs to AML
Start exploring this [Notebook](https://msasg.visualstudio.com/Bing_and_IPG/_git/deeprank?path=%2Fdeeprank%2Fpagerec.ipynb&version=GBaagarg%2Franklm&_a=preview&anchor=getting-started) to submit AML pipelines.

## Using Aether to submit runs to AML/ITP 
### Training
In Aether, by replacing your ITP training subgraph with only one Deeprank AML ITP training module, you can continue to submit to ITP cluster and/or AML compute
and get all the added benefits of AML. 

**Current Training Module submitted to ITP**

![](trainingimage1.GIF)


**AML Deeprank Training Module**
- The Deeprank AML ITP module takes only two parameters **stepConfigFile** and the **workspaceConfigFile** which submits to AML. 
- In this repository, you can find the configuration template for the **stepConfigFile** in this folder 'deeprank/aml_pipeline/configs/pipeline_params/ranklm_train_itp.json'. 
- In this repository, you can find the configuration template for the **workspaceConfigFile** in this folder 'deeprank/aml_pipeline/configs/workspace/itp_workspace.json'. 
- You can edit the **overrideparams** parameter to overwride any parameters instead of editing these parameters in the config file. You can add parameters
as dictionary values for example {batch_size: 10}. 
- You can also add run tags in the **tags** parameter.  

![](trainingimage2.GIF)

**Benefits:**
*	Improved experiment tracking 
*	Automated hyperparameter tuning
*	Increased resource utilization (AML Compute + existing ITP compute)
*	Replace long commands with configs and overridable params

### Inferencing 
In Aether, by replacing your Inferencing subgraph with only one Deeprank AML ITP inferencing module, you can continue to submit to ITP cluster and/or AML compute
and get all the added benefits of AML. 
![](inferenceimage1.GIF)

**AML Deeprank PRS Module**
- The Deeprank AML PRS module takes only two parameters **stepConfigFile** and the **workspaceConfigFile** which submits to AML.
- In this repository, you can find the configuration template for the **stepConfigFile** in this folder 'deeprank/aml_pipeline/configs/pipeline_params/ranklm_inference-prs.json'. 
- In this repository, you can find the configuration template for the **workspaceConfigFile** in this folder 'deeprank/aml_pipeline/configs/workspace/aml_workspace.json'.
- You can edit the **overrideparams** parameter to overwride any parameters instead of editing these parameters in the config file. You can add parameters
as dictionary values for example {batch_size: 10}. 
- You can also add run tags in the **tags** parameter.  

![](inferenceimage2.GIF)

**Configurable Parallelization**
- There is also configurable parallelization where you can specify the number of **numNodes** and **numGPUs** which can save 100x graph complexity. 
![](configure.GIF)
**Benefits:**
*	Increased resource utilization (AML Compute+existing ITP)
*	Automatic retries and non-redundant code/modules for batch inferencing
*	Aether graph for inferencing simplified by 100x




### Hyperparameter optimization
Hyperparameter tuning, also called hyperparameter optimization, is the process of finding the configuration of hyperparameters that results in the best performance. The process is typically computationally expensive and manual. Use this [notebook](https://msasg.visualstudio.com/Bing_and_IPG/_git/deeprank?path=%2Fdeeprank%2Fpagerec.ipynb&_a=preview) to walkthrough how to set up your resources and to learn how to submit an AML Pipeline using the sweep component. The **Hyperparameter Optimization** section of the notebook covers how to configure and submit a pipeline sweep job. See [here](https://componentsdk.azurewebsites.net/components/sweep_component.html) for more details on the Sweep component. 

Use the configuration file [sweep.json](https://msasg.visualstudio.com/Bing_and_IPG/_git/deeprank?path=%2Fdeeprank%2Faml_pipeline%2Fconfigs%2Fpipeline_params%2Fsweep.json) to edit the parameters and settings for your job. This file outlines how you can do the following tasks.  

  * Define the parameter search space. In this example, we are tuning on **batch_size_per_gpu** and **learning_rate**. 
  * Specify a primary metric to optimize. In this example, we are optimizing the metric **onedcg_3**. 
  * Specify early termination policy for low-performing runs
  * Create and assign resources
  * Launch an experiment with the defined configuration
  * Visualize the training runs
  * Select the best configuration for your model

#### Visualize hyperparameter tuning runs
4. After you submit your training job, you can visualize your hyperparameter tuning runs in the [Azure Machine Learning studio UI](ml.azure.com),
or you can use a [notebook widget](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-tune-hyperparameters#notebook-widget).
5. In the **Experiments** tab, if you submitted a pipeline run, select the run and then select the **Steps** tab. 
6. Navigate to the **Child runs** tab to view each hyperdrive child run. This visualization tracks the metrics logged for each hyperdrive child run over 
  the duration of hyperparameter tuning. Each line represents a child run, and each point measures the primary metric value at that iteration of runtime. 
  ![](webxtsweep.gif)


# Additional Information

### How to do interactive debugging
[Coming soon]
### How to view metrics dashboard
[Coming soon]

### Contacts
Contact Aashna Garg (aagarg@microsoft.com), Shané Winner (shwinne@microsoft.com) for any questions/feedback.

Contacts for respective teams issues with: 

ADLS issues:
ComponentSDK issues:
Sweep issues:
PRS issues:

### Resources 
[Sweep Component](https://componentsdk.azurewebsites.net/components/sweep_component.html)

