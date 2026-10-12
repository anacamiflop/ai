# Activity 12 — Reflection Questions: Mérida Homes

Answer every question below using the **Canonical Model** sections only (not the playground).
Submit this file separately from your screenshots — do not just describe the app, use your
actual results.

---

1. Report the **Canonical One-Variable Model's** slope, intercept, R², and MSE.

* **Slope (w):** `8.621`
* **Intercept (b):** `55.18`
* **R²:** `0.9187`
* **MSE:** `28,827.8`

---

2. Report the **Canonical Multi-Variable Model's** four coefficients (size, bedrooms, age,
   distance), intercept, R², and MSE.

* **Coefficient - Size (m²):** `8.15`
* **Coefficient - Bedrooms:** `35.54`
* **Coefficient - Age (years):** `-9.27`
* **Coefficient - Distance to downtown (km):** `-14.29`
* **Intercept (b):** `333.17`
* **R²:** `0.9693`
* **MSE:** `10,880.2`

---

3. Which canonical model has the **higher R²** — one-variable or multi-variable — and what is
   the exact difference between the two R² values?

The **multi-variable model** has the higher R² (`0.9693` vs `0.9187`).  
The exact difference is **0.0506** (`0.9693 - 0.9187 = 0.0506`).

---

4. Using the **Canonical One-Variable Model's** prediction tool, what is the predicted price for
   a 150 m², 3-bedroom, 5-year-old house located 4 km from downtown?

The predicted price is **1,348.3 thousand MXN** ($1,348,300 MXN).

---

5. Using the **Canonical Multi-Variable Model's** prediction tool, what is the predicted price
   for that exact same house?

The predicted price is **1,559.3 thousand MXN** ($1,559,300 MXN).

---

6. Which canonical model predicts a **higher price** for that house, and what is the exact
   dollar (thousands of MXN) difference between the two predictions?

The **multi-variable model** predicts a higher price.  
The exact difference between the two predictions is **211.0 thousand MXN** (`1,559.3 - 1,348.3 = 211.0 thousand MXN` / $211,000 MXN).

---

7. In the Dataset tab, which single feature appears to have the **strongest visual relationship**
   with price?

**Size (m²)** (el tamaño de la casa). En el diagrama de dispersión (*scatter plot*), los puntos muestran una tendencia lineal ascendente muy marcada y agrupada con respecto al precio.

---

8. True or False: increasing the number of features used in a regression model can never
   *decrease* R² on the same training data it was fit on. Briefly justify your answer.

**True.** En la regresión lineal sobre el mismo conjunto de datos de entrenamiento, incluir más variables explicativas nunca reduce el R². Como mínimo, los coeficientes de las variables adicionales se ajustarán a cero (manteniendo el R² igual), o bien explicarán varianza adicional incrementando el valor del R².

---

9. In the One-Variable tab's playground, report **one learning rate** that caused the model to
   diverge (the warning appeared) and **one learning rate** that trained successfully (no
   warning).

* **Learning rate that caused divergence:** `1.0` (o superior).
* **Learning rate that trained successfully:** `0.3` (o `0.1`).
