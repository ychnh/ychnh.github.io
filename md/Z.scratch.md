# Plan of operations

* Get the dict[fold][fam]
* generate data split dict[fold] = train:[fam, fam], test:[fam, fam]

* generate flat list, save flat list 
* generate the fasta files for train, test
* run mmseq -> determine which ones to remove from test
* remove from the flat list

