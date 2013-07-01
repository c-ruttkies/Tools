= Requirements =

* Java 1.6
optional:
* PostgreSQL (for local structure database usage)


= Usage =

General commandline command:
> java -jar MetFragCommandLineTool.jar


Help:
> java -jar MetFragCommandLineTool.jar -h


Mandatory parameters:
* query file (option: -D)
* exact (monoisotopic) mass (in Da) of the measured compound (option: -n)
* sample name (option: -S)

Example:
> java -jar MetFragCommandLineTool.jar -D example.mb -n 272.06847 -S example

The query file (-D example.mb) contains the peak list with mass intensity pairs. An example is given by 
> java -jar MetFragCommandLineTool.jar -e
 # Sample: Naringenin
 # ID: C06561,C00509,C16232
 # Parent Mass: 272.06847
 # Search PPM: 10
 # Mode: 3
 # Charge: 1
 119.051 467.616
 123.044 370.662
 147.044 6078.145
 153.019 10000.0
 179.036 141.192
 189.058 176.358
 273.076 10000.000
 274.083 318.003

Lines starting with # are used to set parameters directly in the query file. 
* Sample -> sample name (-S)
* ID -> database ids (-i) (are specific for the selected database; here: KEGG)
* Parent Mass -> exact (monisotopic) mass of measured compound (-n)
* Search PPM -> mass deviation used to select candidates of the database (-p)
* Mode -> mode of measured compoung ([M+H], [M-H], [M]) (-M)
* Charge -> charge of measured compound (positive, negative) (-C)

Note: The parameters given in the query file are overwritten when set with the commandline option.

== Datebases ==
Databases that can be used for selecting structure candidates (-d):
Online:
* KEGG (http://www.genome.jp/kegg/)
* PubChem (http://pubchem.ncbi.nlm.nih.gov/)
* ChemSpider (http://www.chemspider.com/)
Local:
* SDF
(* local PostgreSQL)

The databases can be queried by the following paramteres in the given priority if serveral options are specified:
1) database ids (-i)
2) molecular formula (-f)
3) monoisotopic mass (-n)

Note: The given database ids are specific for the selected database (KEGG: C00509 -> Naringenin).

For using ChemSpider database a ChemSpider token (-c) is needed. When selecting -d sdf an additional parameter (-L) has to be set with the location of the sdf containing the structure candidates. 
In this case a mass deviation (-p) can also be defined to filter the structures given in the sdf by the given mass. If no mass deviation is specified in this case all strcutures in the sdf are considered.


= Output =
The output files are writen to the directory specified by the user (-R). By default the temp directory is used.
Output files are:
* sdf of the candidates processed
optional:
* sdfs containing assigned fragments of each of the processed candidates (-F)
* file containing parameters used for processing (-P)


= Questions & Problems =
Please contact cruttkie@ipb-halle.de