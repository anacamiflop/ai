# Activity 15 — Reflection Questions: Digit Lab

Answer every question below using the **canonical network** and the app's default values, unless a
question specifically asks about your own Training Lab runs or drawings. Submit this file together
with your labeled screenshots — do not just describe the app, use your actual results.

---

## Part A — Representation (Session 25)

1. How many neurons does the canonical network have in its **input layer**, its **hidden layer**,
   and its **output layer**? Explain why the input layer has exactly that many neurons, and why
   the output layer has exactly 10.

- The input layer has 784 neurons because an MNIST image is 28 × 28 pixels, and the network gets one neuron per pixel: 28 × 28 = 784. The 2-D image is flattened into a list of 784 numbers (the brightness of each pixel).
  
- The output layer has 10 neurons because there are 10 possible answers (the digits 0–9). Each output neuron holds the probability of one digit, and softmax makes the ten probabilities add up to 100%.
  
- The hidden layer (64 neurons, sigmoid activation) is a design choice, not fixed by the problem.

---

2. Report the canonical network's number of **trainable parameters**, and show how that number is
   computed from the layer sizes (weights + biases between each pair of layers).

The network has **50,890** trainable parameters.

- Input → hidden: 784 × 64 = 50,176 weights + 64 biases = **50,240**
- Hidden → output: 64 × 10 = 640 weights + 10 biases = **650**
- Total: 50,240 + 650 = **50,890**

---

3. Report the canonical network's **train accuracy, test accuracy, train loss, and test loss**.

The canonical network has a train accuracy of 97.2%, a test accuracy of 94.1%, a train loss of 0.106, and a test loss of 0.201. The train-test accuracy gap is 3.1 percentage points.

---

4. Choose **one hidden neuron** from "What did the hidden neurons learn?" (include its screenshot).
   Describe what kind of shape or stroke it seems to respond to. Nobody programmed that pattern —
   so where did it come from?

I chose **Neuron 2**. Its picture is dominated by two dark-blue curved strokes: a thick arc at the lower left that curves like a smile, and a shorter arc at the upper right, together forming a wave / S-like shape. Around them there is faint red and the rest is almost white. Since red means "ink here makes the neuron fire" and blue means "ink here keeps it quiet", this neuron is switched off when those two arcs are inked, and it is more active when ink is in the faint red areas and those arcs are empty. So it acts like a detector of "curve here, not there" that helps tell digits apart; I can't say it recognizes one specific digit.

Nobody programmed this pattern. The 784 weights of the neuron started as small random numbers. During training, back-propagation changed each weight many times, using the 6,000 labeled images, to reduce the error. The weights that helped separate the digits were pushed up or down, and after 10 epochs they ended up forming this shape.

## Part B — Back-propagation (Session 26)

5. In the Back-propagation tab with the default learning rate of 0.50, report:
   (a) the network's output **o** before the update,
   (b) the error **E** before the update,
   (c) the new value of weight **w5** after the update, and
   (d) the error **after one update**.

The update lowered the error by 0.0108 (0.1053 → 0.0945).

6. In your own words, explain what the **backward pass** (steps 3 and 4) does and why the
   algorithm is called *back*-propagation. Use the deltas you saw (δo, δh1, δh2) in your
   explanation.

The forward pass goes from the inputs to the output, and the network answered o = 0.5411 when the target was 1.0, so the answer was too low. The backward pass goes the other way, from the output back toward the inputs, and that is why it is called back-propagation.

It starts with the output delta, δo = −0.1140, which says how much and in which direction the output neuron has to change. That delta is then sent back to the hidden neurons through the weights that connect them to the output (w5 and w6), multiplied by each neuron's sigmoid slope. That gave δh1 = −0.0138 and δh2 = +0.0169, so each hidden neuron gets its own small share of the blame. They have opposite signs because w5 is positive and w6 is negative.

Then each weight's gradient is the delta of the neuron it feeds into times the value that travels through it (for example, gradient of w5 = δo · h1 = −0.0671). The weight changes with new = old − 0.5 · gradient, so w5 went from 0.5 to 0.5336. A negative gradient makes the weight go up, a positive one makes it go down, and a bigger gradient means a bigger change.

---

7. Paste your Training Lab **run-history table** (at least 4 runs: defaults, a learning rate that
   is too low, one that is too high, and "all zeros" initial weights). For the too-low and too-high
   runs, describe what the loss and accuracy curves looked like and why that learning rate caused
   it.

I trained 5 runs, all with 1 hidden layer of 64 neurons, sigmoid activation, 10 epochs and batch size 32:

- Run 1 (defaults): learning rate 0.5, small random weights. Train accuracy 97.2%, test accuracy 94.1%. It shows "+0.0 pts vs canonical" and 50,890 parameters, so it is exactly the canonical network (`05_run1_defaults.png`).
- Run 2 (learning rate too low): learning rate 0.001, small random weights. Train accuracy 56.6%, test accuracy 55.4%.
- Run 3 (learning rate too high): learning rate 10, small random weights. Train accuracy 74.6%, test accuracy 73.9%.
- Run 4: the same settings as Run 3 (learning rate 10), and it gave exactly the same result, 74.6% and 73.9%. This confirms that the same settings always give the same result.
- Run 5 (all zeros): learning rate 0.5, all zeros initial weights. Train accuracy 36.4%, test accuracy 35.5%.

---

8. What happened when you trained with **"all zeros"** initial weights? Why can't a network learn
   well if every weight starts at exactly the same value? (Think about what each hidden neuron
   computes when all of them have identical weights.)

The network does learn something, but very little. If every weight starts at exactly the same value, all 64 hidden neurons compute exactly the same thing for every image, so they receive exactly the same gradient and get exactly the same update. They stay identical forever (a "symmetry" that never breaks), so the 64 neurons behave like a single neuron repeated 64 times and the hidden layer cannot learn 64 different patterns. Random initial weights make each neuron start different, so each one can specialize in a different stroke or shape.

---

9. What was the **best test accuracy** you found, and with which settings? Did making the network
   bigger (more neurons or a second layer) or training longer (more epochs) *always* improve the
   test accuracy? Use the **train − test gap** from your runs to explain what you observed.

My best test accuracy was **94.1%** (train 97.2%, gap 3.1 points), from **Run 1**: 1 hidden layer, 64 neurons, sigmoid, learning rate 0.5, 10 epochs, batch size 32, small random initial weights. It can be reproduced with those settings (it is the canonical network).

Does bigger or longer always help? Looking at the gaps in my runs, no, and the train − test gap is a better guide than the training accuracy alone:

- The runs with the smallest gaps (Run 3: 0.7, Run 5: 0.9, Run 2: 1.2) are not the best runs. Their gaps are small because they are *underfit* (too low a learning rate, too high a learning rate, or zero weights): the network is bad on both train and test.
- My best run has the largest gap (3.1 points), and in its curves the train loss keeps falling to 0.106 while the test loss levels off near 0.2, and test accuracy moves only slowly (about 91% at epoch 2 to 94.1% at epoch 10), while train accuracy keeps climbing (97.2%). This is the start of overfitting: extra capacity or extra epochs can keep improving the train score without improving the test score, and the gap would keep growing.

So better results come from good settings (learning rate, initial weights) first. More neurons or more epochs help only while the test accuracy also improves; once the gap grows and test accuracy stalls, bigger or longer only memorizes the training images more.

---

## Part C — Applications (Session 27)

10. For test images **#24, #4, and #6**, report the true label, the canonical network's
    prediction, and its confidence. Then report how many of the 1,000 test images the canonical
    network gets wrong.

- Test image #24: the true label was 7 and the canonical network predicted 7 with 100.0% confidence. It was correct.
- Test image #4: the true label was 4 and the canonical network predicted 4 with 85.9% confidence. It was correct.
- Test image #6: the true label was 9, but the canonical network predicted 4 with 56.0% confidence. It was wrong. It gave 30.0% to 6 and only 1.0% to the true label 9.

The canonical network gets **59 of the 1,000 test images wrong**: its test accuracy is 94.1%, so 941 are correct and 1,000 − 941 = 59 are wrong.

---

11. Describe the results of your **own drawings** (at least 3): which digits did you draw, and
    what did the network answer each time? Give at least one reason why your drawings can be
    harder for this network than the MNIST test images, even though they look perfectly clear to a
    human.

I drew three digits: a 1, a 9 and a 2. The canonical network answered 1 with 94.7% confidence for my 1, 9 with 93.4% confidence for my 9, and 2 with only 57.5% confidence for my 2 (it gave 29.9% to 1 and 7.5% to 3). So it got all three right, but it was much less sure about the 2. For comparison, the Training Lab network from my last run (all zeros) answered 1 (77.6%), 9 (37.1%) and 9 (42.0%), so it got my 2 wrong.

My drawings can be harder than the MNIST test images even though they look clear to a human, because they are different from the images the network learned from. My strokes are thicker and very uniform, and the size, slant and position of my digits are different. Also, shrinking the drawing to 28 × 28 pixels changes details: for example, my 9 has a square closed loop with a straight tail, and in the 28 × 28 version the loop becomes a small box with a dark hole. The network only knows pixel patterns similar to its 6,000 training examples, so a style it has not seen makes it less sure.

---

12. Choose **one application area** from Session 27 (for example medical diagnosis, industrial
    quality control, autonomous driving, finance, agriculture, or education). Describe a neural
    network for it: what would its **inputs** be, what would its **outputs** be, and what is one
    real risk if it makes a wrong prediction, like the canonical network does on image #6?

**Agriculture — detecting crop disease from leaf photos.** The *inputs* would be the pixel values (red, green and blue) of a photo of a leaf taken with a farmer's phone, like the 784 pixel values in this activity but larger and in color. The *outputs* would be one probability per class, for example "healthy", "leaf rust", "blight" and "pest damage", using softmax so the probabilities add up to 100%. A real risk of a wrong prediction is calling a diseased plant "healthy": the farmer would not treat it, the disease could spread through the whole field and the harvest and income would be lost. The opposite error (calling a healthy plant "diseased") would waste money on pesticide. As with test image #6, where the network was wrong with 56.0% confidence, the system can look confident and be wrong, so low-confidence or high-stakes cases should be checked by an agronomist.

