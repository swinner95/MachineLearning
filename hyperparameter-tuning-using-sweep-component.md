# Hyperparameter Tuning using Sweep Component

## Introduction

This document provides an overview of how to use hyperparameter tuning using sweep component. Hyperparameters are adjustable parameters that let you control the model training process.


## Steps 
1. Use this [guide](https://msasg.visualstudio.com/Bing_and_IPG/_git/deeprank?path=%2Fdeeprank%2Fpagerec.ipynb&_a=preview) to walkthrough how to set up your resources. 
2. Use this [notebook](https://github.com/Azure/DesignerPrivatePreviewFeatures/blob/master/azure-ml-components/samples/how-to-use-sweep-component-for-hyperparameter-tuning.ipynb) 
to learn how to use Sweep component in AML Pipeline. The notebook covers the following:
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
5. In the **Experiments** tab, if you submitted a pipeline run, select the run and navigate to the **Steps** tab. 
6. Navigate to the **Child runs** tab to view each hyperdrive child run. This visualization tracks the metrics logged for each hyperdrive child run over 
  the duration of hyperparameter tuning. Each line represents a child run, and each point measures the primary metric value at that iteration of runtime. 
  ![](webxtsweep.gif)
  
## Resources 

1. [How to tune Hyperparameters](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-tune-hyperparameters)
2. [Hyperdrive Package](https://docs.microsoft.com/en-us/python/api/azureml-train-core/azureml.train.hyperdrive?view=azure-ml-py)
3. [hyperparameter-tune-and-warm-start-with-tensorflow.ipynb](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/ml-frameworks/tensorflow/hyperparameter-tune-and-warm-start-with-tensorflow/hyperparameter-tune-and-warm-start-with-tensorflow.ipynb)
4. [Sweep Component](https://componentsdk.azurewebsites.net/components/sweep_component.html)
