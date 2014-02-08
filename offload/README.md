##Program and Data Preparation

* Change work dir to native:

	`cd XSW/offload/`

* Download the FASTA Database(env_nr):

	`wget -c ftp://ftp.ncbi.nih.gov/blast/db/FASTA/env_nr.gz`

* Unzip the FASTA Database:

	`gunzip -c env_nr.gz > db.env_nr`

* Source the environment:

	`source /opt/intel/bin/compilervars.sh intel64`

* Check your Intel(R) Compiler Version:

	`icc -V`

	[*WARNING*] Please use the lastest version of Intel(R) Compiler. 
	Highly recommend the Intel(R) Compiler 2013 SP1, version 14.0.0.080 Build 20130728.


##Usage Instructions

* To run XSW three files must be provided, the scoring matrix, query sequence and the sequence database.

We have attached a scoring matrix(blosum62.mat) and a query sequence(testRefSeq1023.txt) for testing purpose.
The query sequence and database must be in the FASTA format. For example, to run with the default gap penalties 11-1k, the scoring matrix BLOSUM62, the query sequence testRefSeq1023.txt and the sequence database db.env_nr use:

* Step 1: Preproccess the database:

	`./makemicdb4.1.out db.env_nr`
	  			  			 
* Step 2: Run XSW:

	`./XSW  blosum62.mat testRefSeq1023.txt  db.env_nr`


##Screen Output
	
`	testRefSeq1023.txt vs db.env_nr

	Matrix: blosum62.mat, gap_penalty: 11 + 1k


	Score  Description

	156  gi|135775141|gb|EBJ76490.1| hypothetical protein GOS_8843400 [marine metagenome]

	151  gi|144081156|gb|EDI73209.1| hypothetical protein GOS_383657 [marine metagenome]

	147  gi|143611599|gb|EDF85856.1| hypothetical protein GOS_881907 [marine metagenome]

	147  gi|135040727|gb|EBF11339.1| hypothetical protein GOS_9650673 [marine metagenome]

	144  gi|135313729|gb|EBG80175.1| hypothetical protein GOS_9371715 [marine metagenome]

	144  gi|138518781|gb|ECA15111.1| hypothetical protein GOS_6006581 [marine metagenome]

	143  gi|140376280|gb|ECL35020.1| hypothetical protein GOS_3747618 [marine metagenome]

	143  gi|134484268|gb|EBB61936.1| hypothetical protein GOS_203144 [marine metagenome]

	142  gi|138820109|gb|ECC00830.1| hypothetical protein GOS_5596799 [marine metagenome]

	142  gi|134547651|gb|EBB99474.1| hypothetical protein GOS_141611 [marine metagenome]


	CPU calculated 1373 chunks!

	CPU recalculated 99 sequence(s)!

	Xeon Phi calculated 1747 chunks!

	Xeon Phi recalculated 0 sequence(s)!

	Time : 12.860000s

	Query length = 1022

	Residues = 1224211871

	GCUPS = 97.289621

`	  			 	
##Options:

`	Usage: XSW [-h] [-g num] [-e num] [-p num] [-a num] [-m num] [-c num] matrix query db

    		-h       : this help message

    		-g num   : gap open          (default 11)

    		-e num   : gap extention   (default 1)

    		-p num   : the number of xeon phi to use (default 1)

    		-a num   : threads number on CPU (default 12)

    		-m num   : minimum score to be displayed (default 0)

    		-c num   : number of scores to be displayed (default 10)

    		matrix   : scoring matrix file

    		query    : query sequence file (fasta format)

    		db       : sequence database file (fasta format)

`

##Known issue(s):
* 1.symbol lookup error: ./XSW: undefined symbol: __offload_register_image : 
	  Please check your intel(R) Compiler version,  Intel(R) Compiler 2013 SP1 is highly recommended.
