# Activity 17 — Reflection Questions: Second Opinion (Support Vector Machines)

Answer every question using the app's **default settings**, unless a question tells you to change
something. Submit this file together with your labeled screenshots — do not just describe the app,
use your actual results.

---

## Part A — The widest street (margin and support vectors)

1. In *The Widest Street* tab, report the number of **support vectors**, the **margin width**, and
   the **test accuracy**. Then turn on **"Retrain the SVM using only the support vectors"**: how
   many training points were used, and how much did the line change?

   With the default settings, the SVM used 3 support vectors out of 40 training points, the margin width was 1.599, and the test accuracy on 400 new points was 100.0%. After switching on "Retrain the SVM using only the support vectors", only 3 training points were used, and the largest change in the line's equation was 2.8e-07, which is practically zero. The line stayed the same even though 37 points were discarded.

---

2. In your own words, what is a **support vector**, and why does the result of Question 1 explain
   the name "*support* vector machine"?

   A support vector is a training point that sits on the edge of the street (the margin) and therefore fixes where the decision boundary goes. In Q1, the three circled points alone reproduced the same boundary as all 40 points, so the other 37 points could be removed without changing anything. The boundary is held in place ("supported") by those few points, which is why the method is called a support vector machine. With a soft margin, points inside the margin or on the wrong side can also be support vectors.

---

## Part B — C and the soft margin

3. In the *C and the Soft Margin* tab, report the following for **C = 0.001**, **C = 1**, and
   **C = 10000**: margin width, number of support vectors, training points on the wrong side,
   training accuracy, test accuracy, and how the outlier is classified.


   - **C = 0.001:** margin width 10.197, 80 support vectors, 6 training points on the wrong side, training accuracy 92.6%, test accuracy 95.3%, outlier classified as **[VERIFY IN APP: Blue or Red]**.
   - **C = 1:** margin width 2.577, 4 support vectors, 1 training point on the wrong side, training accuracy 98.8%, test accuracy 100.0%, outlier classified as Red.
   - **C = 10000:** margin width 0.015, 3 support vectors, 0 training points on the wrong side, training accuracy 100.0%, test accuracy 94.7%, outlier classified as Blue (its assigned label).
  
---

4. The lecture says: *"A larger value of C can be beneficial when the data points are not
   well-separated or when there is a significant presence of noise or outliers."* Using your numbers
   from Question 3, do you agree? Which C would you choose for this data, and why?

   I disagree with the lecture's statement, at least for this dataset. Raising C to 10000 made the model reach 100.0% training accuracy by tilting the boundary and shrinking the margin to 0.015 so that it could classify the mislabeled outlier "correctly", but test accuracy dropped to 94.7%. The model was memorizing the noise. In the "Every C at once" chart, test accuracy stays at about 100% from roughly C = 0.003 up to C = 30 and then falls as C keeps growing, while the margin shrinks steadily. I would choose C = 1: it has 100.0% test accuracy, a wide margin of 2.577, and it accepts one training error (the outlier) instead of bending the boundary for it. C = 0.001 is too soft (margin 10.197, 6 training errors, 95.3% test accuracy). A large C is not automatically better with noisy data; C should be chosen with validation.

---
## Part C — Kernels

5. In the *Kernels* tab, with the **Circles** dataset, C = 1, gamma = 1, and degree = 2, report the
   **test accuracy** of the linear, polynomial, RBF, and sigmoid kernels. Why does the linear kernel
   fail on this dataset?

   With the Circles dataset, C = 1, gamma = 1, and degree = 2, the test accuracies were 56.0% for the linear kernel, 100.0% for the polynomial kernel, 99.8% for the RBF kernel, and 53.5% for the sigmoid kernel. The linear kernel failed because one class forms a ring inside the other, so a single straight line cannot separate them. It reached only 59.0% training accuracy and needed 193 of the 200 points as support vectors. The polynomial and RBF kernels draw closed curved boundaries around the inner ring, and they needed only 7 and 30 support vectors. The sigmoid kernel did even worse than the linear one (49.5% training accuracy, below chance), so a nonlinear kernel is not guaranteed to fit the data.

---

6. Using the **RBF** kernel, find settings (dataset, C, gamma) that clearly **overfit**: training
   accuracy much higher than test accuracy. Report your settings and both accuracies, include a
   screenshot, and describe what the boundary looks like.

   Settings: Circles dataset, RBF kernel, C = 1000, gamma = 1000. Training accuracy was 100.0% and test accuracy was 65.2%, a gap of 34.8 percentage points (the app itself warns that the boundary is fitting the training points rather than the pattern). All 200 of 200 training points became support vectors. The boundary does not follow the two rings. Instead, each training point gets its own tiny region, and almost the whole plane is assigned to one class. A very high gamma makes each point's influence extremely local, and a very high C punishes any training error. Together they memorize the training points, so the model fails on new points. Screenshot: **[FILENAME]**.

---

## Part D — More than two classes

7. In the *Multi-class* tab (linear kernel, C = 1), how many binary SVMs does **one-vs-one** train,
   and how many does **one-vs-rest** train? Report the **Middle** class's test accuracy for each
   strategy, and explain why one vs rest has trouble with the class in the middle.

   One vs one trained 6 binary SVMs (one for each pair of the 4 classes), and one-vs-rest trained 4 (one per class against all the others). The Middle class had a test accuracy of 93.0% with one vs one and 74.5% with one-vs-rest. Overall accuracy was 96.6% for one vs one and 93.4% for one vs rest. One vs rest has trouble because the Middle class lies in the center, surrounded by the other three groups, so one straight line cannot separate it from all three at once. One vs one only has to separate Middle from one class at a time, which a line can do easily, and the votes of those pairwise SVMs together mark out a small region around it. In the other classes, one-vs-rest did as well or better (for example, Top 100.0% vs 98.5%), so its problem is specific to the class in the middle.

---

## Part E — The practical case: breast-cancer diagnosis

8. In the *Second Opinion: Diagnosis* tab, with the default settings (two features: worst radius and
   worst concave points; RBF kernel; C = 1; gamma = scale), report the **accuracy, recall,
   precision, F1 score**, the number of **missed cancers** (false negatives), and the number of
   **false alarms** (false positives).

   With two features (worst radius and worst concave points), RBF kernel, C = 1, and gamma = scale, the accuracy was 93.6%, recall 92.2%, precision 90.8%, and F1 score 0.915. The model missed 5 cancers (false negatives) and raised 6 false alarms (false positives). In the confusion matrix, 101 benign patients were correctly classified. Accuracy alone hides the fact that 5 patients with cancer were told they were benign.

---

9. Switch to **All 30 features** (same kernel, C, and gamma). Report the same six values. Did the
   extra features help? Which numbers changed the most?

   With all 30 features and the same settings, accuracy was 96.5%, recall 93.8%, precision 96.8%, and F1 0.952. The model missed 4 cancers and raised 2 false alarms. The extra features helped on this test set: accuracy rose 2.9 points, recall 1.6 points, precision 6.0 points, and F1 0.037. Precision changed the most, because false alarms dropped from 6 to 2. Missed cancers only went from 5 to 4, so the improvement was mainly in fewer wrong "malignant" predictions rather than in finding more cancers.

---

10. In the grid search (with **all 30 features**), report the best C, the best gamma, and the
    cross-validation score when choosing by **accuracy**, and again when choosing by **recall**. For
    each choice, report how many cancers the model missed and how many false alarms it raised on
    the test patients. Which of the two would you rather use as a screening aid, and why? Why must
    the test patients not be used to choose C and gamma?

 - **Choosing by accuracy:** best C = 10, gamma = 0.01, mean cross-validated accuracy = 0.975. On the test patients it missed 4 cancers and raised 0 false alarms (accuracy 97.7%, recall 93.8%, precision 100.0%).
    - **Choosing by recall:** best C = 10, gamma = 0.1, mean cross-validated recall = 0.967. On the test patients it missed 2 cancers and raised 4 false alarms (accuracy 96.5%, recall 96.9%, precision 93.9%).

    As a screening aid I would use the model chosen by recall. A missed cancer can delay treatment, while a false alarm usually leads to more tests. Choosing by recall cut missed cancers from 4 to 2, at the cost of 4 extra false alarms. This is not enough to call the model ready for clinical use; the right balance would still need validation. The test patients must not be used to choose C and gamma, because then the test set would influence the model and the final numbers would be optimistic. The grid search uses cross-validation on the training patients only, and the test patients are used once at the end for the winning combination.

---

11. In the *SVM vs. Logistic Regression* tab with **All 30 features** and the default settings,
    report both models' accuracy and number of missed cancers. Which model did better on these
    patients? Then look at the **circles** example at the bottom of the tab. The lecture says SVMs
    "excel" compared with methods like logistic regression. Based on *both* results, when is that
    true, and when isn't it?

    With all 30 features and default settings, the RBF SVM had 96.5% accuracy and 4 missed cancers, and logistic regression had 97.7% accuracy and 4 missed cancers. Logistic regression did better on these patients, by 1.2 points (2 patients), all of it from fewer false alarms (0 vs. 2), since recall was the same (93.8%). With two features it was the opposite: the SVM won by 0.6 points (1 patient), 93.6% vs. 93.0%. On the circles example, logistic regression reached only 53.5% test accuracy, while the RBF SVM reached 99.8%. The lecture's claim holds when the classes need a curved boundary that a kernel can capture, as in the circles, where a straight line cannot work. It does not hold automatically when a straight boundary is already enough: on the 30 feature patient data, logistic regression matched or beat the SVM. Which model is better depends on the data and has to be checked with validation.

---

## Part F — Responsible use

12. Name one other application of SVMs mentioned in the lecture and explain why an SVM suits it. Then
    describe **two safeguards** a hospital should require before using a model like the one in this
    app to support real diagnoses.

     **Application from the lecture:** handwriting recognition. Each image of a digit or letter can be turned into a list of numbers, so the input has many features. An SVM suits this because a kernel such as RBF can draw curved boundaries between characters, as we saw with the circles in the Kernels tab, and the same character is written very differently by different people. Since there are many characters (10 digits, 26 letters), it also needs a multiclass strategy like the one vs one and one vs rest approaches from the Multi class tab.

    **Safeguard 1:** Before use, the hospital should validate the model on recent, representative data from its own patient population, not only on this 1990s research dataset, and report missed cancers and false alarms, including for different patient groups. Settings must be chosen without touching the final evaluation data.

    **Safeguard 2:** Every prediction should be reviewed by a qualified clinician alongside other evidence. The model should support the decision, never make it alone, and there should be a defined way to escalate uncertain or conflicting results, so that a "benign" prediction cannot by itself dismiss a suspicious case.

