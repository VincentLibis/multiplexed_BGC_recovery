# multiplexed_BGC_recovery

Scripts (Python Jupyter notebooks) and DNA sequences associated with the 2022 paper on multiplexed mobilization of biosynthetic gene clusters.  

---
## List of files:

### Notebooks
```./notebooks/CONKAT-seq_PAC_localization.ipynb``` - Detect, dereplicate and localize BGCs contained in an arrayed PAC library.

```./notebooks/nanopore_processing.ipynb``` - Perform de-novo assembly of PAC inserts from Nanopore reads.

### Graph : Predicted domain networks in the library
graphml file visualized with Cytoscape in Figure 2C

### BGCs antismash analysis files
fasta file of the 70 BGCs mobilized into heterologous hosts.

(Antismash 6 analysis results can be dowloaded here : https://www.dropbox.com/s/c75c5rk8nm62bpf/70_documents_from_fasta_antismash_github.zip?dl=0 )

---

## Analysis scripts:
### CONKAT-seq_PAC_localization.ipynb
Generates networks of biosynthetic domains and track their physical location in the PAC library


#### How it works:
input : demultiplexed AD/KS reads from A) genomes B) plate_pools C) well_pools
1) cluster amplicons into OTUs with vsearch (trim primer sequence and truncate reads to 200bp, dereplicate reads within in pool, sort by read count, call OTUs accross all pools)
2) filter OTUs (removing sequences with read count smaller than 3. For each cluster, also removes sequences with low read counts (<5%) relative to the maximum read count of a sequence in the cluster)
3) localize positions of OTUs in the library
4) evaluate co-occurrences and connect domains into networks (evaluate co-occurrences between biosynthetic domains in each category of pools, apply threshold on pvalue and generate graph, cleanup graph from fragile nodes/edges)
5) Annotate nodes with pblast - measure identity to known BGCs ( Extract protein sequences from reference BGCs, blastp translated domains in the graph, annotate graph file)

output : graphml file



### nanopore_processing.ipynb
Performs de-novo assembly of PAC inserts from Nanopore reads. Reads are aligned on 16kbp of pESAC-Apramycin vector sequence using minimap2 with default parameters. Non-aligned reads are kept in full while aligned reads are processed with Jvarkit’s SamExtractClip to recover only their non-aligned regions (i.e. PAC inserts regions clipped by minimap2). Following vector DNA filtering, the reads are assembled using Flye.
