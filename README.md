# Concerti

Concerti is an algorithm for inferring disease evolution phylogenies, at genomic scales, from multiple sites and multiple longitudinal DNA sequencing samples.

## Citation

Please cite the following article if you use Concerti:

Filippo Utro, Chaya Levovitz, Kahn Rhrissorrakrai and Laxmi Parida: A Common Methodological Phylogenomics Framework for intra-patient heteroplasmies to infer SARS-CoV-2 sublineages and tumor clones. to appear.


## Usage

### Download
[Git Large File Storage (LFS)](https://git-lfs.github.com/) is required.
To download please run:

`git lfs clone https://github.com/ComputationalGenomics/Concerti.git`

### Running
The command to run Concerti is simply

```
./Concerti -s <sample_input_file> -o <out_dir>
```
where the required options -s designate the samples input file while -o the output directory.

Concerti was tested on Ubuntu 18.04.5 LTS

### Command line options
```
usage: Concerti [-h] --sample_info SAMPLE_INFO [--patient_name PATIENT_NAME] --store_out_folder STORE_OUT_FOLDER [--store_tmp] [--thd_clustering THD_CLUSTERING]
                [--small_clone_thd SMALL_CLONE_THD] [--thd_zero THD_ZERO] [--criterion CRITERION] [--graph] [--no_longitudinal] 
                [--cnv CNV] [--black_list BLACK_LIST] [--VAF] [--VAFDistance {euclidean,hamming,chebyshev,correlation}]

optional arguments:
  -h, --help            show this help message and exit
  --sample_info SAMPLE_INFO, -s SAMPLE_INFO
  --patient_name PATIENT_NAME, -p PATIENT_NAME
                        Indicates the patient name, if provided it will be used in the output filenames.
  --store_out_folder STORE_OUT_FOLDER, -o STORE_OUT_FOLDER
                        Name of the output folder.
  --store_tmp, -st      Indicates if temporary data should be stored
  --thd_clustering THD_CLUSTERING
                        Threshold to where to cut the dendrogram in the clustering step.
  --small_clone_thd SMALL_CLONE_THD
                        Clones with ccf value in all time points below the provided value will be ignore in the tree construction.
  --thd_zero THD_ZERO   Threshold for which a mutation is considered absent
  --criterion CRITERION
  --graph, -g           Indicates if store plots in supplemental folder.
  --no_longitudinal, -nl
                        Indicates the sample were collected from a longitudinal experiment.
  --cnv CNV, -cnv CNV
  --black_list BLACK_LIST, -bl BLACK_LIST
  --VAF, -vaf           Indicates if the input data are in VAF format.
  --VAFDistance {euclidean,hamming,chebyshev,correlation}, -vd {euclidean,hamming,chebyshev,correlation}
                        Indicates which distance to be use in the case of VAF data.
```

### Input

#### Sample File
The sample input file is a comma separated file where each row indicate informations on the bulk DNA sample, the first row is dedicated for the header. An example of the file is:

```
sample_name,file_sample,time_point_value,ALC
Sample-T-01,/path/Patient1/sample1_MAF.txt,1719,40
Sample-T-02,/path/Patient1/sample2_MAF.txt,2295,100
```
The file_sample column indicate the path where the MAF file for the sample is stored. The time_point_value indicates when the time point was collected, while the ALC (absolute lymphocyte count) is optional and it is used as tumor size proxy if available for display purpose only.

#### MAF 
With respect to the standard [MAF](https://docs.gdc.cancer.gov/Data/File_Formats/MAF_Format/) format additional data can be provided, such as the CCF distribution discretized into 100 bins (easily obtained in MAF format via the absolute tool) as well as the confidence interval. For instance:

```
Hugo_Symbol	... ccf_CI95_low ccf_CI95_high 0 0.01 0.012 ... 1
TIMD4 ... 0.340465829	1 0	2.07E-35	9.88E-33 ... 0.070962262
```

Concerti relies on the assumption is that a set of alterations is present in the same set of clones, then the pair will be present in the same set of samples. Sometime due to sequencing error, or other factor, an alteration may not been detected in a sample but for instance in the multi-time case it was detected in the previous and in the next sample. Hence the corresponding MAF file must be corrected. Since there are several pre-processing filtering to enforce this assumptiom, and they are out of scope of this tool, the user must adjust the MAF prior running the tool.

#### CNV
Copy Number event can also be provided as input to Concerti via a single MAF file as described above, where the column *Sample_ID* indicate which sample the event belong to. CNV event are processed only via their CCF distribution.

#### Alteration filtering
If the user wants to filter a set of alterations (e.g. due to possible artifact) withouth changing the original MAF they can provide as input via a tab separeted file: chromosome, position, reference, alteration. For instance:

```
1	155161125	T	G
5	179278379	GGAATGAGATTCTATGGACTTGGA	-
7	27149924	A	G
```

### Output

The output folder indicated by the `--store_out_folder` (`-o`) option will be created if not existed. The folder will contains a subfolder named *supplement* where extra data will be store. For instance if the `-st` and/or the  `-g` options were indicated these files will be stored inside the supplement one. For each sample, the supplement folder will also contain the possible clonal configuration in a `_tree.csv` (a file per sample), with the following format:

```
tree,pr
(-1,2)(2,4)(2,3)(4,1.0),0.16271127210267092
...
```

The firt column contains the tree information as (parent, child) relationship, where -1 indicate no parent. Whie the second column indicate the probability of the tree. 

A similar file with all compatible trees across sample is then stored in the main output folder as well as `*clonal_structure.csv`: which contains for each row an alteration, the mean CCF (or VAF) for each sample and to which clone/cluster it has been assigned.


## Contact

For assistance with running Concerti, interpreting the results, or other related questions, please feel free to contact: Laxmi Parida <parida@us.ibm.com> or Filippo Utro <futro@us.ibm.com>
## License

See [LICENSE](https://github.com/ComputationalGenomics/Concerti/blob/main/license) for license information.
