# Activity 6 — Reflection Questions: Six Degrees to Katún

Answer every question below based on your own run of the app. Submit this file separately from
your screenshots — do not just describe the app, use your actual results.

**Remember: elaborate your answers.** A correct one-word answer with no explanation will not
receive full credit on the interpretive questions.

---

1. What is the **initial state** and the **goal state** in this activity?

The initial states is **You**, because the search starts from my position in the professional network.

The goal state is **Elena Ruiz**, because she is the person I am trying to reach in order to get a meeting with the CFO of Group Katún.

---

2. List, in order, every person BFS **processed** (took from the front of the line) before
   reaching Elena Ruiz. How many people did it process in total?

1. You
2. Marco Aguilar
3. Sofia Torres
4. Valentina Cruz
5. Roberto Kim
6. Camila Duarte
7. Javuer Mendez
8. Ana Beltran

Therefore, BFS processed a total of **9 people before reaching Elena Ruiz**.

Elena Ruiz was reached when Ana Beltran was processed, so Elena was not processed herself. The research stopped immediately after Elena was found.

---

3. Name the one contact who had **no new introductions** to offer when BFS reached them. Based
   on the network, explain in one sentence why not.

In my run, **two contacts had no new introductions to offer: Diego Torres and Roberto Kim**.

Diego Torres only knew people who had already beedn reached by BFS, so he did not add any new conatcts. Roberto Kim also knew people who had already been reached, so he did not add any new contacts either.

---

4. What is the exact **shortest chain of introductions** from You to Elena Ruiz, and how many
   introductions (hops) does it take?

**You - Marco Aguilar - Valentina Cruz - Cmila Duarte - Javeir Mendez - Ana Beltran - Elena Ruiz**

This chain takes 6 introductions, because BFS explores the network kevek by level, the applicaition guarantees that this is the fewest possible number of introductions.

---

5. According to the "What would last session's DFS have done here?" comparison, how many
   introductions would DFS have needed on this exact same network? Is that more, fewer, or the
   same as BFS's result?

**You - Marco Aguilar - Valentina Cruz - Sofia Chan - Roberto Kim - Camila Duarte - Javier Mendez - Elena Ruiz**

BFS needes **6 introductions**, while DFS needes **8 introductions**. DFS found a valid path, but it was not the shortest path.

---

6. In your own words, explain why BFS is **guaranteed** to find the shortest chain of
   introductions, while DFS is not. Use the words **"line" (or "queue")** and **"stack"**
   somewhere in your answer.

Because BFS esplores the networl level by level, while DFS uses a stack which follows a path as deeply as possible before going back and exploring othe path.

---

7. Name one **real business scenario** (other than this one) where finding the *fewest-hops*
   connection matters more than just finding *any* connection at all — for example, referral
   chains, supply-chain routing, or an approval/escalation chain. Briefly explain why the
   fewest-hops answer specifically matters there.

For example, an approval process in a company because if an employee needs an urgent approval form a senior manger, finding the shortest chain of people who can connect the employee to the final decision-maker is important. A shorter chain means fewer people need to be contacted, which can reduce communication time and help the decision be made faster. Therefore, finding the connection with the fewest hops is more useful than simply finding any possible connection.
