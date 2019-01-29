CBBio v.0.1 By Leila Mirsadeghi

Contents

1 Introduction 

2 Software Tools Requirements

3 Software tools installation on windows 

4 Source code for running software tools

5 Ensemble learning system Requirements

6 Machine learning methods installation on windows

7 Source codes for implementation of machine learning algorithms

1 Introduction
 
This package called "CBBio" proposes a fusion system. This fusion system can help to analysis Whole-Exome Sequencing (WES) data, files (.maf) and so on. 
In this package, the published data in a study [1] on metastatic breast cancer has been used as initial input data. It is also available in cBioPortal [2], and [3].
This proposed fusion method can be used for identification of candidate driver genes associated with cancers based on mutations that occur in genes.

In the first step, it uses four software tools for features extraction from mutation (whole-exome sequencing) data.
These software tools are MutSigCV v.1.4 [4], OncodriveCUST [5], OncodriveFM [6], and NetBox 1.0 [7]. They rank genes based on P-value.

And then any tool assigns a number to genes as a feature.

At next an ensemble machine learning method [8] was applied for driver genes prioritization based on feature Integration. It involves three individual classifiers including non-linear SVM (Support Vector Machine) [9], ANN (Artificial Neural Network) [10] and [11], and RF (Random Forest) [12]. 

They labeled genes based on two indexes 0 and 1 (0 means passenger gene and 1 means driver gene) and also predicted a score for a gene. Finally, the ensemble learning method adopts the final decision for each gene. 

So, this fusion method integrates outputs and makes a decision based on Algebraic Combiners strategy [8] and [13]. It means that this ensemble approach calculates the average among three scores which are special for each gene and come from the results of the individual classifiers.

To analyze the results and rank candidate driver genes, it is recommended to use the analytical capabilities are available in TCGA or cBioPortal. 

2 Software Tools Requirements 

2.1 Requirements for MutsigCV v.1.4:

•	A license for Matlab (Full ToolBox), you can run MutSigCV from its source code file: MutSigCV.m

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
 
•	The MutsigCV software and its reference files are available for download at: 

https://software.broadinstitute.org/cancer/cga/mutsig https://software.broadinstitute.org/cancer/cga/mutsig_run

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

MutSigCV('C:\Users\Ghasedak Store\Desktop\simpleSomaticMutations\gdc_download_20171205_131010\d9876b23-3e7d-4d7b-bc1b-3b4393cd2afb\TCGA.BRCA.muse.d9876b23-3e7d-4d7b-bc1b-3b4393cd2afb.DR-7.0.somatic.maf\data_mutations_extended.maf'...
    ,'C:\Users\Ghasedak Store\Desktop\MutSigCV\Required inputs\exome_full192.coverage.txt'...
    ,'C:\Users\Ghasedak Store\Desktop\MutSigCV\Required inputs\gene.covariates.txt'...
    ,'C:\Users\Ghasedak Store\Desktop\MutSigCV\Example Data\MutSigCV_example_data.1.0.1\LUSC.example.output.txt'...
    ,'C:\Users\Ghasedak Store\Desktop\MutSigCV\Required inputs\mutation_type_dictionary_file.txt'...
    ,'C:\Users\Ghasedak Store\Desktop\MutSigCV\Required inputs\chr_files_hg19')


4.2	Run the following command to see OncodriveCLUST in action:

oncodriveclust -m 3 --cgc C:\ProgramData\Anaconda3\bbglab-oncodriveclust-60e75d0cb432\data/CGC_phenotype.tsv C:\ProgramData\Anaconda3\bbglab-oncodriveclust-60e75d0cb432\examples/nonsyn-mbca.txt C:\ProgramData\Anaconda3\bbglab-oncodriveclust-60e75d0cb432\examples/syn-mbca.txt C:\ProgramData\Anaconda3\bbglab-oncodriveclust-60e75d0cb432\data/gene_transcripts.tsv

4.3	Run the following command to see OncodriveFM in action:

oncodrivefm -e median -m C:\ProgramData\Anaconda3\bbglab-oncodrivefm-0d3030da3f83\data/ensg_kegg.tsv C:\ProgramData\Anaconda3\bbglab-oncodrivefm-0d3030da3f83\data/MBCA1.tdm

4.4	Run the following command to see NetBox in action:

cd C:\netbox\brca_data 
C:\Python\Python36-32\python.exe C:\netbox\bin\netAnalyze.py C:\netbox\brca_data\netbox1.props

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

For SVM: cd [directory] python svm_gene_classification.py -cvr 100

For ANN: cd [directory] python nn_gene_classification.py -cvr 100

For RF: cd [directory] python rf_gene_classification.py -cvr 100

For ensemble learning machine: cd [directory] python all_gene_classification.py -cvr 100

•	Finally, two output files will be created for each of the machines.

One of the files named “…_predictions_train” (.csv) assigns a new label to train data and predicts a score for each gene.
In the next file named “…_predictions_test” (.csv), the test data is labeled and the scores for the genes are predicted.
In this way, genes are prioritized according to their importance in the occurrence of cancer.

References:
[1]	N. Wagle et al., “The Metastatic Breast Cancer (MBC) project: Accelerating translational research through direct patient engagement.” American Society of Clinical Oncology, 2017.
[2]	E. Cerami et al., “The cBio cancer genomics portal: an open platform for exploring multidimensional cancer genomics data.” AACR, 2012.
[3]	J. Gao et al., “Integrative analysis of complex cancer genomics and clinical profiles using the cBioPortal,” Sci. Signal., vol. 6, no. 269, pp. pl1-pl1, 2013.
[4]	M. S. Lawrence et al., “Mutational heterogeneity in cancer and the search for new cancer-associated genes,” Nature, vol. 499, no. 7457, pp. 214–218, 2013.
[5]	D. Tamborero, A. Gonzalez-Perez, and N. Lopez-Bigas, “OncodriveCLUST: exploiting the positional clustering of somatic mutations to identify cancer genes,” Bioinformatics, vol. 29, no. 18, pp. 2238–2244, 2013.
[6]	A. Gonzalez-Perez and N. Lopez-Bigas, “Functional impact bias reveals cancer drivers,” Nucleic Acids Res., vol. 40, no. 21, pp. e169–e169, 2012.
[7]	E. Cerami, E. Demir, N. Schultz, B. S. Taylor, and C. Sander, “Automated network analysis identifies core pathways in glioblastoma,” PLoS One, vol. 5, no. 2, p. e8918, 2010.
[8]	L. Rokach, “Ensemble-based classifiers,” Artif. Intell. Rev., vol. 33, no. 1–2, pp. 1–39, 2010.
[9]	C. Cortes and V. Vapnik, “Support-vector networks,” Mach. Learn., vol. 20, no. 3, pp. 273–297, 1995.
[10]	F. Rosenblatt, “The perceptron: a probabilistic model for information storage and organization in the brain.,” Psychol. Rev., vol. 65, no. 6, p. 386, 1958.
[11]	J. Schmidhuber, “Deep learning in neural networks: An overview,” Neural networks, vol. 61, pp. 85–117, 2015.
[12]	T. K. Ho, “Random decision forests,” in Document Analysis and Recognition, 1995., Proceedings of the Third International Conference on, 1995, vol. 1, pp. 278–282.
[13]	R. Polikar, “Ensemble based systems in decision making,” Circuits Syst. Mag. IEEE, vol. 6, no. 3, pp. 21–45, 2006.


