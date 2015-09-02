I wrote two small perl programs/scripts that can convert tables of rust readings into numeric numbers according to published scales. In case of complex readings such as seedling reading ";1242-3+" a double weighting of the first reading was used for mean calculation. For adult plant rust data conversion, a similar double weighting method was proposed by Dr. Matt Rouse (USDA-CDL) and implemented in our programs.

### Note: Following the convention in perl, the column numbers are counted from zero, thus, 5,7,9 ... means columns 6,8,10 .....etc.
### Note2: Somebody met an error trying to work with Mac version files. For the time being, please save your excel tab of phenotype data as "windows formated text". Click on file--> save as --> windows formated text.  Please add one more header lines for Mac converted text files, as some of the header lines tend to be messed up (will follow on working to improve the code/programs when I got time)
### Note3: It is advised that you replace empty cells with NA or any other characters instead of leaving them blank. Otherwise, it might produce some warning messages, although, that should not affect the conversion results.




(1). seedling data conversion 

usage: perl convert_rust_reading.seedling.pl --typo typo.seedling.txt --pheno TCAP_seedling.txt --columns 5,7,9,11,13,15,17


My method differs from the Zhang et al PlosOne 2014 9(7) in the following:
(1) It tolerates unlimited number of segregations in your reading such as ";123-3+422+33333-33-";
(2) It uses all of the information (i.e., not just the first and last reading); it double weighs the first reading and keep the middle ones too. Let me know if you think this is not a good strategy.
(3) It is fully automated, all extra spaces, slashes, splitting and mathematic weighting and calculations will be taken care of
(4) It is written in perl; Mac machines (OS X 2002 or later) have perl pre-installed.  So the way you can use it, if you have a Mac, is simply dowload all these attachements into one folder. Open terminal, navigate to  the folder using "cd ~/Downloads/folderGWAS" (replace path with your actual folder path); then type command line. That said, the programs are also compatible for Windows files, as long as you know how to access a Linux like system (either local or via SSH), or you know how to install perl in your local Windows machine.

(2). Adult plant rust data conversion

usage 1: perl convert_rust_reading.field.pl --typo typo.field.txt --pheno TCAP_field1.txt --columns 5,7
usage 2: perl convert_rust_reading.field.multiplex.pl --typo typo.field.txt --pheno pheno_LrAM381_summary_Liang2015.txt  --columns 3,4,5,6,7

Usage 1 is for conversion of a single trait yet with two readings at different time of the years, 2nd reading will replace the first reading;  Whereas usage 2 is for conversion of multiple traits or the same trait under multiple environments. The first one only takes two readings; the second one (just like the seedling phenotype data) can practically unlimitted number of columns or readings.

The scales for adult plant rust response types are based on published Stubbs 1986 CIMMYT mannual. The calculation of severity, response and coeficient of infection are similarly double weighted by the first reading. 

Both the two programs are designed to take two input files (not just one phenotype file). The typo files (in both seedling and adult plant data conversion) allow more flexible and automatic control of data conversion. That said, I want to make it clear that the program is already written to avoid ambiguous regular expression matches, so even if the users simply provide a blank typo files or the same one as supplied with our example data, the conversion should perform smoothly for almost all the cases.

The author might consider rewrite the programs in Python, and implement the methods in an R function. If you use this script, or borrowed some of the methods for data conversion or algorithem designs, please cite an abstract or publication: "Gao, L., Turner, M. K., Chao S., Kolmer, J. and Anderson J. A. 2015 Genome wide association study (GWAS) of seedling and adult plant leaf rust resistance in elite wheat breeding lines. "

