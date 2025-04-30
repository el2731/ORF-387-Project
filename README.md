# ORF 387 Networks Project

## Overview
This README provides an overview of our project for the ORF 387: Networks
course during Spring 2025 semester.

## Project Description
This project aims to conduct a comprehensive analysis of the NYC MTA 
network, focusing specifically on the NYC subway and Staten Island 
Railway systems. The analysis includes:

1. **Basic Network Structure Analysis**: Examining the fundamental 
   properties of the transit network.
2. **Network Centrality Analysis**: Identifying key stations and 
   connections within the system.
3. **Network Topology and Spatial Configuration**: Analyzing the 
   geographic layout and connectivity patterns.
4. **Network Resilience**: Evaluating how the network responds to 
   disruptions or station closures.

The analysis utilizes open-source data of stations provided in the 
`MTA_Subway_Stations.csv` file. All code implementation for these 
analyses is available in the `project.ipynb` notebook.

## Requirements
The following packages are required to run the notebook:
- networkx
- numpy
- matplotlib
- pandas
- seaborn
- contextily
- adjustText
- scipy
- sklearn
- IPython

## Installation
To install the required packages, run:
```bash
pip install package_name
```
where `package_name` is the name of one of the packages listed above which
are required to run the code in the notebook.

## Usage
1. Open the `project.ipynb` file in Jupyter Notebook or JupyterLab.
2. Run the cells in sequence.

## File Structure
- `project.ipynb` - Main project notebook containing all code and analysis
- `MTA_Subway_Stations.csv` - Dataset containing comprehensive information
   for all subway and Staten Island Railway stations, including geographic 
   coordinates, Station Master Reference Number (MRN), Complex MRN, Stop ID, 
   serviced train lines, structural type, location relative to Manhattan's 
   Central District (CBD), and ADA-accessibility status. In total, the dataset 
   comprises 496 station entries. 

   [View the MTA Subway Stations dataset](https://catalog.data.gov/dataset/mta-subway-stations)
- `figures/` - Directory containing all the relevant plots and visuals of the analysis done

## Methods
### Basic Network Structure Analysis
- Analyzed degree distribution of station nodes
- Calculated network density and size metrics
- Determined average degree across the network
- Identified and analyzed connected components statistics

### Network Centrality Analysis
- Calculated key centrality measures:
    - Degree centrality
    - Closeness centrality
    - Betweenness centrality
- Grouped stations by complex IDs for unified analysis
- Visualized relative distribution of centrality scores
- Created heatmaps to display centrality score intensity across the network

### Network Topology and Spatial Configuration
- Analyzed borough distribution using pie charts
- Mapped station node density using heatmap visualization
- Implemented radius-based approach for density analysis
- Determined community structure using Girvan-Newman algorithm
- Optimized partitioning to maximize modularity score
- Visualized communities using color-coded representation

### Network Resilience and Robustness
- Identified critical stations within the network
- Measured impact of targeted node removal on network connectivity
- Conducted system vulnerability analysis using various attack strategies
- Analyzed and plotted key metrics in response to node removal:
    - Number of connected components
    - Percentage of remaining nodes in largest component
    - Average path length in largest component

## Results
This project analyzed the network structure, topology, centrality, and 
resilience of the consolidated NYC MTA Subway and Staten Island Railway 
(SIR) systems using graph theory and network science techniques.

### Basic Network Structure Analysis

* **Network Size:** The consolidated network consists of 
  **493 unique station nodes** and **544 connections (edges)**.
* **Connectivity:**
    * Average Degree: ~2.21 (each station connects to approx. 2 others 
      on average).
    * Network Density: 0.0045 (sparse, typical for large transit 
      networks, comparable to Boston MBTA).
* **Components:** The network is divided into 
  **5 connected components**:
    * **Component 1 (Largest):** 59.2% of stations (292 nodes). Includes
      major lines converging on Manhattan 
      (7, A, B, C, D, E, F, G, J, M, N, Q, R, S, W, Z). Forms a 
      Manhattan-centric web radiating outwards.
    * **Component 2:** 31.2% of stations. A more regional corridor 
      (Lines 1, 2, 3, 4, 5, 6) serving Bronx, Manhattan, Brooklyn.
    * **Component 3:** L line shuttle.
    * **Component 4:** S line shuttles.
    * **Component 5:** Staten Island Railway (SIR), 
      isolated operationally.
* **Degree Distribution:**
    * Peaks at degree 2, aligning with the average degree.
    * Right-skewed distribution indicates most stations have low 
      connectivity (degree <= 2), with few high-degree hubs.
    * Gaussian KDE fit shows strong alignment with data (R² = 0.9190).

### Network Centrality Analysis (on Station Complexes)

* **Metrics Used:** Degree, Closeness, and Betweenness centrality (normalized 0-1).
* **Key Findings:**
    * **Manhattan CBD Dominance:** Stations/complexes in Manhattan's 
      Central Business District (CBD) consistently rank high across all 
      centrality measures (e.g., Times Sq-42 St/Port Authority, Fulton St, Canal St).
    * **Outer-Borough Importance:** Crucially, outer-borough hubs, 
      particularly **Atlantic Av-Barclays Ctr (Brooklyn)**, also rank 
      exceptionally high, being **#1 in Betweenness Centrality**, 
      #2 in Degree, and #5 in Closeness, highlighting its critical role 
      as a network bridge beyond just local importance. Jay St-Metrotech 
      (Brooklyn) also ranked high in Betweenness and Closeness.
    * **Overall Centrality Distribution:** All centrality metrics show 
      right-skewed distributions, meaning structural importance is 
      concentrated in relatively few key hubs. Closeness centrality had 
      the best KDE fit (R² = 0.9633).
* **Spatial Visualization:** Heatmaps visually confirm the concentration 
  of high centrality scores in Manhattan CBD and key hubs in Brooklyn 
  and Queens.

### Network Topology and Spatial Configuration

* **Borough Station Counts:** Brooklyn has the highest number of 
  stations (34.1%), followed by Manhattan (30.8%). Queens (16.7%) 
  and Bronx (14.1%) have fewer, and Staten Island (SIR) has the least (4.2%).
* **Station Density:** Despite fewer total stations, Manhattan 
  (esp. Midtown/Lower) exhibits the **highest station density**, 
  reinforcing its role as the operational core. Secondary high-density 
  clusters exist in Downtown Brooklyn, Western Queens, and South Bronx. 
  Outer areas show much lower density.
* **Community Detection (Girvan-Newman):**
    * Identified **22 distinct communities**, largely aligning 
      geographically with specific lines or operational segments.
    * Manhattan acts as a convergence zone for multiple communities, 
      not a single entity.
    * SIR forms a distinct, isolated community.
* **Bridge Analysis (Inter-Community Links):**
    * Found **50 bridge nodes** and **29 bridge edges** connecting the 
      communities.
    * Average bridge node connects to ~1.15 other communities; 
      average bridge coefficient is ~0.52 (balanced internal/external links).
    * Key lines serving as bridges include F, B, A, C, 2.
    * Top bridge nodes (e.g., Nevins St, Bergen St, 
      Broadway-Lafayette St, Jay St-Metrotech, Atlantic Av-Barclays Ctr) 
      often overlap with high-betweenness nodes and are concentrated in 
      Downtown Manhattan and Downtown Brooklyn.
    * Most bridge edges connect communities *within* the same borough, 
      but some cross boroughs.
    * Multiple bridge edges exist between key community pairs 
      (e.g., 10&11, 11&12, 15&16), suggesting network redundancy in 
      core areas.

### Network Resilience and Robustness (Simulated Attacks)

* **Methodology:** Assessed network integrity degradation under 
  simulated node/edge removals using various attack strategies. Measured 
  impact via # components, Largest Connected Component (LCC) size, and 
  average path length in LCC.
* **Attack Strategies:**
    * Centrality-Based: Removing nodes by descending Degree, Closeness, 
      or Betweenness.
    * Structural: Removing entire Lines (by size) or Complexes (by 
      aggregate degree).
* **Key Findings:**
    * **Vulnerability to Targeted Attacks:** The network is highly 
      vulnerable to targeted removal of nodes with high **Closeness** or 
      **Betweenness** centrality, and removal of major **Complexes**. 
      These attacks cause rapid fragmentation (sharp increase in 
      components, rapid decrease in LCC size).
    * **Degree vs. Other Centrality:** Degree-based attacks cause 
      slower fragmentation compared to Closeness/Betweenness attacks.
    * **Line Removal Impact:** Removing entire lines causes slower 
      topological fragmentation but has a significant impact on network 
      efficiency (average path length).
    * **Evidence of Robustness:** Despite vulnerabilities, the network 
      shows inherent robustness, particularly against line removals. The 
      stabilization of average path length during prolonged line attacks 
      suggests the presence of redundancy and alternative routing options.

## Contributors
- Michelle Chen
- Joshua Lee
- Evan Lin