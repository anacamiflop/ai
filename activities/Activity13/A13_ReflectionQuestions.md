# Activity 13 — Reflection Questions: Regularization at Mérida Homes

Answer every question below using the **Canonical Model** sections only (not the playground),
unless a question specifically asks about your own playground exploration. Submit this file
separately from your screenshots — do not just describe the app, use your actual results.

---

1. For the **plain (unregularized) model**, report the train R², the test R², and the exact
   gap between them.

The original model had a Train R² of 0.9871 and a Test R² of 0.8851, with a gap of 0.1020. After applying Ridge regularization with 0.03, the Train R² decreased slightly to 0.9861, while the Test R² increased to 0.8926. This represents an improvement of 0.0075 in Test R². Ridge helped the model generalize slightly better to unseen data by reducing the impact of large coefficients while maintaining high predictive accuracy.

---

2. Report all 8 coefficients of the **Canonical Ridge Model**.

The Ridge model uses eight features: size, bedrooms, age, distance to downtown, street number, owner's lucky number, front door paint color code, and owner's zodiac sign score. 

---

3. Report the **Canonical Ridge Model's** train R² and test R². Is the test R² better or worse
   than the plain model's test R² from Question 1?

The original model achieved a Train R² of 0.9871 and a Test R² of 0.8851. With Lasso regularization at 30, the Train R² decreased to 0.9777 and the Test R² decreased to 0.8760. Although the Test R² was slightly lower than that of the original model, Lasso simplified the model by setting two coefficients exactly to zero. This shows that Lasso can perform feature selection, making the model easier to interpret while potentially sacrificing a small amount of predictive accuracy.

---

4. Report all 8 coefficients of the **Canonical Lasso Model**, and name exactly which feature(s)
   were driven to zero.

The Lasso model uses eight features: size, bedrooms, age, distance to downtown, street number, owner's lucky number, front door paint color code, and owner's zodiac sign score.  The coefficients which drive to zero are, owner's lucky number and front door paint color code.

---

5. Report the **Canonical Lasso Model's** train R² and test R².

I would choose the Ridge model because it achieved the highest Test R² of 0.8926, compared with 0.8851 for the original model and 0.8760 for Lasso. This suggests that Ridge provides the best predictive performance on unseen data among the three models. It also reduces the magnitude of the coefficients, helping control overfitting without completely removing features. However, if simplicity and feature selection were more important than maximizing predictive accuracy, Lasso would also be a reasonable option.

---

6. In your own words, explain the key difference between how **Ridge** and **Lasso** treat
   coefficients as λ grows, based on what you saw in the bar charts.

Ridge and Lasso both penalize large coefficients to reduce overfitting, but they work differently. Ridge uses an L2 penalty that shrinks coefficients toward zero but generally does not make them exactly zero. Lasso uses an L1 penalty, which can set some coefficients exactly to zero and therefore eliminate features from the model. In my experiments, Lasso eliminated two features at 30 and 46, and four features at 70. This demonstrates how Lasso can perform automatic feature selection, while Ridge generally retains all features.

---

7. True or False: increasing λ always improves test R². Justify your answer using your own
   playground exploration (report at least one λ value where this was NOT the case).

**False.** Increasing λ does not always improve Test R² because excessive regularization can cause underfitting. In my Ridge experiments, the Test R² decreased from 0.8354 at λ = 0.26 to 0.7633 at λ = 0.53 and 0.6904 at λ = 0.86. In my Lasso experiments, the Test R² decreased from 0.8760 at λ = 30 to 0.8733 at λ = 46 and 0.8599 at λ = 70. These results show that stronger regularization can reduce the model's ability to capture meaningful patterns in the data. Therefore, λ should be selected carefully to balance overfitting and underfitting.

---

8. Name one **real business or IT scenario** (other than house pricing) where you'd worry about
   a model overfitting due to too many irrelevant features. Which regularization type (L1 or L2)
   would you reach for first, and why?

I would recommend regularization because it helps prevent a house-price prediction model from relying too heavily on individual features or random patterns in the training data. This can improve its ability to predict prices for houses it has not seen before. In the Mérida Homes example, variables such as an owner's lucky color code or the front door paint color code are unlikely to provide meaningful information about a property's market value. Lasso can eliminate irrelevant features, while Ridge reduces the influence of large coefficients. The best choice depends on the company's priorities: Ridge is useful when predictive accuracy is the main goal, while Lasso is helpful when a simpler and more interpretable model is preferred.
