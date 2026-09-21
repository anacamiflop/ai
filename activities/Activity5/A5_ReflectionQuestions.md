# Activity 5 — Reflection Questions: The Whispering Cave

Answer every question below based on your own exploration in the app. Submit this file
separately from your screenshots — do not just describe the app, use your actual results.

**Remember: elaborate your answers.** A correct one-word answer with no explanation will not
receive full credit on the interpretive questions.

---

## Part 1 — Facts, Rules, and Recursion (Session 10)

1. Write out one `tunnel(X, Y)` fact directly from the Tunnel Rules tab (any one you like), and
   report whether `reachable(Entrance, Treasure Room)` came back **TRUE** or **FALSE** when you
   asked the Oracle.
**Answer** One tunnel`(X,Y)` fact from the Tunnel Rules tab is:
`tunnel(bat_roost, entrance).`
When I asked the Oracle whether `reachable(Entrance, Treasure Room)` was possible, the result was **TRUE**. This means that there is a route from the Entrance to the Treasure Room. The Oracle explored the tunnelsand eventually found a route that reached the Treasure Room.

   
2. The rule is: `reachable(X, Y) :- tunnel(X, Y).` and `reachable(X, Y) :- tunnel(X, Z), reachable(Z, Y).`
   Which of these two lines is the **base case**, and which is the **recursive case**? In your own
   words, explain what makes the second line "recursive."

**Answer** The base case is:
`reachable(X,Y) :-tunnel(X,Y).`

This is the base case because it checks whether there is a tunnel that goes directly from X to Y. If there is a direct tunnel, the destination has been reached and no more recursive steps are necessary.

The recursive case ir:
`reachable(X,Y) :-tunnel(X,Z), reachable(Z,Y).`

This is the recursive case because the rule uses `reachable` again inside its own definition. It first moves from X to an intermediate chamber Z and then checks whether Z can eventually reach Y. This allows the search to continue through several tunnels until reaches the destination.

---

## Part 2 — The Search Space (Session 11)

3. What is the **initial state** and the **goal state** in this activity?

**Answer** The initial state is **Entrance** because that is where the exploration begins. The goal state is **Treasure Room** because the objective is to reach the chamber containing the treasure.

4. According to the app's brute-force count, how many total possible paths exist from the
   Entrance to the Treasure Room? List every path.

**Answer** According to the app's brute-force count, there are exactly **2 possible paths** from Entrance to Treasure Room, without repeated chamber.

1. `Entrance - Torch Hallway - Crustal Cavern - Treasure Room`
2. `Entrance - Bast Roost - Echo Chamber - Torch Hallway - Crystal Cavern - Treassure Room`

The first path has 3 tunnels, while the second path has 5 tunnels.

5. In your own words, explain the difference between the **search space** (every possible path)
   and the single path a search algorithm like DFS actually finds. Why can these be different?


**Answer** The search space is the collection of all possible paths that could be taken from the initial state to the goal state. In this activity , the search space contains two possible paths from Entrance to Treasure Room.

DFS does not necessarily explore all possible paths before finding the goal. Instead, it follows one branch as deeply as possible. If it reaches a dead end, it backtracks and tries another branch. Therefore, the search space can contain several possible solutions, while DFS may only need to find one of them. The path DFS finds depends on the order in which it explores the available tunnels.

---

## Part 3 — Depth-First Search (Session 12)

6. List, in order, every chamber DFS actually **visited** (not skipped) before finding the
   treasure. How many chambers did it visit in total?

**Answer** The chambers DFS actually visited, in order, were:

1. Entrance
2. Bat Roost
3. Spider Tunnel
4. Old Mine Shaft
5. Bottomless Pit
6. Echo Chamber
7. Torch Hallway
8. Cystal Cavern
9. Treassure Room

Therefore, DFS visited a total of **9 chambers** before finding the reasure.

The visited order is different from the final successful path because DFS explored some branches that did not lead directly to the treasure.

7. Name the one chamber where DFS hit a genuine **dead end** and had to backtrack. Separately,
   name the one chamber on the map that was **never visited at all** before the treasure was
   found, and explain why not.

**Answer** The genuine dead end was **Bottomless Pit**, when DFS reached this chamber, there were no new tunnels to explore, so it had to backtrack and return to a precious chamber.

The chamber that was never visited before the treasure was found **Underground Lake**. DFS did not need to explore this branch because it eventually reached Crystal Cavern and then the Treasure room. Once the treasure was found, the search stopped, so Underground Lake remained unvisited.

8. What is the exact path DFS used to reach the treasure (the chain of chambers from Entrance to
   Treasure Room, not just the order things were visited)? Is it the same as the *shortest*
   path you listed in Question 4? If not, explain in your own words why Depth-First Search
   doesn't always find the shortest path.

**Answer:** The exact path DFS used to reach the treasure was:

`Entrance - Bat Roost - Echo Chamber - Torch Hallway - Crystal Cavern - Treasure Room`

This is **not** the shortest path.

The shortest path listed in Question 4 was:

`Entrance → Torch Hallway → Crystal Cavern → Treasure Room`

The shortest path has 3 tunnels, while the path found by DFS has 5 tunnels.

DFS does not always find the shortest path because its main strategy is to go as deep as possible into one branch before backtracking. It does not compare all possible paths by their length before choosing one. In this activity, DFS explored the Bat Roost branch first, so it visited several chambers before reaching the Treasure Room.

## Part 4 — Synthesis

9. Explain, as if to a 10-year-old, why the recursive `reachable(X, Y)` rule from Session 10 and
   the step-by-step stack-based search from Session 12 are really "the same idea" wearing two
   different costumes.

**Answer** Imagine that you are looking for a toy in a big house. You start in one room and choose a door to another room. If the toy is not there, you continue thtough another door. You keep gping until you find the toy or reach a room where there are no more doors to try. Then you go back and try another option. 

The recursive `reachable(X,Y)` rule does this by calling `reachable` again to continue searching through another tunnel. The DFS algorithm does the same basic thing using a stack to remember which chambers still need to be explored.

Both methods go deeper into one branch and backtrack when that branch cannot lead to the goal. Therefore, they are the same basic search idea expressed in two different ways: recursion in one case and an explicit stack in the other.

10. Name one real-world use of Depth-First Search **other than** cave/maze exploration (for
    example: exploring a file system, checking whether a website's links can reach a certain
    page, or solving a puzzle). Briefly explain how "go as deep as possible, then backtrack"
    applies in that example.

**Answer:** One real-world use of Depth-First Search is exploring a computer's file system.

For example, if a computer needs to search through folders for a specific file, DFS can start in one folder and enter its first subfolder. It can continue opening folders inside that folder until it reaches a folder with no more unexplored subfolders. Then it can go back to the previous folder and explore another branch.

This follows the DFS idea of going as deep as possible first and then backtracking when there is nowhere else to go.
