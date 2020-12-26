# Concerti

Concerti is an algorithm for inferring disease evolution phylogenies, at genomic scales, from multiple sites and multiple longitudinal DNA sequencing samples.

## Citation

Please cite the following article if you use Concerti:

Filippo Utro, Chaya Levovitz, Kahn Rhrissorrakrai and Laxmi Parida: A Common Methodological Phylogenomics Framework for intra-patient heteroplasmies to infer SARS-CoV-2 sublineages and tumor clones. to appear.


## Usage

### Running
The command to run Concerti is simply

```
python Concerti.py -s <sample_input_file> -o <out_dir>
```
where the required options -s designate the samples input file while -o the output directory.


### Command line options


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
Hugo_Symbol	... ccf_CI95_low ccf_CI95_high 0 0.01 0.012..1
TIMD4 ... 0.340465829	1 0	2.07E-35	9.88E-33 0.070962262
```

#### CNV
Copy Number event can also be provided as input to Concerti via a MAF file as described before via their CCF distribution.

### Output





## Contact

For assistance with running Concerti, interpreting the results, or other related questions, please feel free to contact: Laxmi Parida <parida@us.ibm.com> or Filippo Utro <futro@us.ibm.com>

## License

See [LICENSE](https://github.com/ComputationalGenomics/Concerti/blob/main/license) for license information.
