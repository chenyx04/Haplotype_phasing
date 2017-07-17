# Haplotype_phasing

Spectral-stitching algorithm for solving haplotype phasing problem. It implements the algorithm proposed in:


Chen, Y., Kamath, G., Suh, C., & Tse, D. (2016, June). Community recovery in graphs with locality. In International Conference on Machine Learning (pp. 689-698).


The current version is implemented in python, MATLAB and R for simple evaluation. The subsampling and preprocess step is in python. The main program is in MATLAB. And evaluation is in R. We will release a finished and formal pure python code soon. We apologize for the potential inconvenience for running the current version.

The present code requires CVX package in matlab (http://cvxr.com/cvx/) and foreach & doParallel package in R. In a future release of a pure python version, we'll get rid of these dependency. 

If you have any question, please feel free to contact 

Banghua Zhu (13aeon.v01d@gmail.com)

Yuxin Chen (yuxin.chen@princeton.edu)

## Usage

We provide a demo for running on chromosome 20 of NA12878 WGS data.

First run 'subsample&preprocess.py' for subsampling the coverage and generate adjacent matrix file required for main program.

Then run 'pipeline.m' to run spectral-stitching algorithm on generated adjacent matrix. 

Finally, run measure_performance_across_subsamples.R to get the metrics switch error rate and unphased SNPs. Run N50.py to get N50.

If you have a a adjacent matrix (or contact map) in the same format as 'contactmap_demo.csv', You can run 

```
phased_seq = Spectral_stitching('contactmap_demo.csv');
```

 to get the phased sequence.

The format of contact map file should be:

\# of rows (space) \# of columns (space) Number of linkages

SNP pos x1 (space) SNP Index y1 (space) \# of reads that indicate x1 and y1 belong to one community (If one read indicates x1 and y1 are all 0 or all 1, then this adds 1, else this minuses 1)

SNP pos x2 (space) SNP Index y2 (space) \# of reads that indicate x2 and y2 belong to one community

For example, if you have 4 reads, the first read indicates SNP1 and SNP2 are in the same community. The second read indicates SNP1 and SNP2 are in different community. The third read indicate SNP1 and SNP3 are in the same community. The fourth read indicates SNP1 and SNP2 are in different community. Then the contact map should be:

3 3 3

1 1 -1     (The first read +1, the second read -1, the fourth read -1.)

1 3 1      (The third read +1.)




## Usage of New python version

We've uploaded a preliminary python version for spectral stitching algorithm. It takes in either the refhap reads file or contact map as defined above.

We provide two examplanary dataset, run the following script to get help
'''
python spectral_stitching -h
'''
The demo script for running on refhap reads file is 
'''
python spectral-stitching.py -r refhapreads_demo.txt  -o out.phased
'''

For running on contact map file, type
'''
python spectral-stitching.py -c contactmap_demo.csv  -o out.phased
'''

If you want a whole continuous snp output instead of blocked one. Try parameter -nb




