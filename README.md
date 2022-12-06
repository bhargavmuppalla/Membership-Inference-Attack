# Membership-Inference-Attack
Membership inference attacks were first described by Shokri et al. [1] in 2017. Since then, a lot of research has been conducted in order to make these attacks more efficient, to measure the membership risk of a given model, and to mitigate the risks.

The aim of a membership inference attack is quite straight forward: Given a trained ML model (we termed is as “the target model”) and some data point, decide whether this point was part of the model’s training sample or not. You might not see the privacy risk right away, but think of the following situation: imagine you are in a clinical context. There, you may have an ML model that is supposed to predict an adequate medical treatment for cancer patients. This model, naturally, needs to be trained on the data of cancer patients. Hence, given a data point, if you are able to determine that it was indeed part of the model’s training data, you will know that the corresponding patient must have cancer. As a consequence, this patient’s privacy would be disclosed. This example may convince you of the importance of membership privacy. Basically, in any context where the sheer fact of being included in a sample can be privacy disclosing, membership inference attacks pose a severe risk.

# How Membership-Inference-Attack Works?
Most membership inference attacks work similar as the original example described by Shokri et al. [1], namely by building a binary meta-classifier fattack that, given a target model f and a data point xi, decides whether or not xi was part of the model’s training set X.

![alt text](https://github.com/bhargavmuppalla/Membership-Inference-Attack/blob/main/MIA.png)

Membership Inference attack is type of attack on machine learning models to detect the data that is used for training the model. When the target model has been trained using sensitive data, membership inference can raise security and privacy issues.

In our Project the target_model(the machine learning model which we are attacking) predicts the images. When data is passed to target model, it returns a vector of values indicating the probability of each image. The index which has largest value in the vector is predicted as image label.

Now To create MIA model. We need outputs from target model.

The main idea for MIA model is, if we pass training data to target_model for prediction it predicts with higher confidence. Whereas if we try to predict using target_model for new data, prediction confidence with be relatively lower.

Based on above idea, MIA model is created. During training, a threshold value is calculated based on which members(data used in training the target model) and non-members are segregated when predicting.



MIA Model Code Details:
Training:
We have been given train_data_partials.npy file which contains a set of data sample used for training target model. Prediction for these should be 1. 

First step is normalizing the data. This step is important to calculate threshold. If data is in different range, threshold doesn’t influence our prediction properly. So min max normalization(x-min/max-min) is performed on the data. After normalizing all the values will in the range of [0,1].

A function called normalize() is Implemented, which takes list of list as parameter and modify the list values so that minimum value in list is 0 and max value will be 1. This normalize function is called




After normalizing, calculating threshold is done using calculate_threshold()

In Calculate threshold, sum of differences between all the values and maximum value of the list is calculated for each vector and average is taken for this sum.

Similarly averages for all vectors will be calculated. And average of these averages are returned as threshold.


The reason for this average of differences with the maximum value is, for training data the difference with maximum value with other elements in the vector should be higher for training data as compared to testing data as the prediction confidence will be higher for training data.

calculate_threshold()  is called for members data to get members threshold and also called for non members data to get non_members threshold

for classification purpose, non_members threshold is used to classify members and non members. If average of difference of evaluation data vector is greater than threshold, then it is categorized as member, else non member.

Result and evaluation:
Prediction evaluation_data.npy is stored in Your_evaluation_result variable which is a list of 1’s and 0’s.

When MIA is tested with test_member_data.npy and test_non_member_data.npy. an accuracy of 53% is achieved. 

The reason for low accuracy of MIA model can be because of robustness of target model, which has an accuracy of 90%. Which means it performs well for new data without any bias towards training data.
