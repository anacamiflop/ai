# Activity 14 — Reflection Questions: ShopSmart Churn Prediction

Answer every question below using the **Canonical Model** sections only (not the playground),
unless a question specifically asks about your own playground exploration. Submit this file
separately from your screenshots — do not just describe the app, use your actual results.

---

1. For the **plain (unregularized) model**, report the train accuracy, test accuracy, train
   loss, and test loss.

- **Train accuracy:** 100%
- **Test accuracy:** 77%
- **Train loss:** 0.022
- **Test loss:** 2.887

The unregularized model achieves 100% training accuracy, but its test accuracy is only 77%. Its training loss is 0.022, while its test loss is 2.887. This indicates overfitting because the model performs extremely well on the training data but does not generalize as effectively to unseen customers.

---

2. Report all 8 coefficients of the **Canonical L2 (Ridge) Model**.

1. Tenure (months as a customer): **-1.30**
2. Average monthly spend: **-0.14**
3. Support tickets filed: **0.70**
4. Days since last purchase: **0.47**
5. Favorite color: **-0.19**
6. Customer's lucky number: **-0.62**
7. Day of week they signed up: **-0.18**
8. Length of their referral code: **-0.25**

---

3. Report the **Canonical L2 Model's** train and test accuracy. How do they compare to the
   plain model's from Question 1?

- **Train accuracy:** 95%
- **Test accuracy:** 83%

Compared with the plain model, the Canonical L2 model's training accuracy decreased from 100% to 95%, while its test accuracy increased from 77% to 83%. This suggests that L2 regularization reduced overfitting and improved the model's ability to predict churn for unseen customers.

---

4. Report all 8 coefficients of the **Canonical L1 (Lasso) Model**, and name exactly which
   feature(s) were driven to zero.

1. Tenure (months as a customer): **-2.00**
2. Average monthly spend: **0**
3. Support tickets filed: **0.40**
4. Days since last purchase: **0.27**
5. Favorite color: **0**
6. Customer's lucky number: **0**
7. Day of week they signed up: **0**
8. Length of their referral code: **0**

L1 zeroed out five of the eight features: average monthly spend, favorite color, customer's lucky number, day of week they signed up, and length of their referral code. The three features that retained non-zero coefficients were tenure, support tickets filed, and days since last purchase.

---

5. Report the **Canonical L1 Model's** train and test accuracy.

- **Train accuracy:** 95%
- **Test accuracy:** 73%

The Canonical L1 model achieves 95% training accuracy and 73% test accuracy. Although it simplifies the model by eliminating five features, its test accuracy is lower than that of both the plain model and the Canonical L2 model. This shows that removing features does not always improve predictive performance.

---

6. In your own words, explain the key difference between how **L2** and **L1** treat
   coefficients as λ grows, based on what you saw in the bar charts.

As λ increases, L2 regularization gradually shrinks coefficients toward zero, but they generally remain nonzero. In contrast, L1 regularization can set coefficients exactly to zero, effectively removing features from the model. In my experiments, L1 eliminated five features at λ = 0.05, seven at λ = 0.28, and all eight at λ = 0.37. This demonstrates that L1 can perform automatic feature selection, while L2 mainly reduces coefficient magnitudes.

---

7. True or False: the unregularized model's 100% training accuracy means it's the best model to
   actually deploy for predicting churn on new customers. Justify your answer using the actual
   numbers from Question 1.

**False.** Although the unregularized model achieves 100% training accuracy, its test accuracy is only 77%. Its training loss is 0.022, while its test loss is 2.887, which is more than 130 times higher. This indicates that the model has overfit the training data and may not predict churn as reliably for new customers. The Canonical L2 model achieves a higher test accuracy of 83%, making it a stronger candidate based on test accuracy.

---

8. Name one **real business or IT scenario** (other than churn prediction) where a
   classification model could overfit due to too many irrelevant features. Which
   regularization type (L1 or L2) would you reach for first, and why?

One example is an IT department predicting whether a support ticket will violate its service level agreement. Useful features might include ticket priority, issue category, and time since creation, while irrelevant features could include an employee's favorite color or an arbitrary ticket identifier.

I would start with L1 regularization because it can set the coefficients of irrelevant features to zero. This simplifies the model and makes it easier to identify which factors are most useful for predicting SLA violations.
