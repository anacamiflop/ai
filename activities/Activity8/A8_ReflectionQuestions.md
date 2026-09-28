# Activity 8 — Reflection Questions: ShopSmart Assistant

Answer every question below based on your own run of the app. Submit this file separately from
your screenshots — do not just describe the app, use your actual results.

Most questions below have one exact correct answer, drawn directly from the app. Answer them
precisely — cite the exact rule ID, fact name, or value where asked.

---

1. Match each of the five expert-system components to what it is **in this specific app**:
   Knowledge base, Inference engine, User interface, Knowledge acquisition mechanisms,
   Explanation mechanisms.

- **Knowledge base:** The four IF-THEN rules listed in the knowledge Base tab (R1-R4).
- **Interference. engine:** The rule-checking logic in the "Run the Inference Engine" tab.
- **User interface:** The Streamlit app itself, where the user selects a profile and checks the rules.
- **Knowledge acquisition mechanisms:** The process used to create the four rules by business and IT expert.
- **Explanation mechanisms:** The condition-by condition trace that shows why each rule fired or did nor fire.

---

2. Fill in the blank: the IF-THEN format used by every rule in ShopSmart's knowledge base is
   traditionally called a **______ rule**.

The IF-THEN format is tradirionally called a **production rule**.

---

3. For **Profile A**, which rule(s) fire, and what is the resulting conclusion?

For Profile A, **R1 - Loyalty Discount** fires.

The conclusion is: **Offer a 10% discount on the next purchase.**

The other three rules do not fire because their conditions are not satisfied.

---

4. For **Profile B**, which rule(s) fire, and what is the resulting conclusion?

For Profile B, **R2 - Free Shipping** fire.

Conclusion: **Unlock free shipping.**, the other three rules do not fire.

---

5. For **Profile C**, does the **Account Lockout (R3)** rule fire? Name the exact condition
   (fact name and its actual value for Profile C) that determines the answer.

No, **R3 - Account Lockout does not fire**.

Profile C has **5 failed login atttempts**, so the first condition is satisfied. However, the rule also requires **IP address flagged? = False**, while the actual value is **True**.
Therefore, the IP adress flagged condition prevents R3 from firing.

---

6. For **Profile D**, how many rules fire in total? List every resulting conclusion.

**4 of 4 rules fired**.

1. **Offer a 10% discount on the next purchase**
2. **Unlock free shipping**
3. **Temporarily lock the account for security review**
4. **Trigger emergency cooling and alert IT**

---

7. For **Profile E**, how many rules fire? What does the Final Summary say?

**0 rules fire**, and the Final Summary says: **"No rules triggered - no action needed for this profile."**

---

8. True or False: ShopSmart's inference engine starts from a hypothesis (like "this account
   should be locked") and works backward to check whether the facts support it. Justify your
   answer using the term **"forward chaining"** or **"backward chaining."**

**False**, ShopSmart uses **forward chaining** because the inference engine starts with the known facts of each profile and checks the rules one by one. It does not start with a hypothesis and work backward. When all the conditions of a rule are satisfied, the sule fires and produces its conclusion.

---

10. Propose **one new IF-THEN rule**, written in the same format as R1–R4, that ShopSmart could
   add for IT, Business, or a user-experience/design concern not already covered by the
   existing four rules. State which department it belongs to.

**R5 - Low Stock Alert (Business)**

IF product_stock < 10 AND product_is_active = True THEN alert the inventory team to restock the product.
