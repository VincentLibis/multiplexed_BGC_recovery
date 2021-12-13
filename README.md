# multiplexed_BGC_recovery

Scripts (Python Jupyter notebooks) and DNA sequences associated with the 2021 paper on multiplexed mobilization of biosynthetic gene clusters (BGCs).  

---
## List of files:

### Notebooks
```./notebooks/CONKAT-seq_PAC_localization.ipynb``` - Detect, dereplicate and localize BGCs contained in an arrayed PAC library.

```./notebooks/nanopore_processing.ipynb``` - Perform de-novo assembly of PAC inserts from Nanopore reads.

### Graph : Predicted domain networks in the library
graphml file visualized with Cytoscape in Figure 2C

### BGCs antismash analysis files
fasta file of the 70 BGCs mobilized into heterologous hosts and antismash analysis results 

---

## Analysis scripts:
### CONKAT-seq_PAC_localization.ipynb
Generates networks of biosynthetic domains and track their physical location in the PAC library
input : demultiplexed AD/KS reads from 1) genomes 2) plate_pools 3) well_pools
output : graphml file

### nanopore_processing.ipynb
Performs de-novo assembly of PAC inserts from Nanopore reads. Reads are aligned on 16kbp of pESAC-Apramycin vector sequence using minimap2 with default parameters. Non-aligned reads are kept in full while aligned reads are processed with Jvarkit’s SamExtractClip to recover only their non-aligned regions (i.e. PAC inserts regions clipped by minimap2). Following vector DNA filtering, the reads are assembled using Flye.
