### EX7 Implementation of Link Analysis using HITS Algorithm
### DATE: 27.02.26
### AIM: To implement Link Analysis using HITS Algorithm in Python.
### Description:
<div align = "justify">
The HITS (Hyperlink-Induced Topic Search) algorithm is a link analysis algorithm used to rank web pages. It identifies authority and hub pages 
in a network of web pages based on the structure of the links between them.

### Procedure:
1. ***Initialization:***
    <p>    a) Start with an initial set of authority and hub scores for each page.
    <p>    b) Typically, initial scores are set to 1 or some random values.
  
2. ***Construction of the Adjacency Matrix:***
    <p>    a) The web graph is represented as an adjacency matrix where each row and column correspond to a web page, and the matrix elements denote the presence or absence of links between pages.
    <p>    b) If page A has a link to page B, the corresponding element in the adjacency matrix is set to 1; otherwise, it's set to 0.

3. ***Iterative Updates:***
    <p>    a) Update the authority scores based on the hub scores of pages pointing to them and update the hub scores based on the authority scores of pages they point to.
    <p>    b) Calculate authority scores as the sum of hub scores of pages pointing to the given page.
    <p>    c) Calculate hub scores as the sum of authority scores of pages that the given page points to.

4. ***Normalization:***
    <p>    a) Normalize authority and hub scores to prevent them from becoming too large or small.
    <p>    b) Normalize by dividing by their Euclidean norms (L2-norm).

5. ***Convergence Check:***
    <p>    a) Check for convergence by measuring the change in authority and hub scores between iterations.
    <p>    b) If the change falls below a predefined threshold or the maximum number of iterations is reached, the algorithm stops.

6. ***Visualization:***
    <p>    Visualize using bar chart to represent authority and hub scores.

### Program:
~~~
import numpy as np
import matplotlib.pyplot as plt

def hits_algorithm_fixed(adj_matrix, iterations=17):
    num_nodes = len(adj_matrix)

    # Initialize scores
    authority = np.ones(num_nodes)
    hub = np.ones(num_nodes)

    print("HITS Algorithm (3x3 Matrix - 17 Iterations)\n")
    print("Iteration\tAuthority Scores\t\tHub Scores\n")

    for i in range(iterations):
        # Authority Update
        authority = np.dot(adj_matrix.T, hub)

        # Normalize Authority
        if np.sum(authority) != 0:
            authority = authority / np.sum(authority)

        # Hub Update
        hub = np.dot(adj_matrix, authority)

        # Normalize Hub
        if np.sum(hub) != 0:
            hub = hub / np.sum(hub)

        # Print iteration results
        print(f"{i+1}\t\t{np.round(authority,4)}\t{np.round(hub,4)}")

    return authority, hub


# 🔹 3x3 Matrix (Example)
adj_matrix = np.array([
    [0, 1, 1],
    [1, 0, 0],
    [1, 0, 0]
])

# Run Algorithm
authority, hub = hits_algorithm_fixed(adj_matrix, iterations=17)

# ------------------------------
# Final Results
# ------------------------------
print("\nFinal Authority Scores:", np.round(authority, 4))
print("Final Hub Scores:", np.round(hub, 4))

# ------------------------------
# Ranking
# ------------------------------
auth_rank = sorted(range(len(authority)), key=lambda i: authority[i], reverse=True)
hub_rank = sorted(range(len(hub)), key=lambda i: hub[i], reverse=True)

print("\nAuthority Ranking:")
for i in auth_rank:
    print(f"Node {i} - {authority[i]:.4f}")

print("\nHub Ranking:")
for i in hub_rank:
    print(f"Node {i} - {hub[i]:.4f}")

# ------------------------------
# Bar Chart
# ------------------------------
nodes = np.arange(len(authority))
bar_width = 0.35

plt.figure(figsize=(8, 6))
plt.bar(nodes - bar_width/2, authority, bar_width, label='Authority')
plt.bar(nodes + bar_width/2, hub, bar_width, label='Hub')

plt.xlabel('Nodes')
plt.ylabel('Scores')
plt.title('HITS Algorithm (17 Iterations)')
plt.xticks(nodes, [f'Node {i}' for i in nodes])
plt.legend()
plt.tight_layout()
plt.show()
~~~


### Output:
<img width="1582" height="952" alt="image" src="https://github.com/user-attachments/assets/82544661-33e6-44ef-bd05-fd3a2857f60e" />

### Result:
Link Analysis using HITS Algorithm in Python Executed Successfully.
