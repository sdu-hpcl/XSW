# Xsw
*   A fast Smith-Waterman Algorithm Implementation on Intel Xeon Phi Coprocessors.

## Introduction
* Xsw is a fast implementation of Smith-Waterman algorithm performed on the Intel(R) MIC platform. We achieved a speed of 70G CUPS (cell update per second) on a single Xeon Phi 7110p in native mode and 98G CUPS on a E5-2620 CPU with one Xeon Phi 7110p in offload mode processing query P58299 with database env-nr_FASTA. Large databases like nr(19G) are supported at about 90 GCUPS using fast external storage devices(e.g. SSD).

##Installation and Usage
* Three files must be provided to run Xsw: the scoring matrix, query sequence and the database. The query sequence and database should be in FASTA format.
For example, steps to run the query testRefSeq0511.txt to the database db.env_nr with the default gap penalties and scoring matrix are as following:

** For native version: **

* Step 1: Preproccess the database:
 
    `./makemicdb.out db.env_nr 244`

    *[NOTE:] if your Xeon Phi has 61 cores, it is 244, if 60 cores it is 240.*
    
* Step 2: Upload the database and program to xeon phi:

    `./scp db.env_nr.* blosum62.mat testRef* Xsw.mic mic0:`

* Step 3: Login xeon phi card:

    `./ssh mic0`
    
* Step 4: Run Xsw on xeon phi:

    `./Xsw.mic blosum62.mat testRefSeq0511.txt db.env_nr`

** For offload version: **

* Step 1: Preproccess the database:

    `./makemicdb4.1.out db.env_nr`
    
* Step 2: Run Xsw:

    `./Xsw.mic blosum62.mat testRefSeq1023.txt db.env_nr`

##Reference

* ** Paper is under submission.**

##Authors and Contributors
* Author 1

* Author 2
   
* Author 3

##Support or Contact
* If you have any questions, please contact: **Weiguo,Liu** ( *weiguo.liu@sdu.edu.cn*).

