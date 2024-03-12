ARGs-MGEs-MAP manual
==========================================

This is a modified version of [Ublastx_stageone-2.3](https://github.com/biofuture/Ublastx_stageone) . We upgraded the antibiotic resistance gene (ARG) database, thereby enhancing the detection capability of ARGs. Additionally, we incorporated the detection capability for mobile genetic elements (MGEs).
The antibiotic resistance genes (ARGs) database is derived from [ARGs-OAP (v2.2)](https://github.com/biofuture/Ublastx_stageone) , [CARD 2022 (v3.25) ] (https://card.mcmaster.ca/), and [DeepARG] (https://github.com/gaarangoa/deeparg).
The mobile genetic elements (MGEs) database is sourced from [mobileOG-db](https://github.com/clb21565/mobileOG-db).


If you  have any questions or suggestions of this tool, please leave us a message in the Issues. 

The change log of this version includes:
1. MGE analysis pipeline
2. Updates to the ARG database

Prepare compulsory command
============================
1. bbmap
a. download packages from here (https://sourceforge.net/projects/bbmap/)
b. install bbmap
c. copy the whole folder "bbmap" into the subfoler "bin" under "ARGs-MGEs-MAP"

2. samtools
a. download packages from here (http://www.htslib.org/download/)
b. install samtools
c. copy executable "samtools" into the subfoler "bin" under "ARGs-MGEs-MAP"

3. mimimap2
a. download packages from here (https://github.com/lh3/minimap2)
b. install minimap2
c. copy executable "mimimap2" into the subfoler "bin" under "ARGs-MGEs-MAP"

Prepare the meta-data file of your samples  
==========================================
To run the pipeline, users need to prepare relative meta-data.txt file and put all the pair-end fastq file into one directory  
Example of meta-data file **meta-data.txt**  Tips:   
* You need keep the first and second column's name as SampleID and Name
* The SampleID are required to be unique numbers counting from 1 to 2 to 3 etc.
* Category is the classification of your samples into groups and we will colored your samples in PcoA by this informaton
* The meta-data table should be separated by tabular for each of the items 
* The Name of each sample should be the fastq file names for your pair-end Illumina sequencing data, your fastq files will automatically be recognized by Name_1.fq and Name_2.fq, so you need to keep the name consistent with your fq file name. (if you files are end with .fastq or .fasta, you need to change them to end with .fq or .fa)
 
**Please make sure the meta-data file is pure txt format, if you edit the file under windows, using nodepad++ and check the end of each line by cliking View-> Show Symbol -> Show All Characters. If the line is end up with CRLF, please remove the CR by replace \r to nothing in the replace dialogue frame. Please make sure that the fourth column is the lenght of the reads**

SampleID | Name | Category | ReadLength     
---------|------|----------|---------  
 1       | STAS | ST       | 100   
 2       | SWHAS104 | SWH  | 100   


Stage one
==================
Put all your fastq files into one directory in your local system (notice the name of your fastq files should be Name_1.fq and Name_2.fq). your can give -h to show the help information. Examples could be found in source directory example, in example directory run test:   

```
#ARG analysis
nohup ./argoap_pipeline_stageone_version2.3 -i inputfqs -o testoutdir -m meta-data.txt -n 8

./argoap_pipeline_stageone_version2.3  -h

#MGE analysis
nohup ./mobile_pipeline_stageone_version2.33 -i inputfqs -o testoutdir -m meta-data.txt -n 8

./mobile_pipeline_stageone_version2.3  -h
```
The results are in testoutdir/

The **extracted.fa** and **meta_data_online.txt** are two files needed for ublastx_stage_two analysis.   

The meta-data-online.txt looks like this 

SampleID | Name | Category | ReadLength |#ofreads | #of16S| **#ofCell**   
---------|------|-----------|----------|-------|----|---- 
 1       | STAS | ST  | 100| 200000 | 10.1  |   4.9
 2       | SWHAS104 | SWH | 100|200000 | 9.7 |    4.1

Stage two
========================================================
Normally, just run
```
# ARG analysis
nohup perl argoap_pipeline_stagetwo_version2 -i extracted.fa -m meta_data_online.txt -o testout -l 25 -d 80 -e 1e-7

#MGE analysis
nohup perl mobile_pipeline_stagetwo_version2 -i extracted.fa -m meta_data_online.txt -o testout -l 25 -d 80 -e 1e-7
```

Adjustment parameters
========================================================
If you have your own requirements for the analysis results，you can adjust the following parameters in the second step of analysis.
```
#Custom parameters
-l length filtering default 25 aa 
-e evalue filtering default 1e-7
-d identity filtering default 80


# ARG analysis
perl argoap_pipeline_stagetwo_version2 -i extracted.fa -m meta_data_online.txt -o testout -l 25 -d 80 -e 1e-7
perl argoap_pipeline_stagetwo_version2 -i extracted.fa -m meta_data_online.txt -o testout -l 50 -d 80 -e 1e-8

#MGE analysis
perl mobile_pipeline_stagetwo_version2 -i extracted.fa -m meta_data_online.txt -o testout -l 25 -d 80 -e 1e-7
perl mobile_pipeline_stagetwo_version2 -i extracted.fa -m meta_data_online.txt -o testout -l 50 -d 80 -e 1e-8
```

This pipeline is distributed in the hope to achieve the aim of management of antibiotic resistant genes in envrionment, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.This pipeline is only allowed to be used for non-commercial and academic purpose.

**The SARG database is distributed only freely used for academic prupose, any commercial use should require the agreement from the developer team.** 
