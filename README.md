ARGs-MGEs-MAP manual
==========================================

This is a modified version of [Ublastx_stageone-2.3](https://github.com/biofuture/Ublastx_stageone) .

If you  have any questions or suggestions of this tool, please leave us a message in the Issues. 

The change log of this version includes:
1. MGE analysis pipeline
2. Updates to the ARG database

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

Run the following command to exec the pipeline
==================================

 

The **meta_data_online.txt** includes some intemediate numbers information such as #ofreads, #of16S, #ofCells, etc. All the tables are in the files with prefix: stage2output.

The meta-data-online.txt looks like this 

SampleID | Name | Category | ReadLength |#ofreads | #of16S| **#ofCell**   
---------|------|-----------|----------|-------|----|---- 
 1       | STAS | ST  | 100| 200000 | 10.1  |   4.9
 2       | SWHAS104 | SWH | 100|200000 | 9.7 |    4.1



This pipeline is distributed in the hope to achieve the aim of management of antibiotic resistant genes in envrionment, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.This pipeline is only allowed to be used for non-commercial and academic purpose.

**The SARG database is distributed only freely used for academic prupose, any commercial use should require the agreement from the developer team.** 
