##Program and Data Preparation
* Change work dir to native:

	`cd XSW/native/`

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

* Three files must be provided to run XSW: the scoring matrix, query sequence and the database. blosum62.mat is provided as the default scoring matrix.The query sequence and database should be in FASTA format. 
* For example, steps to run the query testRefSeq0511.txt to the database db.env_nr with the default gap penalties and scoring matrix are as following:	

* Step 1: Preproccess the database:

	`./makemicdb.out db.env_nr 244`

	 [NOTE:] if your Xeon Phi has 61 cores, it is 244, if 60 cores it is 240.

* Step 2: Upload the database and program to xeon phi:

	`scp db.env_nr*.* blosum62.mat testRef* XSW mic0:`

* Step 3: Login xeon phi card:

	`ssh mic0`

* Step 4: Run XSW on xeon phi:

	`./XSW  blosum62.mat testRefSeq0511.txt  db.env_nr`


##Screen Output:

`	testRefSeq0511.txt vs db.env_nr

	Matrix: blosum62.mat, gap_open: 11, gap_extend_open: 1


	Score  Description

        618  >gi|143361067|gb|EDE55525.1| hypothetical protein GOS_1110460 [marine metagenome]

        594  >gi|135202882|gb|EBG14753.1| hypothetical protein GOS_9482059 [marine metagenome]

        587  >gi|402681658|gb|EJX05232.1| bifunctional NADH:ubiquinone oxidoreductase subunit C/D [gut metagenome]

        497  >gi|136486216|gb|EBO47492.1| hypothetical protein GOS_8074195 [marine metagenome]

        446  >gi|136253269|gb|EBM91275.1| hypothetical protein GOS_8332376 [marine metagenome]

        431  >gi|135408601|gb|EBH43929.1| hypothetical protein GOS_9262408 [marine metagenome]

        428  >gi|142690261|gb|ECZ87559.1| hypothetical protein GOS_2104459 [marine metagenome]

        421  >gi|140983057|gb|ECO83629.1| hypothetical protein GOS_3881951 [marine metagenome]

        419  >gi|140676288|gb|ECM74653.1| hypothetical protein GOS_5185030 [marine metagenome]

        419  >gi|135216851|gb|EBG22991.1| hypothetical protein GOS_9468369 [marine metagenome]


	Query length = 511

	Residues = 1224211871

	Time : 9.154000s

	GCUPS = 68.338680
`
	  			 	
##Options:

`	Usage: XSW [-h] [-g num] [-e num] [-p num] [-m num] [-c num] matrix query db

			-h       : this help message

			-g num   : gap open          (default 11)

			-e num   : gap extend open   (default 1)

			-p num   : threads number (default 244)

			-m num   : minimum score to be displayed (default 0)

			-c num   : number of scores to be displayed (default 10)

			matrix   : scoring matrix file

			query    : query sequence file (fasta format)

			db       : sequence database file (fasta format)

`
