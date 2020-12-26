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
The sample input file is a comma separated file where each row indicate informations on the bulk DNA sample, row 1 is dedicated for the header. An example of the file is:

```
sample_name,file_sample,time_point_value,ALC
Sample-T-01,/path/Patient1/sample1_MAF.txt,1719,40
Sample-T-02,/path/Patient1/sample2_MAF.txt,2295,100
```
The file_sample column indicate the path where the MAF file for the sample is stored. The time_point_value indicates when the time point was collected, while the ALC (absolute lymphocyte count) is optional and it is used as tumor size proxy if available for display purpose only.

#### MAF 



### Output





## Contact

For assistance with running Concerti, interpreting the results, or other related questions, please feel free to contact: Laxmi Parida <parida@us.ibm.com> or Filippo Utro <futro@us.ibm.com>

## Licence

See LICENSE for license information.
