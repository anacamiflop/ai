# Activity 7 — Reflection Questions: YucaExpress Route Challenge

Answer every question below based on your own run of the app. Submit this file separately from
your screenshots — do not just describe the app, use your actual results.

**Remember: elaborate your answers.** A correct one-word answer with no explanation will not
receive full credit on the interpretive questions.

---

1. What is the **initial state** and the **goal state** in this activity?

The initial state is **Depot**, where the courier starts the delivery.

The goal state is **Client Office**, which is the final delivery destination.

---

2. What route did **Greedy Best-First** take (list every junction, in order), and what was its
   **total distance driven**?

Greedy Best-First Search found this route:

**Depot - Hub Norte - Parque Cruce - Retorno del Lago - Client Office**

Total distance: **19.34 km**.

---

3. What route did **A\*** take (list every junction, in order), and what was its **total
   distance driven**?

A* found this route:

**Depot - Hub Sur - Anillo Periferico - Circuito Sur - Client Office**

Total distabce: **11.23 km**.

A* uses the evaluation dunction which is:

**f(n) = g(n) + h(n)**

Where g(n) is the real distance already driven and h(n) is the straight-line estimate to the goal.

---
4. One road in this map costs noticeably more than the straight-line distance between its two
   junctions would suggest. Name that road (its two endpoints) and report both its real cost
   and the straight-line distance between those same two junctions.

One example os the one from **Retorno del Lago to Client Office**

- Real road distance **9.49 km**.
- Straight-Line distance: **3.16 km**.

The difference is significant because the road distance is much longer than the straight-line estimate.

---

5. Which algorithm found the cheaper overall route, and by how many kilometers?

A* found the cheaper route.

Greedy Best-First Search traveled **19.34 km**, while A* traveled **11.23 km**.

The difference is:

**19.34 - 11.23 = 8.11 km**

Therefore, the A* route was **8.11 km shorter** than the Greedy route.

---

6. In your own words, explain **why** Greedy Best-First got misled into a more expensive route
   while A\* did not. Use the terms **g(n)** and **h(n)** somewhere in your answer.

Greedy got misled because it only looked at h(n), which is the straight-line distance to the Client Office. For example, it chose Retorno del Lago because its h(n) was only 3.16 km, so it looked like it was very close to the goal. However, the actual road from there to the Client Office was 9.49 km.

A* worked differently because it looked at both g(n) and h(n). The g(n) showed how much distance had already been driven, while h(n) estimated the distance that was left. By adding both values with f(n) = g(n) + h(n), A* was able to avoid the route that looked close but was actually longer. That is why A* found the shorter route of 11.23 km.

---

7. Name one **real business or logistics scenario** where blindly chasing whatever "looks
   closest to the goal" — without accounting for the real cost already spent — could backfire,
   similar to Greedy's mistake here.

One example could be a delivery company choosing the warehouse that looks closest to a customer on a map.

The closest warehouse in a straight line may have traffic, blocked roads, one-way streets, or a difficult route. Another warehouse that looks farther away could have a much faster or shorter actual driving route.

This is similar to the YucaExpress example because the closest point according to the heuristic was not necessarily the cheapest route in terms of real road distance.

---

8. Suppose the heuristic in this app sometimes *overestimated* the true remaining distance
   instead of always underestimating it. Would A\* still be guaranteed to find the cheapest
   route? Why or why not?

No. A* is not guaranteed to find the cheapest route if the heuristic overestimates the true remaining distance.

For A* to guarantee the cheapest route, the heuristic should be **admissible**, meaning that it should not overestimate the actual remaining cost.

If h(n) overestimates the remaining distance, A* could incorrectly consider a good route too expensive and choose another route instead.
