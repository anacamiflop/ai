# Activity 16 — Reflection Questions: Customer Groups (k-means)

Answer every question using the app's **default settings**, unless a question tells you to change
something. Submit this file together with your labeled screenshots — do not just describe the app,
use your actual results.

---

## Part A — The data and the algorithm

1. **Before running anything**, look at the chart in the *Meet the Customers* tab. How many groups
   of customers do you see by eye? Describe each group in plain words (for example, "people who
   visit often but spend little").

I could distinguish **four groups** by eye:

- **Group 1 (lower left):** customers who visit only about 2 times per month and spend little per visit (around 300 MXN).
- **Group 2 (upper left):** customers who also visit rarely (about 4 times per month) but spend a lot each time (roughly 1,500 to 2,000 MXN per visit).
- **Group 3 (middle):** customers who visit fairly often (about 10 to 14 times per month) and spend a good amount per visit (roughly 1,000 to 1,500 MXN).
- **Group 4 (lower right):** customers who visit very often (about 15 times per month) but spend little each time (around 250 MXN per visit).

---

2. In the *Step by Step* tab with the default settings (k = 4, Random customers, seed 4, maximum
   iterations 30, tolerance 0), run k-means to the end. Report:
   (a) how many iterations it took,
   (b) which stopping rule stopped it, and
   (c) the final WCSS.

- (a) Iterations: **10**
- (b) Stopping rule: **convergence**. In iteration 10, 0 customers changed cluster and the largest centroid move was 0, so the centroids stopped moving.
- (c) Final WCSS: **34.82**

---

3. In your own words, explain what the **assignment step** and the **update step** do. Then look at
   the WCSS column of your iteration log: what happened to WCSS from one iteration to the next?
   Explain why it can never go up.

The assignment step puts each customer in the cluster of its nearest centroid. The update step moves each centroid to the average position of the customers assigned to it. The two steps repeat until a stopping rule is reached.

In my iteration log, WCSS never went up: 91.04, 89.88, 89.08, 87.64, 84.7, 71.3, 39.04, 34.86, 34.82 and 34.82. The same happens inside a single iteration: in iteration 1, WCSS was 108.11 after the assignment and 91.04 after the update. WCSS can never go up because assigning each customer to its nearest centroid can only keep or reduce its squared distance, and the mean of a cluster is the point that minimizes the sum of squared distances to its members. Neither step can increase the total.

---

4. Keep the default settings, but:
   (a) set **maximum iterations to 3**, and
   (b) set maximum iterations back to 30 and the **tolerance to 0.1**.

   For each run, report the stopping rule, the number of iterations, and the final WCSS. Compare
   them with your answer to Question 2. What is the risk of stopping k-means early? (Hint: look at
   the "largest centroid move" column of the full run's log.)

- **(a) Maximum iterations = 3:** the algorithm stopped because it reached the **maximum number of iterations**, before converging. It completed **3 iterations** and the final WCSS was **88.51**. The log showed 89.08 after the third update, but the app made a final reassignment of each customer to its nearest centroid, which produced 88.51.
- **(b) Tolerance = 0.1 (maximum iterations back to 30):** the algorithm stopped by the **tolerance rule**, because the largest centroid move (0.079) was no more than 0.1. It completed **2 iterations** and the final WCSS was **89.45** (the WCSS shown after the second update was 89.88, and 12 customers had changed clusters in that iteration).
- **Comparison with Question 2:** the default run stopped by convergence after **10 iterations** with a final WCSS of **34.82**. Both early runs ended with a WCSS of about 89, more than double that value.

**Risk of stopping early:** the clusters can be left unfinished. A small centroid move does not mean the algorithm is done. In the full run's log, the largest centroid moves in iterations 2 and 3 were only 0.079 and 0.075, but in iteration 6 the move rose to 0.505 and WCSS dropped from 84.7 to 71.3, and in iteration 7 it dropped to 39.04. If I had stopped after the small moves, I would have missed those big improvements.

---

## Part B — Starting centroids

5. With **Random customers** and k = 4, try different random seeds until you find one whose final
   WCSS is clearly worse than in Question 2. Report the seed and its final WCSS, include a
   screenshot, and describe what went wrong (look at where the centroids ended up).

- Seed: **8**
- Final WCSS: **387.35** (vs. **34.82** in Question 2)

What went wrong: three of the four starting centroids landed in the same group (occasional, low-spending customers in the lower left), so that natural group was split into three small clusters of 36, 28 and 32 customers. The fourth centroid ended in the middle of the chart and absorbed 204 customers from the three other natural groups. k-means cannot fix this on its own, because each centroid only moves to the mean of its own customers and cannot jump to another part of the chart.

---

6. In the *Restarts* tab (k = 4, 20 runs), report:
   (a) the best WCSS found,
   (b) how many random starts reached it,
   (c) how many k-means++ starts reached it, and
   (d) the worst random-start WCSS.

   The lecture says that when k-means converges, it "has reached an optimal and stable result."
   Every one of these runs converged. Based on your numbers, is the lecture's statement completely
   true? Explain.

- (a) Best WCSS found: **34.82**
- (b) Random starts that reached it: **11 of 20**
- (c) k-means++ starts that reached it: **17 of 20**
- (d) Worst random-start WCSS: **387.35** (seed 8)

Is the lecture's statement completely true? No. All the runs converged, but they did not all reach the same result: some stabilized near 90 and the worst reached 387.35, more than 11 times the best. Convergence means assignments and centroids became stable, but the algorithm can stop at a local minimum rather than the global optimum. That is why it is worth running several restarts and keeping the lowest WCSS. k-means++ was more reliable (17 of 20 vs. 11 of 20), but it did not reach the best result every time either.

---

7. Choose **Pick my own** and deliberately choose 4 bad starting customers. Report the 4 customer
   numbers you chose and the final WCSS, include a screenshot of the final clusters, and describe
   what the final clusters got wrong.

- Starting customers I chose: **4**
- Final WCSS: **34.82**


What the final clusters got wrong: A natural group split into several clusters while other groups were merged into one cluster.

---


## Part C — Choosing k and making business decisions

8. In the *Choosing k & Segments* tab, which k does the **elbow method** suggest, and which k does
   the **silhouette score** suggest? Do they agree with your guess in Question 1?
   
- Elbow method suggests **k = 4**: WCSS falls sharply up to k = 4 and then flattens.
- Silhouette score suggests **k = 4**: it has its highest value at k = 4 (about 0.75).
- Both methods **agree with my guess in Question 1**, where I distinguished four groups by eye. The elbow and the silhouette score confirm that four is a good number of segments for this data.

---

9. In the segment report with k = 4:
   (a) give each cluster a business name,
   (b) say which cluster brings in the largest share of total monthly revenue, and report that
   cluster's share of customers and its share of revenue, and
   (c) propose one specific marketing action for each cluster.

**(a) and (c) Names and marketing actions:**

- **Cluster 1: "Occasional budget shoppers"** (95 customers, 32%). They visit about 2.1 times per month and spend about 313 MXN per visit. *Action:* send a discount coupon for a second purchase within the same month to encourage another visit.
- **Cluster 2: "Frequent budget shoppers"** (81 customers, 27%). They visit about 15.1 times per month but spend only about 241 MXN per visit. *Action:* offer discounted bundles of related products to raise the amount they spend on each visit.
- **Cluster 3: "Occasional premium shoppers"** (71 customers, 24%). They visit about 3.9 times per month and spend about 1,653 MXN per visit. *Action:* send personalized premium product recommendations and reminders about new collections to bring them back more often.
- **Cluster 4: "Frequent premium shoppers"** (53 customers, 18%). They visit about 11.1 times per month and spend about 1,258 MXN per visit. *Action:* offer VIP early access to new products and priority service to reward them and keep them from leaving.

**(b) Largest share of revenue:** **Cluster 4** ("Frequent premium shoppers") brings in the largest share of total monthly revenue. It represents only **18%** of customers but generates about **48%** of monthly revenue **[verify the exact percentage in the app's report before submitting]**. Cluster 4 earns far more than its share of customers because it combines frequent visits with a high spend per visit. In contrast, Cluster 1 is the biggest group (32% of customers) but contributes only a small fraction of revenue.

---
## Part D — Limits of k-means

10. In the *Where k-means Fails* tab, for **each** of the two datasets, report the percentage of
    points k-means put in their true group, the WCSS of k-means' answer, and the WCSS of the true
    groups. What does comparing the two WCSS values tell you about *why* k-means fails on these
    datasets?

**Two moons (non-spherical groups):**
- Points k-means put in their true group: **75.0%**
- WCSS of k-means' answer: **121.2**
- WCSS of the true groups: **182.1**

**One big group, two small ones (different sizes and densities):**
- Points k-means put in their true group: **81.1%**
- WCSS of k-means' answer: **1051.8**
- WCSS of the true groups: **1345.6**

**What the WCSS comparison means:** in both datasets, the WCSS of k-means' answer is **lower** than the WCSS of the true groups. So k-means did exactly what it is built to do: it found a partition that is better for its own objective, minimizing the sum of squared distances to the centroids. It "fails" because that objective favors compact, round clusters of similar size, which does not match the real structure of these data. In the two moons, each group is curved, so k-means cuts them with a straight boundary and 25% of the points end up in the wrong group. In the second dataset, the big, spread-out group is split (k-means put 228 points in one cluster, while the true big group has 300) and some of its points are grouped with the small ones. The problem is the mismatch between the objective and the true groups, not too few iterations or a bad starting point.

---

## Part E — Another application

11. In the *Bonus: Photo Compression* tab, with the coffee photo (k-means++, seed 0), report the
    bits per pixel and the uncompressed size for **k = 4, 16, and 32**, along with the original's
    size. What is the smallest k at which the photo still looks acceptable to you, and why?

The original photo is 600 x 400 pixels, uses **24 bits per pixel** and has an uncompressed size of **703 KB**.

- **k = 4:** **2 bits per pixel**, uncompressed size **59 KB** (average error per color 19.7).
- **k = 16:** **4 bits per pixel**, uncompressed size **117 KB** (average error per color 8.4).
- **k = 32:** **5 bits per pixel**, uncompressed size **147 KB** (average error per color 5.8).

**Smallest acceptable k: 16.** With k = 4 the photo looks like a poster: the gradients on the wooden table and in the coffee disappear, and the reflection on the spoon is lost. With k = 16 the cup, the coffee foam, the wood grain and the spoon's shine are all recognizable, and the average error per color drops from 19.7 to 8.4. Going to k = 32 improves the error only a little more (5.8) while the size grows from 117 KB to 147 KB. So k = 16 is the best balance: the photo is about 6 times smaller than the original (117 KB vs. 703 KB) and still looks good to me.

**Optional: my own photo.** I also uploaded my own photo (a bridge over a river, 600 x 338 pixels) and used k = 20 with k-means++ and seed 0. It used **5 bits per pixel**; the original's uncompressed size was **594 KB** and the 20-color version was **124 KB (4.8x smaller)**, with an average error per color channel of **7.8**. k-means converged after 34 iterations. The buildings and the bridge still look good, but the sky shows visible bands, because it is a smooth gradient that gets split into a few flat blue tones, and the dark water and shadows lose some detail. This tells me the number of colors needed depends on the photo: images with large smooth gradients, like a clear sky, need more colors than very textured images.

---

12. Describe **one other real-world use of k-means** (not customers or photos). What would each data
    point be, which features would you cluster on, how would you choose k, and what would you do
    with the clusters once you had them?

A real use of k-means is **grouping bike-share stations** to manage how bikes are redistributed during the day.

- **What each data point is:** one bike-share station.
- **Features:** average number of bikes taken out per hour in the morning, average number of bikes returned per hour in the morning, the same two numbers for the afternoon, and the percentage of trips that happen on weekends. I would standardize all the features so that none of them dominates the distances just because of its units.
- **How I would choose k:** I would run k-means for several values of k (for example 2 to 10) and compare the elbow curve and the silhouette score, as in this activity. I would also check that the groups make sense for the operations team, because they can only handle a small number of different schedules.
- **What I would do with the clusters:** each cluster would get its own rebalancing plan. For example, stations that empty out in the morning (near residential areas) would get bikes delivered before the morning rush, stations that fill up (near offices) would have bikes collected and moved elsewhere, and stations with low use all day could get fewer docks or fewer visits from the trucks. This saves truck trips and reduces the number of stations that are empty or full when users need them.

