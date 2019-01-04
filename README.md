# CBBio
Contents
1 Introduction 
2 Software Tools Requirements
3 Software tools installation on windows 
4 Source code for running software tools
5 Ensemble learning system Requirements
6 Machine learning methods installation on windows
7 Source codes for implementation of machine learning algorithms

1 Introduction 
This package can help to analysis Whole-Exome Sequencing (WES) data, files (.maf) and so on. It is used for identification of candidate driver genes associated with cancers based on mutations that occur in genes.
In the first step, it uses four software tools for features extraction from mutation (whole-exome sequencing) data.
These software tools are MutSigCV v.1.4 [1], OncodriveCUST [2], OncodriveFM [3], and NetBox 1.0 [4]. They rank genes based on P-value (0=P-value=1). And then any tool assigns a number to genes as a feature.
At next an ensemble machine learning method [5] was applied for driver genes prioritization based on feature Integration. It involves three individual classifiers including non-linear SVM (Support Vector Machine) [6], ANN (Artificial Neural Network) [7] and [8], and RF (Random Forest) [9]. They labeled genes based on two indexes 0 and 1 (0 means passenger gene and 1 means driver gene) and also predicted a score for a gene. Finally, the ensemble learning method adopts the final decision for each gene. So, this fusion method integrates outputs and makes a decision based on Algebraic Combiners strategy [5] and [10]. It means that this ensemble approach calculates the average among three scores which are special for each gene and come from the results of the individual classifiers.
To analyze the results and rank candidate driver genes, it is recommended to use the analytical capabilities are available in TCGA or cBioPortal. 

2 Software Tools Requirements 

2.1 Requirements for MutsigCV v.1.4:

•	A license for Matlab (Full ToolBox), you can run MutSigCV from its source code file: MutSigCV.m
•	If you do not have a license for Matlab, you can run the compiled version of MutSigCV using the free Matlab MCR: run_MutSigCV.sh <path_to_MCR> mutations.maf coverage.txt covariates.txt output.txt

2.2 Requirements for OncodriveCLUST:
•	Python 3; OncodriveCLUST depends on Python 3 and some external libraries, numpy, scipy, pandas and statsmodels.
•	Anaconda 3; The easiest way to install all this software stack is using the well-known Anaconda Python distribution.

2.3 Requirements for OncodriveFM:

•	Python 3; OncodriveFM depends on Python 3 and some external libraries, numpy, scipy, pandas and statsmodels.
•	Anaconda 3; The easiest way to install all this software stack is using the well-known Anaconda Python distribution.

2.4 Requirements for NetBox:
•	Java 1.5 or later.
•	Python 2.5 or later. 

3 Software tools installation on windows

3.1 To install MutsigCV v.1.4, you must have: 
•	The MutsigCV software and its reference files are available for download at: https://software.broadinstitute.org/cancer/cga/mutsig https://software.broadinstitute.org/cancer/cga/mutsig_run

3.2 To install OncodriveCLUST, you must have: 
•	OncodriveCLUST software and its requirements are available for download at: http://bg.upf.edu/group/projects/oncodrive-clust.php
https://bitbucket.org/bbglab/oncodriveclust/overview

3.3 To install OncodriveFM, you must have: 
•	OncodriveFM software and its requirements are available for download at: http://bg.upf.edu/group/projects/oncodrive-fm.php
https://bitbucket.org/bbglab/oncodrivefm

3.4 To install NetBox 1.0, you must have: 
•	The NetBox software, user guide, checking updates, and example datasets are available for download at: http://cbio.mskcc.org/netbo

4 Source code for running software tools

4.1 Run the following command to see MutsigCV in action:
?	MutSigCV('C:\[directory]\....maf'...
 ,'C:\[directory]\MutSigCV\Required inputs\exome_full192.coverage.txt'...
 ,'C:\[directory]\MutSigCV\Required inputs\gene.covariates.txt'...
,'C:\[directory]\MutSigCV\ExampleData\MutSigCV_example_data.1.0.1\LUSC.example.output.txt'...
,'C:\[directory]\MutSigCV\Required inputs\mutation_type_dictionary_file.txt'...
 ,'C:\Users\[directory]\MutSigCV\Required inputs\chr_files_hg19')

4.2	Run the following command to see OncodriveCLUST in action:
?	oncodriveclust -m 3 --cgc C:\[directory]\Anaconda3\bbglab-oncodriveclust-60e75d0cb432\data/CGC_phenotype.tsv C:\[directory]\Anaconda3\bbglab-oncodriveclust-60e75d0cb432\examples/…_nonsyn.txt C:\[directory]\Anaconda3\bbglab-oncodriveclust-60e75d0cb432\examples/…_syn.txt C:\[directory]\Anaconda3\bbglab-oncodriveclust-60e75d0cb432\data/gene_transcripts.tsv

4.3	Run the following command to see OncodriveFM in action:

?	oncodrivefm -e median -m C:\[directory]\Anaconda3\bbglab-oncodrivefm-0d3030da3f83\data/ensg_kegg.tsv C:\[directory]\Anaconda3\bbglab-oncodrivefm-0d3030da3f83\data/….tdm

4.4	Run the following command to see NetBox in action:
?	cd C:\netbox\..._data
C:\Python\Python36-32\python.exe C:\netbox\bin\netAnalyze.py C:\netbox\..._data\netbox1.props

5 Ensemble learning system Requirements 
Requirements for machine learning methods:
Python 2.5 or later; We used scikit-learn package to train machine learning models and implement our algorithms in python.

6 Machine learning methods installation on windows
Scikit-learn package is available for download at:
https://scikit-learn.org/stable/
Please follow the steps below to install three individual machine learning methods and the proposed ensemble learning method:
•	Download and UnRAR File named “CBBio.rar”.

•	Replace your desired files including feature file (.csv), positive and negative data files (.txt), and Test file (.txt) instead of the default file.
Note that the file names and formats are preserved.

7   Source codes for implementation of machine learning algorithms
To implement learning machine methods run the following commands in anaconda prompt 2:
?	For SVM: cd [directory] python svm_gene_classification.py
?	For ANN: cd [directory] python nn_gene_classification.py
?	For RF: cd [directory] python rf_gene_classification.py
?	For ensemble learning machine: cd [directory] python all_gene_classification.py

•	Finally, two output files will be created for each of the machines.
One of the files named “…_predictions_train” (.csv) assigns a new label to train data and predicts a score for each gene.
In the next file named “…_predictions_test” (.csv), the test data is labeled and the scores for the genes are predicted.
In this way, genes are prioritized according to their importance in the occurrence of cancer.

References:
[1]	M. S. Lawrence et al., “Mutational heterogeneity in cancer and the search for new cancer-associated genes,” Nature, vol. 499, no. 7457, pp. 214–218, 2013.
[2]	D. Tamborero, A. Gonzalez-Perez, and N. Lopez-Bigas, “OncodriveCLUST: exploiting the positional clustering of somatic mutations to identify cancer genes,” Bioinformatics, vol. 29, no. 18, pp. 2238–2244, 2013.
[3]	A. Gonzalez-Perez and N. Lopez-Bigas, “Functional impact bias reveals cancer drivers,” Nucleic Acids Res., vol. 40, no. 21, pp. e169–e169, 2012.
[4]	E. Cerami, E. Demir, N. Schultz, B. S. Taylor, and C. Sander, “Automated network analysis identifies core pathways in glioblastoma,” PLoS One, vol. 5, no. 2, p. e8918, 2010.
[5]	L. Rokach, “Ensemble-based classifiers,” Artif. Intell. Rev., vol. 33, no. 1–2, pp. 1–39, 2010.
[6]	C. Cortes and V. Vapnik, “Support-vector networks,” Mach. Learn., vol. 20, no. 3, pp. 273–297, 1995.
[7]	F. Rosenblatt, “The perceptron: a probabilistic model for information storage and organization in the brain.,” Psychol. Rev., vol. 65, no. 6, p. 386, 1958.
[8]	J. Schmidhuber, “Deep learning in neural networks: An overview,” Neural networks, vol. 61, pp. 85–117, 2015.
[9]	T. K. Ho, “Random decision forests,” in Document Analysis and Recognition, 1995., Proceedings of the Third International Conference on, 1995, vol. 1, pp. 278–282.
[10]	R. Polikar, “Ensemble based systems in decision making,” Circuits Syst. Mag. IEEE, vol. 6, no. 3, pp. 21–45, 2006.

