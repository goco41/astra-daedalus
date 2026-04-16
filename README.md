# Urbek Farming Pattern Optimizer
### **[Try the Live Interactive Pattern Editor](https://goco41.github.io/Urbek_City_Patterns/)**

This project contains the ultimate toolset for finding and refining farming patterns in **Urbek City Builder**. Developed through an iterative journey documented on Reddit, this repository provides a high-performance Python solver and a web-based visual editor.

## Evolution of the Pattern
This project started as a quest to find the theoretical maximum efficiency for farming layouts.
*   **Post #1:** 61.35 points
*   **Post #2:** 62.62 points
*   **Post #3:** 63.012 points
*   **Post #4 (Latest):** **78.1 points**

**The Story Behind the Big Leap:**
That massive jump from 63 to the upper echelons actually originated from a **bug** in the code. The algorithm generated a pattern hitting 69 points, but it unfortunately violated some of the game's strict building rules. However, my collaborator **vninect** stepped in and managed to sanitize and improve that bugged layout, reaching a completely valid 72x18 pattern with nearly 70 points. 

Sometime later, vninect achieved an even more impressive "mini" 9x18 pattern scoring 76. I used this mini pattern as a base to push the optimizer even further, scaling and refining it to create a "medium" 27x18 pattern that holds the current record of **78.1**.

## Project Components

### 1. Trifecta Pattern Editor (`index.html`)
A standalone, browser-based visual editor designed to manually tweak patterns or visualize solver exports.
*   **God Mode:** Place buildings anywhere ignoring rules for quick drafting.
*   **Rule Engine:** Real-time validation of building requirements (radii, neighbors, road access).
*   **Import/Export:** Seamlessly copy-paste Python arrays to and from the solver.
*   **Interactive Info:** Click any building to see its current production and synergy status.

And a lot more, check upper rigth 'Documentation' to see it all.

### 2. The Solver (`optimizer.py` / `urbek_city_optimizer.ipynb`)
A heavy-duty optimization script that uses Constraint Programming and Meta-heuristics.
*   **Google OR-Tools (CP-SAT):** Handles the complex logic of building requirements.
*   **ALNS (Adaptive Large Neighborhood Search):** A loop that "destroys" parts of the pattern and rebuilds them to find better local optima.
*   **Numba-Accelerated:** Geometric calculations (Manhattan/Chebyshev distances) are compiled to machine code for speed.
*   **Tiling Support:** Optimized for multiple vertical/horizontal stacks.

### 3. The Corruption Algorithm Concept (`corruption.ipynb`)
The bug that accidentally boosted our score to 69 gave me an idea for a brand new approach based on **rule corruption**. The theory is to deliberately break game rules (relaxing minimums, maximums, or radii) to escape local optima and reach a higher-scoring invalid state, and then run a secondary repair process to "sanitize" it back into legality. I haven't been able to recreate the magic or make this algorithm work perfectly yet, so I am leaving the code and the idea here. If anyone can figure out how to make this corruption-based logic hum, it might be the key to breaking the next major barrier!

---

## Getting Started

### Prerequisites
To run the Python solver, you need:
```bash
pip install ortools numpy numba matplotlib
```

### Running the Solver
1.  Open the Python script or Jupyter Notebook.
2.  Define your building requirements in type_catalog (or TYPE_DEFS in the corruption script) and their output in productions.
3.  Set your time limit (in seconds).
4.  Run the notebook cell
5.  The script will output a `patron_clean.csv` and a Python-formatted matrix.

### Using the Editor
1.  Open `index.html` in any modern web browser.
2.  Paste a matrix into the "Import" box.
3.  Use the **Move/Swap** tool to manually refine the layout.
4.  Check the **Average Score** in the header to see the impact of your changes.

---

## Building Logic
The solver respects the complex interdependencies of Urbek's late-game farming:
*   **Food Plants (10):** Require proximity to Farm Sheds (8).
*   **Fruit Processors (9):** Require a massive number of Orchards (7).
*   **Silos (6):** Synergize with Warehouses (I8).
*   **Road Connectivity:** All buildings (except specific ones) must be connected via a pathing rank system to the main road.

---

## History & Community
This project was born and raised on the r/Urbek subreddit. You can follow the full development history and community discussions here:

*   [Update #1: Initial Discovery](https://www.reddit.com/r/urbek/comments/1ldv8mf/is_this_really_the_best_pattern_for_farming/)
*   [Update #2: Breaking the 62 Barrier](https://www.reddit.com/r/urbek/comments/1lf6s8b/is_this_the_best_pattern_for_farming_update/)
*   [Update #3: The 63.01 optimization](https://www.reddit.com/r/urbek/comments/1lvmts0/is_this_the_best_pattern_for_farming_update_30/)
*   [Update #4: The 78.1 big leap](https://steamcommunity.com/app/1411740/discussions/0/807974496347725576/)

---

## Academic References

The optimization logic of this project is based on state-of-the-art research in Combinatorial Optimization and Vehicle Routing Problems:

*   **Røpke, S., & Pisinger, D. (2006):** [An Adaptive Large Neighborhood Search Heuristic for the Pickup and Delivery Problem with Time Windows](https://backend.orbit.dtu.dk/ws/portalfiles/portal/3154899/An%20adaptive%20large%20neighborhood%20search%20heuristic%20for%20the%20pickup%20and%20delivery%20problem%20with%20time%20windows_TechRep_ropke_pisinger.pdf). (The foundation for the adaptive loop and operator weight adjustment).
*   **Hojabri, H., et al. (2016):** [Large Neighborhood Search with Constraint Programming for a Vehicle Routing Problem with Synchronization Constraints](https://www.cirrelt.ca/documentstravail/cirrelt-2016-31.pdf). (Inspiration for the intensity parameters and LNS-CP integration).
*   **Thomas, C., & Schaus, P. (2018):** [Revisiting the Self-Adaptive Large Neighborhood Search](https://dial.uclouvain.be/pr/boreal/object/boreal%3A200499/datastream/PDF_01/view). (Logic for the operator portfolio and efficiency-based weight updates).
*   **Souza, F., et al. (2024):** [An Investigation of Generic Approaches to Large Neighbourhood Search (iVRG)](https://drops.dagstuhl.de/storage/00lipics/lipics-vol307-cp2024/LIPIcs.CP.2024.39/LIPIcs.CP.2024.39.pdf). (Methodology for Improved Variable-Relationship Guided selection).
*   **Pacino, D., & Van Hentenryck, P. (2011):** [Large Neighborhood Search and Adaptive Randomized Decompositions for Flexible Jobshop Scheduling](https://backend.orbit.dtu.dk/ws/files/54505265/Large_Neighborhood_Search_and_Adaptive_Randomized.pdf). (Framework for randomized decomposition strategies).
 
---
## License
This project is open-source and available under the **GNU General Public License v3.0**.

If you modify the solver's logic or enhance the optimization algorithms to reach new records, the license requires you to share those improvements under the same terms. Let's keep the Urbek optimization engine open for everyone!
Feel free to fork, optimize further, and share your scores!

**Can you beat 78.1?** If so, open a PR or post it on Reddit, Steam or Discord!
