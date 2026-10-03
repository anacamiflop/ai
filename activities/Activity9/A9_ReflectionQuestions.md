# Activity 9 — Reflection Questions: Pack for the Trip

Answer every question below based on your own run of the app. Submit this file separately from
your screenshots — do not just describe the app, use your actual results.

**Remember: elaborate your answers.** A correct one-word answer with no explanation will not
receive full credit on the interpretive questions.

---

1. What is the bag's weight limit, and how many total possible packing combinations exist for
   8 items?

The bag's weight limit is **8 kg**. Since there are 8 items and each item can either be included or not included, there are:

**2^8 = 256 possible packing combinations.**

---

2. What is the **true optimal packing** (list the items) and its total value, according to the
   brute-force check?

The true optimal packing is:

- Laptop
- Charger
- Camera
- Client Gift

The total weight is **8 kg** and the total usefulness value is **29**.

The brute-force check confirmed that this is the best possible combination among all **256 possible combinations**.

---

3. What is **Generation 1's** best-in-generation fitness, and which items does that packing
   plan contain?

In **Generation 1**, the best-in-generation fitness was **24**.

The packing contained:

- Laptop
- Camera
- Client Gift

The total weight was **7 kg** and the total usefulness value was **24**, so the combination was within the 8 kg limit.

---

4. At which generation does **"Best-ever"** first reach its final value, and what is that
   value?

**Best-ever first reached its final value in Generation 6**, with a value of **29**.

In that generation, the algorithm found the combination:

- Laptop
- Charger
- Camera
- Client Gift

This packing has a total weight of **8 kg** and a usefulness value of **29**.

---

5. Did the Genetic Algorithm find the true optimal packing? If yes, say at which generation it
   was first found; if no, report the exact gap between the algorithm's best-ever value and the
   true optimum.

Yes, the Genetic Algorithm found the **true optimal packing**.

It was first found in **Generation 6**, with a value of **29**. This matches the true optimum found by the brute-force check, so there is **no gap** between the Genetic Algorithm's result and the optimal solution.

---

6. Find one generation where **"Best in Generation"** is *lower* than **"Best-ever."** Name that
   generation, and explain in one sentence why that's possible for this particular kind of
   genetic algorithm (non-elitist).

**Generation 9** is an example because:

- Best in Generation = **26**
- Best-ever = **29**

This can happen because the Genetic Algorithm is **non-elitist**. This means that the best solution from a previous generation is not necessarily kept in the next population.

For example, in Generation 9, the best solution had a value of 26, while the algorithm still remembered that it had previously found a solution with a value of 29. Therefore, **Best-ever stays at 29 even though the current generation's best solution is only 26**.

---

7. In your own words, explain what **crossover** and **mutation** each contribute to a genetic
   algorithm's ability to find good solutions, using this packing problem as your example.

**Crossover** combines parts of two existing solutions to create a new packing plan. For example, one solution might contain the Laptop and Camera, while another contains the Charger and Client Gift. Crossover can combine useful parts from both solutions and potentially create a better packing combination.

**Mutation** makes a small random change to a solution, such as adding or removing one item. In this problem, mutation could help the algorithm discover a combination that it had not previously tried, such as the optimal combination of the Laptop, Charger, Camera, and Client Gift.

Together, crossover and mutation help the population explore different combinations instead of staying with the same solutions.

---

8. Name one **real business, IT, or design scenario** (other than packing a suitcase) where a
   genetic algorithm would be useful instead of just checking every possible option by brute
   force. Briefly explain why brute force wouldn't work well there.

A Genetic Algorithm could be useful for **employee scheduling in a company**. The algorithm could create schedules while considering employee availability, working hours, required skills, and business needs.

Brute force would not work well because the number of possible schedules would become extremely large as the number of employees and shifts increases. A Genetic Algorithm can search through many possible solutions and find a good schedule without having to check every possible combination.
