## Gal10 ##

I have chosen to create phylogenies of yeasts based off of the conserved gene Gal10. Gal10 encodes the enzyme UDP-glucose-4-epimerase, which catalyzes conversion of UDP-galactose to UDP-glucose. Without an enzyme like this, yeast species are unable to metabolize and consume galactose. This makes it a very interesting candidate gene for geneticists who would like to see relationships in species with this enzyme as well as to do wet lab research on galactose consumption.

The goal of this project is to build phylogenies from 20-100 gal10 gene sequences of different yeast species. 

To start this project, I copied 20 fasta files from NCBI of GAL10 genes from diferent yeast species
Then I decided Busco would be best for Quality control

## Trial and Error ##

Downloaded miniconda for busco installation
miniconda was unable to solve environment
uninstalled miniconda

Installed the larger program Anaconda via browser
Attmpted to run 
  
    >conda install -c "bioconda/label/cf201901" busco
  
in the interface, but was given this error:

Solving environment: failed with initial frozen solve. Retrying with flexible solve.

PackagesNotFoundError: The following packages are not available from current channels:

  - busco

Current channels:

  - https://conda.anaconda.org/bioconda/label/cf201901/win-64
  - https://conda.anaconda.org/bioconda/label/cf201901/noarch
  - https://repo.anaconda.com/pkgs/main/win-64
  - https://repo.anaconda.com/pkgs/main/noarch
  - https://repo.anaconda.com/pkgs/r/win-64
  - https://repo.anaconda.com/pkgs/r/noarch
  - https://repo.anaconda.com/pkgs/msys2/win-64
  - https://repo.anaconda.com/pkgs/msys2/noarch

To search for alternate channels that may provide the conda package you're
looking for, navigate to

    https://anaconda.org

and use the search bar at the top of the page.

Attempted to run

   >conda install -c bioconda busco

was given this error:
Solving environment: failed with initial frozen solve. Retrying with flexible solve.
Solving environment: -
Found conflicts! Looking for incompatible packages.
This can take several minutes.  Press CTRL-C to abort.
failed

UnsatisfiableError: The following specifications were found to be incompatible with each other:

Output in format: Requested package -> Available versions 

Attempted to type 

    >conda info 

to understand my conda package and was blessed with this error:
>>> conda info
  File "<stdin>", line 1
    conda info
          ^
SyntaxError: invalid syntax
  
Used
  
    >quit()
  
to exit the interactive pyhton shell
Now able to type in the anaconda prompt wihtout syntax errors
                  
    >conda install -c "bioconda/label/cf201901" busco
  
and was given the same error
Ran 
  
    >conda create -n BUSCO -c bioconda -c conda-forge busco=5.4.5 python=3.9.13 conda activate BUSCO
  
and was given this same error:
Solving environment: failed

PackagesNotFoundError: The following packages are not available from current channels:

  - activate

Current channels:

  - https://conda.anaconda.org/bioconda/win-64
  - https://conda.anaconda.org/bioconda/noarch
  - https://conda.anaconda.org/conda-forge/win-64
  - https://conda.anaconda.org/conda-forge/noarch
  - https://repo.anaconda.com/pkgs/main/win-64
  - https://repo.anaconda.com/pkgs/main/noarch
  - https://repo.anaconda.com/pkgs/r/win-64
  - https://repo.anaconda.com/pkgs/r/noarch
  - https://repo.anaconda.com/pkgs/msys2/win-64
  - https://repo.anaconda.com/pkgs/msys2/noarch

To search for alternate channels that may provide the conda package you're
looking for, navigate to

    https://anaconda.org

and use the search bar at the top of the page. 
Ran 
  
    >conda install -c conda-forge -c bioconda busco=5.4.4
  
and got this error:
Collecting package metadata (current_repodata.json): failed

CondaHTTPError: HTTP 000 CONNECTION FAILED for url <https://conda.anaconda.org/conda-forge/win-64/current_repodata.json>
Elapsed: -

An HTTP error occurred when trying to retrieve this URL.
HTTP errors are often intermittent, and a simple retry will get you on your way.
'https//conda.anaconda.org/conda-forge/win-64'
    
Forgot to turn the WI-FI on
Ran 
  
   >conda install -c conda-forge -c bioconda busco=5.4.4 
  
again
It was unable to understand the environment
I then attmpted this command 
  
   >conda create -p /vol/bigdata/BUSCO
  
which gave me this:
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 22.9.0
  latest version: 23.1.0

Please update conda by running

    $ conda update -n base -c defaults conda

  environment location: C:\vol\bigdata\BUSCO



Proceed ([y]/n)?

    >n 
      
Then ran:
  
   >conda update -n base -c defaults conda
  
which successfully updated conda
    
Then I attempted this command again 
  
   >conda create -p /vol/bigdata/BUSCO
  
which gave me the same option as above but without the notification to update
Next I ran this 
  
    >conda activate C:\vol\bigdata\BUSCO
  
which activated the busco specific environment
I then ran this 
  
    >conda install -p /vol/bigdata/BUSCO -c conda-forge -c bioconda busco=5.4.5
  
which gave me this error
Collecting package metadata (current_repodata.json): failed

CondaSSLError: OpenSSL appears to be unavailable on this machine. OpenSSL is required to
download and install packages.

Exception: HTTPSConnectionPool(host='conda.anaconda.org', port=443): Max retries exceeded with url: /conda-forge/win-64/current_repodata.json (Caused by SSLError("Can't connect to HTTPS URL because the SSL module is not available."))

I then close my prompt and reopened it and ran these commands
  
    >conda deactivate
    
    >conda activate base
    
    >conda install -n python=3.9
    
    >conda create -n scipy-env scipy
    
    >conda activate scipy-env
    
to "create a test environment"
Also of note I had to run
  
    >conda deactivate
  
to leave the env before I ran
  
    >conda env remove -n scipy-env
  
to remove the test environment
 In post this seems useless
    
I then ran
  
    >conda update --all
    
I gave up on conda for now, and dowloaded a linux shell for windows.
  
Basically, I never resolved this issue and didn't use BUSCO on my data. However, my data never needed any type of quality control. Basically, my data is already quality contolled because I took the data off of a public database (NCBI). The sequences are submitted after being confirmed by other like sequences of the same genes. To explain this a little bit more, if I were using genomes and aligning genomes to each other then I wouls need to use some QC site/program, but since I am using a signle gene they have built-in QC because of their nature.
  
 ## Alignment and R ##  
  
I installed some alignment programs using  

  >sudo apt install clustalo
    
and similarly for muscle I used
    
    >sudo apt install muscle
  
  
I then added 20 sequences to my GAL10 data because I thought it would be cool to make a larger tree.
then to align my data I used
  
    >clustalo --in gal10dntp.fasta --out gal10dntp.align --force --outfmt clustal --wrap 80
       
In class we looked to create distance-based and parsimony-based trees for our data. Here are the commands I used for the parsimony tree in RStudio.
    
    >library(ape)
  
    >library(phangorn)
  
    >library(adegenet)
  
    >dna <- fasta2DNAbin(file="gal10aaaling.fasta")
       
    >dna2 <- as.phyDat(dna)
  
    >tre.ini <- nj(dist.dna(dna,model="raw"))
           
    >parsimony(tre.ini, dna2)
    
   I am unsure why, but once the parsiomny command is used, it gives those using AA sequences an error that crashes R. 
Here are the commands I used for the distance based tree. 
    
    >library(ape)
  
    >library(adegenet)
  
    >library(phangorn)
  
    >dna <- fasta2DNAbin(file="gal10aaaling.fasta")
            
    >D <- dist.dna(dna, model="TN93")
          
    >tre <- nj(D)
            
    >tre <- ladderize(tre)
            
    >plot(tre, cex=.6)
  
    >title("A simple NJ tree")

This tree worked, but I think because we tried to convert Amino acids back into nucleotides the tree is quite bad, as everything is on the same line.
    
**Also, at some point between the start of this log file and making these tree, I added 15 fasta sequences to make it 35 total. There are 2-3 non yeast fungi and a duplicate, all taken off of NCBI in the file: Gal10_AA.fasta** 
                        
## Tree building and realignment ##
                        
Now, we want to make trees from our alignments. 
I made a tree earlier, which will be in the data file, but the tips are all mislabeled and hard to understand so I redid the alignments as such.
    
    >Sudo apt install mafft
    >mafft -h
    >mafft 
    which automatically asks
Input file? (FASTA format; Folder=/mnt/c/users/quaid)

    >Gal10_AA.fasta 
    
Output file?

    >Gal10AA.align.fasta
    
Output format?
  1. Clustal format / Sorted
  2. Clustal format / Input order
  3. Fasta format   / Sorted
  4. Fasta format   / Input order
  5. Phylip format  / Sorted
  6. Phylip format  / Input order

    >3
    
Strategy?
  1. --auto
  2. FFT-NS-1 (fast)
  3. FFT-NS-2 (default)
  4. G-INS-i  (accurate)
  5. L-INS-i  (accurate)
  6. E-INS-i  (accurate)

    >3<
    
Additional arguments? (--ep # --op # --kappa # etc)

    >
    
command=
"/usr/bin/mafft"  --retree 2 --reorder "gal10_AA.fasta" > "gal10AA.align.fasta"
Type Y or just enter to run this command.

    >Y
    
I then did the same with clustalo: 
    
    >sudo apt install clustalo
    >clustalo --in gal10_AA.fasta --out gal10AAC.align.fasta

With these I made 4 trees, 1 of each alignment in IQtree2 and RAXml:
    
    >sudo apt install iqtree
    >sudo apt install raxml
    >iqtree2 -s gal10AA.align.fasta
    >iqtree2 -s gal10AAC.align.fasta -m LG+G4
    >raxmlHPC-PTHREADS-AVX -T 2 -s gal10aa.align.fasta -n gal10aa.treefile -m PROTGAMMALG4X -p 32 [X]
    >raxmlHPC-PTHREADS-AVX -T 2 -s gal10aac.align.fasta -n gal10aac.treefile -m PROTGAMMALG4X -p 32 [X]
    
The output files are should all be in data_raw 

 IQtree2 is the most updated verion of the most used tree-building algorithm. It starts by building a parsimony tree and using NNI moves to find maximum likelihood trees. It also uses substitution models as references to be able to make these maximum likelihood trees. 
    
RAxML is itself not the most updated version. I have never installed programs without using WSL so I decided I did not want to download and unpackage RAxML-NG and to just use RAxML. RAxML's creators have said that the program is maybe faster, but definitely not as accurate as iqtree. RAxML uses SPR (pruning and regrafting) to find its maximum likelihood trees. It also uses substitution models to accomplish this, with albeit less models available. 
    
I placed the rooted treefiles into data_clean
  
  ## Organization ##
  
My files seem like they are all over the place, so here I will clarify the flow of my files and folders.
All of my files thus far are inside of data_raw and data_clean. We should start within data_raw to find Gal10AA.fasta. This is the file that contains all 35 of my gal10 sequences with correct taxa names. From this, alignments were created with mafft and then clustalo. To differentiate these alignments I added a C into Gal10AAC.align.fasta to show that file is the clustalo output and the other more standard Gal10AA.align.fasta is the mafft output file. Also within the base level of the data_raw folder residesa nexus format file used for mrbayes. The folders within data_raw are pretty self explanatory, containing the respective output files from tree running softwares RAXml and IQtree2 on each respective alignment. 
Then, data_clean contains .pdf files created on Interactive Tree of Life (ITOL, a tree viewer used to visualize trees from their paranthetical output files.) Each one has a self explanatory name, with an added C to specify clustalo and .RAX to specify RAXml was used for that file. 
  
  ## MrBayes ##
  
Inside of the ubuntu interface I installed mrbayes using;
  
  >sudo apt install mrbayes
  
I then opened the mafft output file Gal10AA.align.fasta in UNIPRO Ugene and copied/downloaded it into a nexus format using that program. I attempted to use the block provided for us;
  
  begin mrbayes;
 set autoclose=yes;
 prset brlenspr=unconstrained:exp(10.0);
 prset shapepr=exp(1.0);
 prset tratiopr=beta(1.0,1.0);
 prset statefreqpr=dirichlet(1.0,1.0,1.0,1.0);
 lset nst=2 rates=gamma ngammacat=4;
 mcmcp ngen=10000 samplefreq=10 printfreq=100 nruns=1 nchains=3 savebrlens=yes;
end;
  
However, I received an error.
  
  >mb
  >exe gal10AA.align_copy1.nex
  
        Too many taxa in matrix
      Deleting previously defined characters
      Deleting previously defined taxa
      Error when setting parameter "MatrixInfo" (2)
      The error occurred when reading char. 1-5 on line 43
         in the file 'gal10aacopy.nex'

   Returning execution to command line ...

   Error in command "Execute"
  
line 43 reads; begin mrbayes;
  I deleted the portion of the nexus file that specified where the reading of the file ended and the beginning of mrbayes begun, the program read them all together and couldn't process the transition. Thus I added that back to the block and made some changes to make it more fitting to amino acid data;
  
  ;
end;
begin mrbayes;
 set autoclose=yes;
 prset brlenspr=unconstrained:exp(10.0);
 prset shapepr=exp(1.0);
 prset aamodelpr=mixed;
 lset nst=2 rates=gamma ngammacat=6;
 mcmcp ngen=2500000 samplefreq=100 printfreq=1000 nruns=2 nchains=3 savebrlens=yes;
end;
  
I was able to run this command, but I received a different error when attempting to run mcmc:
  
  >mb
  >exe gal10AA.align_copy1.nex
  >mcmc
  
  Running benchmarks to automatically select fastest BEAGLE resource... failed to open /dev/dri/renderD128: Permission denied
failed to open /dev/dri/renderD128: Permission denied

OpenCL error: CL_DEVICE_NOT_FOUND from file <GPUInterfaceOpenCL.cpp>, line 122.
  
I figured this was a driver error, so I installed gcc using;
  
  >sudo apt install gcc
  
But had no luck running the program again. I attempted to use something to build Beagle, but that didn't seem to work either. I'm looking into how wsl interacts with opencl but am having no luck deciding if it's really worth installing a program like that. 
  
