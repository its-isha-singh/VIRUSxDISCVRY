# IQ-TREE
written by: [Vedika Jha], Edited By: Caitlin Oxley

[10 minute] IQ-TREE is a user-friendly way to generate phylogenetic trees using maximum likelihood (ML) methods. It allows users to input a sequence alignment of any kind (DNA, protein, etc.), chose an appropriate evolutionary model for substitution rates, and other parameters for branch support and tree searching. It then outputs an inferred phylogenetic tree of all sequences in the alignment. This allows users to understand how unknown viruses are related to known viruses in their family or order, or compare how different strains of an unknown virus are related. It an also be used to learn more about the emerging obelisk.


**Tutorial Objective**: We will understand how to use the Tree Inference tool of IQ-TREE to generate phylogenetic trees for a given alignment of sequences.

## Input / Prerequisites
- [Tool Weblink](http://iqtree.cibiv.univie.ac.at/)
- [Link to example data](http://www.cibiv.at/~jana/example.phy)
- ...

## Output

When running the Tree Inference tool, the results will contain up to seven files. The main output will be the phylogenetic tree of the aligned sequences generated by the maximum likelihood method. This will be provided in .svg, .pdf, and .treefile formats (can be viewed using treeviewer programs such as FigTree). The other files include a run log (.log), full results of the run (.iqtree), and a checkpoint file (ckp.gz) if the run was stopped. The full results of the run (.iqtree) can be visualized on the webserver. 


### 00. Navigate to a text editor
I used sublime to put my sequences into a form that can be recognized by a MSA tool.
Using the SRA number as the main identifier of each obelisk sample sequence.
eg."(OBELISK_SRA_NUMBER) >
obelisk_sequence""
Then I saved the file with a ".txt" suffix.
![Sublime Text Editor](img/iqtree/tutorial_q1.png)

### 0. Generate an alignment of sequences that you want to map on your tree

Before using this IQ-tree, you will need an alignment of your sequences of any kind (DNA, protein, codon, etc.). Sequences may include Rdrp sequences of similar viruses (identified using BLAST) or known viruses in the same family/order. This alignment can be generated in several ways, including Clustal Omega, MEGA/Muscle, or MAFFT. See links at the bottom of this document.
Here is an example of Clustal Omega
![Clustal Omega](img/iqtree/clustal_omega.png)

### 1. Navigate to IQ-Tree, tree inference tab
![IQ Tree home page](img/iqtree/IQ_TREE_1.png)

### 2. Input your alignment
Next to "Alignment file" press "Browse..." to input the MSA file.
The alignment must be in Phylip, Fasta, Nexus, Clustal, or MSF format. These formats can be generated from the tools listed in step 00 and 0.

You can select the sequence type based on how you did your alignment, or leave the program to auto-detect it. If you use auto-detect, the analysis results page will show what sequence type is used. If you select sequence type, make sure it matches what your alignment has (for example, using Muscle Codon alignment means you should select Codon, using Clustal Omega DNA alignment means you should use DNA) Binary sequences are encoded by the characters 0 and 1, and morphology sequences allow 0-9 and A-Z as characters, these types are not as common.

You generally do not need to use the partition model, as this is for multi-gene alignments and different subtitution models for each gene. If you think this is needed for your data (containing multiple genes that are likley to evolve very differently), see the link below.

### 3a. (Optional) Use the model selection tool to identify the best fitting substitution model

By navigating to the "Model Selection" tab and inputting the alignment (following step 2), you can find out which substitution model is the best fit for your data. Submit your job using "BIC" as the selection criterion. BIC has slightly different criterion for selecting the best model, penalizing models with more parameters. In the literature, it has been shown to be more accurate for phylogenetic data (see links below). However, getting results from corrected AIC as well (running another job) can help you better understand your data.

The lower the value of both AIC and BIC tests, the better the model fits your alignment.

### 3b. Choose your substitution model on the Tree Inference Tool

Choose your substitution model either based on the model selection tool step above, or use "auto". If the lowest value model from the BIC result included "+ G", "+R", and/or "+ I", check the "Gamma", "Free Rate", and/or "Invar. sites" buttons accordingly.

No other parameters (State frequency, ascertainment bias) need to be changed from default for this analysis.

### 4. Select branch support analysis methods and other parameters

Calculating branch support can show you how likely the resulting branch in the tree is given the data, kind of like a confidence interval. Using ultrafast bootstrap will be the fastest option, and all other parameters can be left at the default.

### 5. Submit the Job.
Click the "Submit" to start the analysis.
You will be directed to Job Progress page where you can see the time you submitted the file and the status of the analysis.
![Submit the job tab](img/iqtree/iq-TREE_2.png)

### 6. Visualize results in webserver, download trees for further visualization
Click the "Full Result" tab to see your tree.
The output will include:
- The phylogentic tree in newik format.
- Model summary: list of the best-fit substitution model and parameters.
-Log file: analysis steps and likelihood scores.
-Bootstrap file : bootstrap support values

Download the necessary files of interest.
Below is the phylogentic tree that was produced using the obelisk371 data.
![Phylogentic Tree](img/iqtree/-q_tree-3.png))

In the "Analysis Results" tab, you will also see the model finder (if "auto" was used for model selection), the parameters of the model used, the maximum likelihood tree, and the consensus tree from "bootstrapped" data (see below for bootstrapping details). The Maximum likelihood tree can tell you how your sequences are related, but if it disagrees with your consensus tree, then those branches/clades/relationships are not well supported.

Other programs such as FigTree can be used to further manipulate the tree. Download the results (using the "Download selected jobs" button) and open the .treefile in other programs to reroot the tree (if you have a known outgroup) or change labeling. The .pdf or .svg can be used for result reporting if no further manipulation is required.

### Conclusion

That's it! You've used IQ-TREE to generate a phylogenetic tree!

Here, I've provided basic tutorial on how to use IQ-TREE to select a maximum likelihood substitution model and generate a phylogenetic tree. The resulting tree from your analysis can show you how different viral species/strains are related to one another. You can learn more about the details of model selection and the IQ-TREE tool in the links below. 

### See Also:

- [IQ-TREE 2: New Models and Efficient Methods for Phylogenetic Inference in the Genomic Era](https://academic.oup.com/mbe/article/37/5/1530/5721363?login=true)
- [Why use phylogenetic analysis](https://bmcecolevol.biomedcentral.com/articles/10.1186/1471-2148-13-161)
- [Principles of phylogenetics](https://www.nature.com/articles/nrg3186)
- [Multi-gene alignments, partitioned analysis](http://www.iqtree.org/doc/Advanced-Tutorial#partitioned-analysis-for-multi-gene-alignments)
- [AIC vs BIC in phylogenetics](https://academic.oup.com/mbe/article/37/2/549/5613171)
- [Bootstrapping in phylogenetics](https://www.jstor.org/stable/3182855?seq=1)
