# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
The main dataset for this project is the BankMarketing dataset ("https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv). This dataset contains both categorical and numerical features (20) and target/label for supervised classification ('y'). The aim of the project is to predict if a client will subscribe a term deposit (binary class). For that different approaches were carried out based on the following workflow: 



Concretely, a **LR baseline** was provided through train.py script. This is totally parametrizable and will enable the Hyperdrive to explore a hyperparameter space using the sampling method that we choose (in this case it was **RandomParameterSampling** choosen). After tuning the hyperparameters using **Hyperdrive** and getting an optimal model, the AutoML process was carried out for both comparison. The best model from both processes are saved in order to compare their performance. 




**In 1-2 sentences, explain the solution: e.g. "The best performing model was a ..."**

Accuracy of best run HyperDrive : 0.9074355083459787




## Scikit-learn Pipeline
**Explain the pipeline architecture, including data, hyperparameter tuning, and classification algorithm.**

**What are the benefits of the parameter sampler you chose?**

**What are the benefits of the early stopping policy you chose?**

## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**

## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**

## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**

## Proof of cluster clean up
**If you did not delete your compute cluster in the code, please complete this section. Otherwise, delete this section.**
**Image of cluster marked for deletion**
