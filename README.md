# Bitcoin OTC Network Analysis

A comprehensive graph-based analysis of the **Bitcoin OTC trust network** using Python and NetworkX. This project explores the structural properties of a real-world signed social network where users rate each other's trustworthiness on a Bitcoin trading platform.

---

## Dataset

**Source:** [Stanford SNAP — Bitcoin OTC Trust Network](https://snap.stanford.edu/data/soc-sign-bitcoinotc.html)

The dataset is a **who-trusts-whom** network of Bitcoin traders on the OTC (over-the-counter) platform. Each user can rate another user on a scale of **-10 (total distrust) to +10 (total trust)**.

| Column | Description |
|--------|-------------|
| `source` | User giving the rating |
| `target` | User receiving the rating |
| `rating` | Trust score (-10 to +10) |
| `time` | Unix timestamp of the rating |

---

## Project Structure

```
bitcoin-otc-network-analysis/
│
├── bitcoin-otc-network-analysis.ipynb   # Main analysis notebook
└── README.md
```

---

## Analysis Performed

### 1. Graph Construction
- Loaded dataset directly from Stanford SNAP via URL
- Built an undirected graph using NetworkX from edge list
- Visualised the raw network using random layout and spring layout

### 2. Basic Graph Statistics
- Total number of edges
- Average node degree
- Network density
- Number of connected components

### 3. Shortest Path Analysis
- Computed all-pairs shortest path lengths
- Calculated network diameter (longest shortest path)
- Plotted the **distribution of shortest path lengths** across the network

### 4. Centrality Measures

| Centrality Type | What it measures |
|----------------|-----------------|
| **Degree Centrality** | How many direct connections a node has |
| **Betweenness Centrality** | How often a node lies on shortest paths between others |
| **Closeness Centrality** | How quickly a node can reach all other nodes |
| **Eigenvector Centrality** | Influence based on the quality of a node's neighbours |

Each centrality metric includes:
- Top 10 most central nodes
- Histogram of distribution across all nodes
- Network visualisation with node size proportional to centrality score

### 5. Clustering & Triangles
- Computed **average clustering coefficient** of the network
- Plotted clustering coefficient distribution
- Counted total triangles in the network
- Calculated mean triangles per node

### 6. Bridge Detection
- Identified **bridges** (edges whose removal disconnects the graph) — highlighted in red
- Identified **local bridges** (edges connecting otherwise distant parts) — highlighted in green
- Visualised both on the network graph simultaneously

### 7. Assortativity
- Computed **degree assortativity coefficient** (do high-degree nodes connect to other high-degree nodes?)
- Verified using Pearson correlation coefficient via SciPy

### 8. Community Detection
Two algorithms applied:
- **Label Propagation** — fast, scalable community detection on the full graph
- **Asynchronous Fluid Communities (`asyn_fluidc`)** — applied to the largest connected component, detecting 8 communities

Both results visualised with randomly assigned colours per community.

---

## Requirements

```bash
pip install networkx pandas numpy matplotlib
```

| Library | Version (recommended) |
|---------|----------------------|
| `networkx` | >= 2.8 |
| `pandas` | >= 1.4 |
| `numpy` | >= 1.21 |
| `matplotlib` | >= 3.5 |

---

## How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/bitcoin-otc-network-analysis.git
   cd bitcoin-otc-network-analysis
   ```

2. Install dependencies:
   ```bash
   pip install networkx pandas numpy matplotlib
   ```

3. Open the notebook:
   ```bash
   jupyter notebook bitcoin-otc-network-analysis.ipynb
   ```

4. Run all cells. The dataset is fetched automatically from the Stanford SNAP URL — no manual download needed.

> **Note:** Computing all-pairs shortest path lengths (`nx.all_pairs_shortest_path_length`) can be slow on large graphs. For the Bitcoin OTC network (~5,000 nodes, ~35,000 edges), expect this step to take a few minutes.

---

## Key Findings

- The network has a **small-world structure** — most nodes are reachable within a few hops despite the network being large.
- A small number of nodes have **very high betweenness centrality**, acting as critical bridges in the trust network.
- The **clustering coefficient** is notably higher than random graphs of the same size, suggesting that trust tends to be transitive (friends of friends trust each other).
- Community detection reveals distinct **clusters of traders** who predominantly interact within their group.
- The assortativity analysis indicates whether high-trust traders preferentially connect with other high-trust traders.

---

## Visualisations

The notebook generates the following plots:

- Raw network graph (random layout)
- Spring-layout network graph
- Shortest path length distribution (bar chart)
- Degree centrality histogram + node-size visualisation
- Betweenness centrality histogram + node-size visualisation
- Closeness centrality histogram + node-size visualisation
- Eigenvector centrality histogram + node-size visualisation
- Clustering coefficient histogram
- Bridge and local bridge visualisation (red/green edges)
- Community detection visualisation (label propagation)
- Community detection visualisation (fluid communities, k=8)

---

## References

- S. Kumar, F. Spezzano, V.S. Subrahmanian, C. Faloutsos. *Edge Weight Prediction in Weighted Signed Networks.* IEEE ICDM 2016.
- S. Kumar, B. Hooi, D. Makhija, M. Kumar, V.S. Subrahmanian, C. Faloutsos. *REV2: Fraudulent User Prediction in Rating Platforms.* ACM WSDM 2018.
- [NetworkX Documentation](https://networkx.org/documentation/stable/)
- [Stanford SNAP Dataset](https://snap.stanford.edu/data/soc-sign-bitcoinotc.html)

---

## License

This project is open source and available under the [MIT License](LICENSE).
