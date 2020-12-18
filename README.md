# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
The main dataset for this project is the BankMarketing dataset ("https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv). This dataset contains both categorical and numerical features (20) and target/label for supervised classification ('y'). The aim of the project is to predict if a client will subscribe a term deposit (binary class). For that different approaches were carried out based on the following workflow: 

![GitHub pipeline](/images/creating-and-optimizing-an-ml-pipeline.png)

Concretely, a **LR (logistic regression) baseline** was provided through train.py script. This was totally parametrizable and will enable the Hyperdrive to explore a hyperparameter space using the sampling method that we choose (in this case it was **RandomParameterSampling** choosen). After tuning the hyperparameters using **Hyperdrive** and getting an optimal model, the AutoML process was carried out for both comparison. The best model from both processes are saved in order to compare their performance. 




From both approaches in the pipeline (HD and AutoML) the best performing model was a AutoML. Concretely VotingEmsemble with an accuracy of 0.91763. See below both accuracies of best runs on both approaches.

**Accuracy of best run HyperDrive : 0.9074355083459787**

**Accuracy of best model AutoML (VotingEnsemble) : 0.91763**




## Scikit-learn Pipeline

For skit-learn pipeline, traditional ML data split was carried out (80-20) for train-test dataset on **train.py** after dealing with categorical data (one-hot encoding). **Train.py** was fully parametrizable to enable Hyperdrive the exploration of a hyperparameter search space during fine-tuning. Hyperparameters explored were '--C' Inverse of regularization strength and '--max_iter' Maximum number of iterations to converge. Classification algorithm was LogisticRegression. 


The parameter sampler chosen is **RandomSamplingParameter**. It supports discrete and continuous hyperparameters. It is perfect for first approaches and for non exhaustive search space exploration (based on sampling distribution selected). This makes this approach less expensive than other choices as GridSampling.

Early stopping chosen was **MedianStoppingPolicy** based on Google Vizier: A Service for Black-Box Optimization. The main advantage of this policy is that it allows us to be conservative (incurring in less costs) and early stop without losing promising processes. From Microsoft heuristic: 25%-35% savings with no loss on primary metric.


## AutoML
AutoML trained several models based on target metric (Accuracy). Among others there were StackEnsemble, StandardScalerWrapper, XGBoostClassifier, LightGBM, MaxAbScaler...resulting best model VotingEmsemble with aforementioned Accuracy (see images/automl_train_models.png for further details and /images/automl_metrics_and_explanation for additional metrics and model explanation). 


## Pipeline comparison

During this project 2 pipelines were compared: hyperdrive driven pipeline and automl driven pipeline (see workflow above). However, the goal of each pipeline was different. Hyperdrive aimed to automate efficient hyperparameter tuning through one selected model (Logistic Regression in this case). Whereas AutoML enabled multiple concurrent model training based on different algorithms as well as parameters configurations. 
Thus, as expected, AutoML outperformed Hyperdrive in our main evaluation metric (Accuracy). VotingEmsemble as a result of autoML had an accuracy of 0.91763, while Hyperdrive was able to achieve an 0.9074355083459787. 
Please refer to 'images' folder for further metrics and screenshots.


## Future work
There are some areas of improvement identified for future experiments:
1- Additional hyperparameters configurations exploration could be carried out under Hyperdrive pipeline.
2- From AutoML outputs data imbalance and bias has been identified. Further data exploration and some corrective measures would help on that. Bias mitigation will lead us to more realistic results.
3- In case of having enough resources a more exhaustive hyperparameter grid exploration through GridSampling could be done. 

## Proof of cluster clean up
Deleted on notebook: cpu_cluster.delete()
![GitHub cluster_proof](/images/resource_delete_proof.png)

