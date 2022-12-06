# Membership-Inference-Attack
Membership inference attacks were first described by Shokri et al. [1] in 2017. Since then, a lot of research has been conducted in order to make these attacks more efficient, to measure the membership risk of a given model, and to mitigate the risks.

The aim of a membership inference attack is quite straight forward: Given a trained ML model (we termed is as “the target model”) and some data point, decide whether this point was part of the model’s training sample or not. You might not see the privacy risk right away, but think of the following situation: imagine you are in a clinical context. There, you may have an ML model that is supposed to predict an adequate medical treatment for cancer patients. This model, naturally, needs to be trained on the data of cancer patients. Hence, given a data point, if you are able to determine that it was indeed part of the model’s training data, you will know that the corresponding patient must have cancer. As a consequence, this patient’s privacy would be disclosed. This example may convince you of the importance of membership privacy. Basically, in any context where the sheer fact of being included in a sample can be privacy disclosing, membership inference attacks pose a severe risk.

# How Membership-Inference-Attack Works?
Most membership inference attacks work similar as the original example described by Shokri et al. [1], namely by building a binary meta-classifier fattack that, given a target model f and a data point xi, decides whether or not xi was part of the model’s training set X.

