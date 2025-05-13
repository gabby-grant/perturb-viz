# perturb-viz
This script visualizes perturbed genes identified by GEMDiff in a network context, highlighting connections between perturbed genes and top differentially expressed genes.

A visualization tool for highlighting perturbed genes identified by GEMDiff in a network context.

## Overview

PerturbViz is designed to create network visualizations that highlight relationships between perturbed genes (identified by GEMDiff) and differentially expressed genes. The tool provides an intuitive way to visualize how perturbed genes relate to up/downregulated genes in a gene interaction network.

## Features

- Visualizes perturbed genes in the context of a gene interaction network
- Highlights top up and down regulated genes 
- Calculates network centrality metrics to identify key genes
- Produces publication-ready network visualizations
- Generates detailed network statistics for further analysis
- Customizable visualization parameters

## Installation

```bash

# Clone the repository
git clone https://github.com/yourusername/PerturbViz.git
cd PerturbViz

# Install dependencies

pip install pandas numpy matplotlib networkx
```

## Usage

### Basic Usage

```bash
python perturbviz.py --network network_data.tsv --perturbed "TMEM184A,PDE1C,GPR146,FAM110B" --degs degs_results.tsv
```

### Input File Formats

1. **Network file** (required): Tab-delimited file with at least two columns for source and target genes
   
```
Source Target
Gene1 Gene2
Gene1 Gene3
Gene2 Gene4
```

2. **Perturbed genes** (optional): Either a comma-separated list or a file with one gene per line
   
```
TMEM184A
PDE1C
GPR146
FAM110B
```

3. **DEG file** (optional): Tab-delimited file with gene and log2FC columns
   
```
gene log2FC pvalue padj
Gene1 2.5 0.001 0.005
Gene2 -1.8 0.002 0.01
Gene3 0.5 0.1 0.2
```

### Command Line Options
```
--network, -n Network file (tab-delimited with source/target columns)
--perturbed, -p Comma-separated list of perturbed genes or path to file with one gene per line
--degs, -d DEG file with gene and log2FC columns
--output, -o Output prefix for generated files (default: perturb_network)
--top_genes, -t Number of top up/downregulated genes to highlight (default: 10)
--max_nodes, -m Maximum nodes to include in visualization (default: 200)
--layout, -l Network layout algorithm: spring, kamada_kawai, circular, spectral (default: spring)
--node_size Base node size for perturbed genes (default: 80)
--include_neighbors Depth of neighboring genes to include (default: 1)
--dpi DPI for output image (default: 300)
--width Figure width in inches (default: 14)
--height Figure height in inches (default: 12)
```

## Example

```bash
python perturbviz.py --network gene_interactions.tsv --perturbed perturbed_genes.txt --degs deseq_results.tsv --output uterine_perturb --top_genes 15 --include_neighbors 2
```

## Output Files

1. `uterine_perturb_network.png`: Network visualization with color-coded nodes
2. `uterine_perturb_stats.tsv`: Detailed network statistics for each gene
3. `uterine_perturb_edges.tsv`: Edge list of the visualized network

## Integration with GEMDiff Workflow

PerturbViz is designed to work seamlessly with GEMDiff outputs:

1. Run GEMDiff to identify perturbed genes:

```bash
python scripts/perturb.py --config config.yaml --model_path models/model10000.pt
```
