# Individualized Risk Assessment of Preoperative Opioid Use by Interpretable Neural Network Regression

Table of contents
=================

<!--tc-->
   * [Table of contents](#table-of-contents)
   * [Overview](#overview)
   * [Requirements](#requirements)
   * [INNER Model](#inner-model)
   * [Data](#data)
   * [Demo](#demo)
<!--tc-->

Overview
========

This project aims to understand the risk of preoperative opioid. A novel Interpretale Neural Network Regression (INNER) is proposed to conduct individualized risk assesment of preoperative opioid use. Intensive simulations and statistical analysis of 34,186 patients expecting surgery in the Analgesic Outcomes Study (AOS) show that the proposed INNER not only can accurately predict the preoperative opioid use based on preoperative characteristics as deep neural network (DNN), but also can estimate the patient-specific odds of opioid use without pain and the odds ratio of opioid use for one  unit increase in  the reported overall body pain, leading to more straightforward interpretations on opioid tendency compared to DNN.

Requirements
============

The project has been tested on Python 3.7.4 with `Tensorflow == 2.0.0`, `Scikit-learn == 0.20.2` , `Pandas == 0.24.1` and `Numpy == 1.17.4`.

INNER Model
===========

<img align="middle" src="https://github.com/YumingSun/INNER/blob/master/utilities/ArchitecutreOfINNER.png">

In the INNER model, we  utilize DNN to construct individualized coefficients in a logistic regression model, wherein  the regression coefficients are functions of individual characteristics. They lead to two metrics, Baseline Opioid Tendency (BOT) and Pain-induced Opioid Tendency (POT), which are useful for the individualized assessment of opioid use for each patient. In particular, BOT refers to the odds of receiving preoperative opioids when the patient does not report pain and POT is the odds ratio of  receiving preoperative opioids for one unit increase in the reported overall body pain. To print the summary of the INNER model architecture used for AOS data run:
```
$ python SummaryModel.py
```

Data
====
The training dataset, `TrainingData.csv`, and the testing dataset, `TestingData.csv`, are simulated as described in the _Simulation Study_ part of the papaer. There are 16,000 observations in the training dataset and 4,000 observations in the testing dataset. Both of the two datasets have one label and three features. 

Demo
====
* `train.py`: The script used to train the INNER model. To train the INNER model run:
```
$ python train.py PATH_TO_TRAINING_DATA PATH_TO_MODEL
```
It trains the INNER model using training data at `PATH_TO_TRAINING_DATA` and saves the trained model at `PATH_TO_MODEL`. Pre-trained model is `pre_trained_model.h5`. The training process takes about one minute.

* `test.py`: The script used to evaluate the performance of the INNER model. To evaluate the performance run:
```
python test.py PATH_TO_TESTING_DATA PATH_TO_MODEL
```
It evaluate the performance of pre-trained model at `PATH_TO_MODEL` using testing data at `PATH_TO_TESTING_DATA`. It prints out the C statistics, accuaracy, sensitivity, specificity and balance accuracy. The testing process takes few seconds.

* `estimate.py`: The script used to estimate the BOT and POT. To estimate these two metrics run:
```
python estimate.py PATH_TO_ESTIMATE_DATA PATH_TO_MODEL PATH_TO_OUTPUT
```
It estimate the BOT and POT for each subject in the data at `PATH_TO_ESTIMATE_DATA` using pre-trained model at `PATH_TO_MODEL`. It prints out the first five results and save all the results at `PATH_TO_OUTPUT`. The estimation process takes few seconds.
