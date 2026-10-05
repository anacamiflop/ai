# Activity 10 — Reflection Questions: SmartWash Fuzzy Controller

Answer every question below based on your own run of the app. Submit this file separately from
your screenshots — do not just describe the app, use your actual results.

**Remember: elaborate your answers.** A correct one-word answer with no explanation will not
receive full credit on the interpretive questions.

---

1. List the **four steps** of the fuzzy reasoning pipeline, in order, and briefly describe what
   each one does.

The four steps of the fuzzy reasoning pipeline are:

1. **Fuzzification:** The controller takes the exact input values, such as load size and dirtiness, and converts them into membership degrees between 0 and 1. An input can belong to more than one fuzzy term at the same time.

2. **Inference:** The controller applies the IF-THEN rules to the membership degrees. The strength of each rule is determined by taking the minimum value of the membership degrees in its conditions.

3. **Aggregation:** The controller combines the results of all the rules that produce the same output term. The strongest rule for each output term is used.

4. **Defuzzification:** The aggregated fuzzy output is converted into one precise wash time in minutes. SmartWash uses the weighted-average method to obtain the final value.

---

2. For **P1** (small load, light dirt), report the Load and Dirt membership degrees for every
   term, and the final wash time.

For P1, the Load Size is 1 kg and the Dirtiness is 1. The Load membership degrees are Small = 0.8, Medium = 0.2, and Large = 0.0. The Dirt membership degrees are Light = 0.8, Moderate = 0.2, and Heavy = 0.0.

   The resulting aggregated output strengths are Short = 0.8, Medium = 0.2, and Long = 0.0. Using these values, the final wash time is **21.0 minutes**.

---


3. For **P2** (right in the middle), which single rule fires, at what strength, and what is the
   final wash time?

For P2, the only rule that fires is **IF Load = Medium AND Dirt = Moderate THEN Time = Medium**. Its firing strength is **1.0**, since both the Medium load membership and Moderate dirt membership are 1.0.

   The aggregated output is Medium = 1.0, while Short = 0.0 and Long = 0.0. Therefore, the final wash time is **45.0 minutes**.

---

4. For **P3** (large load, heavy dirt), list every rule that fires (strength greater than 0)
   and report the final wash time.

For P3, the Load Size is 9 kg and the Dirtiness is 9. Four rules fire:

   - **IF Load = Medium AND Dirt = Moderate THEN Time = Medium**, with a strength of 0.2.
   - **IF Load = Medium AND Dirt = Heavy THEN Time = Long**, with a strength of 0.2.
   - **IF Load = Large AND Dirt = Moderate THEN Time = Long**, with a strength of 0.2.
   - **IF Load = Large AND Dirt = Heavy THEN Time = Long**, with a strength of 0.8.

   After aggregation, the output strengths are Short = 0.0, Medium = 0.2, and Long = 0.8. The final wash time is **69.0 minutes**.

---

5. **P4** and **P5** land on the exact same wash time. Report both profiles' aggregated
   Short/Medium/Long output strengths and confirm they match.

For P4, which has a Load Size of 2 kg and Dirtiness of 8, the aggregated output strengths are:

   - Short = 0.4
   - Medium = 0.6
   - Long = 0.4

   For P5, which has a Load Size of 8 kg and Dirtiness of 2, the aggregated output strengths are:

   - Short = 0.4
   - Medium = 0.6
   - Long = 0.4

   Therefore, the aggregated strengths are exactly the same for both profiles. Both produce a final wash time of **45.0 minutes**.

---

6. In your own words, explain **why** P4 (small load, heavy dirt) and P5 (large load, light
   dirt) end up at the same wash time. What does this tell you about how load size and
   dirtiness "trade off" against each other in this controller?

P4 has a small load but a high level of dirtiness, while P5 has a large load but a low level of dirtiness. In P4, the small load tends to reduce the required washing time, but the heavy dirt increases it. In P5, the large load increases the required washing time, while the light dirt decreases it.

   Even though the inputs are different, the fuzzy rules balance these effects in such a way that both profiles produce the same aggregated strengths: Short = 0.4, Medium = 0.6, and Long = 0.4. Because the aggregated outputs are identical, both profiles result in a wash time of 45.0 minutes.

   This shows that load size and dirtiness can compensate for each other in the controller. A smaller load that is very dirty can receive the same washing recommendation as a larger load that is relatively clean.

---

7. The defuzzification method used in this app is one of three named in the course material.
   Name it, and state the three reference values (in minutes) it uses for Short, Medium, and
   Long.

The app uses **weighted-average defuzzification**. The reference values are:

   - **Short = 15 minutes**
   - **Medium = 45 minutes**
   - **Long = 75 minutes**

   The aggregated strength of each output is multiplied by its corresponding reference value, and the results are divided by the sum of the aggregated strengths.
   
---

8. Name one **real-world device or system** (other than a washing machine) where fuzzy logic
   would be a natural fit. Briefly describe what its inputs and output would be.

A **smart irrigation system** would be a good real-world application of fuzzy logic. Its inputs could be soil moisture and outdoor temperature, with categories such as Dry, Moderate, Wet, Cool, Warm, and Hot. Its output could be the amount of time that the irrigation system should water.

   For example, if the soil is very dry and the weather is hot, the system could increase the watering time. If the soil is already moist and the weather is cool, it could reduce the watering time. Fuzzy logic would allow the system to make gradual decisions instead of using only strict thresholds.
