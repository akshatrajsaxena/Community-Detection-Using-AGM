<h1 align="center">Community Detection Using AGM</h1>
<p align="center"><i>Analyzing GitHub user networks using Agglomerative Greedy Modularity (AGM) algorithm</i></p>
<div align="center">
  <a href="https://github.com/akshatrajsaxena/Community-Detection-Using-AGM/stargazers"><img src="https://img.shields.io/github/stars/akshatrajsaxena/Community-Detection-Using-AGM" alt="Stars Badge"/></a>
  <a href="https://github.com/akshatrajsaxena/Community-Detection-Using-AGM/network/members"><img src="https://img.shields.io/github/forks/akshatrajsaxena/Community-Detection-Using-AGM" alt="Forks Badge"/></a>
  <a href="https://github.com/akshatrajsaxena/Community-Detection-Using-AGM/pulls"><img src="https://img.shields.io/github/issues-pr/akshatrajsaxena/Community-Detection-Using-AGM" alt="Pull Requests Badge"/></a>
  <a href="https://github.com/akshatrajsaxena/Community-Detection-Using-AGM/issues"><img src="https://img.shields.io/github/issues/akshatrajsaxena/Community-Detection-Using-AGM" alt="Issues Badge"/></a>
  <a href="https://github.com/akshatrajsaxena/Community-Detection-Using-AGM/graphs/contributors"><img alt="GitHub contributors" src="https://img.shields.io/github/contributors/akshatrajsaxena/Community-Detection-Using-AGM" ?color=2b9348"></a>
  <a href="https://github.com/akshatrajsaxena/Community-Detection-Using-AGM/blob/master/LICENSE"><img src="https://img.shields.io/github/license/akshatrajsaxena/Community-Detection-Using-AGM ?color=2b9348" alt="License Badge"/></a>
</div>
<br>

# Community Detection Using AGM

This project focuses on analyzing GitHub user networks using the Agglomerative Greedy Modularity (AGM) algorithm to detect and analyze community structures within the network.

## Project Overview

The main objectives of this project are:

1. **Network Graph Creation**: Creating a network graph from the GitHub users' interaction data using NetworkX, where nodes represent users and edges represent connections between them.

2. **Community Detection**: Implementing the Agglomerative Greedy Modularity algorithm to identify distinct communities within the network graph.

3. **Community Assignment**: Assigning users to their respective communities and analyzing the community structure.

4. **Modularity Analysis**: Calculating and analyzing the modularity score to evaluate the quality of the community detection.

## Technologies Used

- **NetworkX**: A Python library used for creating, manipulating, and studying complex networks.
- **Python**: The primary programming language used for implementing the AGM algorithm and data processing.
- **PySpark**: Initially used for data processing (optional alternative implementation provided).
- **CSV**: Used for storing and reading edge data.

## Getting Started

To get started with the project, please follow these steps:

### 1. **Clone the Repository**:

```bash
git clone https://github.com/akshatrajsaxena/Community-Detection-Using-AGM.git
```

### 2. **Install Dependencies**:

```bash
pip install networkx
pip install numpy
pip install pandas
pip install pyspark  # Optional for Spark implementation
```

### 3. **Data Format**:

Ensure your edge data is in CSV format with the following structure:
```
id_1,id_2
1,2
2,3
...
```

### 4. **Run the Community Detection**:

Execute the Python script to perform community detection:
```python
python community_detection.py
```

## Implementation Details

### Graph Creation
```python
import networkx as nx
import csv

# Read edges from CSV
edges_list = []
with open("musae_git_edges.csv", 'r') as file:
    csv_reader = csv.DictReader(file)
    for row in csv_reader:
        id_1 = int(row['id_1'])
        id_2 = int(row['id_2'])
        edges_list.append((id_1, id_2))

# Create NetworkX graph
G = nx.Graph()
G.add_edges_from(edges_list)
```

### Community Detection
```python
from networkx.algorithms.community import greedy_modularity_communities

# Detect communities using AGM
communities = list(greedy_modularity_communities(G))

# Calculate modularity score
modularity = nx.algorithms.community.quality.modularity(G, communities)
```

### Community Assignment
```python
from collections import defaultdict

# Create community assignments dictionary
communities_dict = defaultdict(list)
for i, community in enumerate(communities):
    for node in community:
        communities_dict[node] = i

# Print assignments
for node, community in sorted(communities_dict.items()):
    print(f"{node}: {community}")
```

## Project Structure

The project includes the following main components:

- `community_detection.py`: Main script containing the implementation of graph creation and community detection
- `musae_git_edges.csv`: Input data file containing the edge information
- `requirements.txt`: List of Python dependencies
- `README.md`: Project documentation

## Output Format

The program outputs:
1. List of detected communities with their members
2. Overall modularity score of the network
3. Individual node-to-community assignments

## License

This project is licensed under the [MIT License](https://github.com/akshatrajsaxena/Community-Detection-Using-AGM/blob/main/LICENSE)

## Contact

If you have any questions or would like to get in touch, you can reach me at [Akshat Raj Saxena](mailto:akshat22054@iiitd.ac.in).
EOF
