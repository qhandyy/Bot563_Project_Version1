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
  
  ## Astral ##
  
There is no direct installation for Astral, so I downloaded a zip file to my computer and unzipped to be able to use the program. I relocated my mafft iqtree tree to the folder for this analysis. I used 
  
  >java -jar astral.5.7.8.jar -i Gal10AA.align.fasta.treefile
  
This worked and gave me an astral file output (Gal10AA.astral), but its usage is limited since my data only contain 1 gene so the coalescent has no way of heightening my data. I took a photo of the tree and added into the data_clean folder in the repository as well. 
  
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
  Average standard deviation of split frequencies: 0.008882

   Analysis completed in 3 hours 48 mins 33 seconds
   Analysis used 13479.07 seconds of CPU time
   Likelihood of best state for "cold" chain of run 1 was -29933.69
   Likelihood of best state for "cold" chain of run 2 was -29934.34

   Acceptance rates for the moves in the "cold" chain of run 1:
      With prob.   (last 1000)   chain accepted proposals by move
          2.2 %     (  1 %)     ExtSPR(Tau,V)
          1.7 %     (  2 %)     ExtTBR(Tau,V)
          3.0 %     (  2 %)     NNI(Tau,V)
          2.6 %     (  2 %)     ParsSPR(Tau,V)
          3.1 %     (  2 %)     ParsTBR(Tau,V)
         26.3 %     ( 25 %)     Multiplier(V)
         17.9 %     ( 20 %)     Nodeslider(V)
          3.8 %     (  4 %)     TLMultiplier(V)
          0.0 %     (  0 %)     Uniform(Aamodel)

   Acceptance rates for the moves in the "cold" chain of run 2:
      With prob.   (last 1000)   chain accepted proposals by move
          2.1 %     (  2 %)     ExtSPR(Tau,V)
          1.7 %     (  2 %)     ExtTBR(Tau,V)
          2.7 %     (  3 %)     NNI(Tau,V)
          2.2 %     (  2 %)     ParsSPR(Tau,V)
          2.9 %     (  3 %)     ParsTBR(Tau,V)
         26.4 %     ( 27 %)     Multiplier(V)
         18.0 %     ( 17 %)     Nodeslider(V)
          3.9 %     (  4 %)     TLMultiplier(V)
          0.0 %     (  0 %)     Uniform(Aamodel)

   Chain swap information for run 1:

                1       2       3
        --------------------------
      1 |            0.68    0.43
      2 |  166915            0.71
      3 |  166484  166601

   Chain swap information for run 2:

                1       2       3
        --------------------------
      1 |            0.66    0.40
      2 |  166095            0.68
      3 |  166911  166994

   Upper diagonal: Proportion of successful state exchanges between chains
   Lower diagonal: Number of attempted state exchanges between chains

   Chain information:

     ID -- Heat
    -----------
      1 -- 1.00  (cold chain)
      2 -- 0.91
      3 -- 0.83

   Heat = 1 / (1 + T * (ID - 1))
      (where T = 0.10 is the temperature and ID is the chain number)



     Setting sumt nruns to 2
   Summarizing trees in files "Gal10AA.align_copy1.nex.run1.t" and "Gal10AA.align_copy1.nex.run2.t"
   Using relative burnin ('relburnin=yes'), discarding the first 25 % of sampled trees
   Writing statistics to files Gal10AA.align_copy1.nex.<parts|tstat|vstat|trprobs|con>
   Examining first file ...
   Found one tree block in file "Gal10AA.align_copy1.nex.run1.t" with 5001 trees in last block
   Expecting the same number of trees in the last tree block of all files

   Tree reading status:

   0      10      20      30      40      50      60      70      80      90     100
   v-------v-------v-------v-------v-------v-------v-------v-------v-------v-------v
   *********************************************************************************

   Read a total of 10002 trees in 2 files (sampling 7502 of them)
      (Each file contained 5001 trees of which 3751 were sampled)

   General explanation:

   In an unrooted tree, a taxon bipartition (split) is specified by removing a
   branch, thereby dividing the species into those to the left and those to the
   right of the branch. Here, taxa to one side of the removed branch are denoted
   '.' and those to the other side are denoted '*'. Specifically, the '.' symbol
   is used for the taxa on the same side as the outgroup.

   In a rooted or clock tree, the tree is rooted using the model and not by
   reference to an outgroup. Each bipartition therefore corresponds to a clade,
   that is, a group that includes all the descendants of a particular branch in
   the tree.  Taxa that are included in each clade are denoted using '*', and
   taxa that are not included are denoted using the '.' symbol.

   The output first includes a key to all the bipartitions with frequency larger
   or equal to (Minpartfreq) in at least one run. Minpartfreq is a parameter to
   sumt command and currently it is set to 0.10.  This is followed by a table
   with statistics for the informative bipartitions (those including at least
   two taxa), sorted from highest to lowest probability. For each bipartition,
   the table gives the number of times the partition or split was observed in all
   runs (#obs) and the posterior probability of the bipartition (Probab.), which
   is the same as the split frequency. If several runs are summarized, this is
   followed by the minimum split frequency (Min(s)), the maximum frequency
   (Max(s)), and the standard deviation of frequencies (Stddev(s)) across runs.
   The latter value should approach 0 for all bipartitions as MCMC runs converge.

   This is followed by a table summarizing branch lengths, node heights (if a
   clock model was used) and relaxed clock parameters (if a relaxed clock model
   was used). The mean, variance, and 95 % credible interval are given for each
   of these parameters. If several runs are summarized, the potential scale
   reduction factor (PSRF) is also given; it should approach 1 as runs converge.
   Node heights will take calibration points into account, if such points were
   used in the analysis.

   Note that Stddev may be unreliable if the partition is not present in all
   runs (the last column indicates the number of runs that sampled the partition
   if more than one run is summarized). The PSRF is not calculated at all if
   the partition is not present in all runs.The PSRF is also sensitive to small
   sample sizes and it should only be considered a rough guide to convergence
   since some of the assumptions allowing one to interpret it as a true potential
   scale reduction factor are violated in MrBayes.

   List of taxa in bipartitions:

      1 -- Saccharomyces_cerevisiae
      2 -- Saccharomyces_paradoxus
      3 -- Kazachstania_unispora
      4 -- Kazachstania_exigua
      5 -- Torulaspora_delbrueckii
      6 -- Zygotorulaspora_mrakii
      7 -- Lachancea_fermentati
      8 -- Zygosaccharomyces_bailii
      9 -- Zygosaccharomyces_rouxii
     10 -- Zygosaccharomyces_mellis
     11 -- Kluyveromyces_lactis
     12 -- Kluyveromyces_marxianus
     13 -- Brettanomyces_bruxellensis
     14 -- Brettanomyces_nanus
     15 -- Candida_margitis
     16 -- Candida_theae
     17 -- Candida_metapsilosis
     18 -- Candida_parapsilosis
     19 -- Candida_oxycetoniae
     20 -- Candida_jiufengensis
     21 -- Candida_pseudojiufengensis
     22 -- Candida_subhashii
     23 -- Candida_albicans
     24 -- Candida_viswanathii
     25 -- Scheffersomyces_stipitis
     26 -- Schizosaccharomyces_pombe
     27 -- Debaryomyces_fabryi
     28 -- Schizosaccharomyces_osmophilus
     29 -- Clavispora_lusitaniae
     30 -- Candida_railenensis
     31 -- Schizosaccharomyces_japonicus
     32 -- Schizosaccharomyces_japonicus2
     33 -- Purpureocillium_lilacinum
     34 -- Gonapodya_sp.
     35 -- Rhizopus_azygosporus

   Key to taxon bipartitions (saved to file "Gal10AA.align_copy1.nex.parts"):

   ID -- Partition
   -----------------------------------------
    1 -- .**********************************
    2 -- .*.................................
    3 -- ..*................................
    4 -- ...*...............................
    5 -- ....*..............................
    6 -- .....*.............................
    7 -- ......*............................
    8 -- .......*...........................
    9 -- ........*..........................
   10 -- .........*.........................
   11 -- ..........*........................
   12 -- ...........*.......................
   13 -- ............*......................
   14 -- .............*.....................
   15 -- ..............*....................
   16 -- ...............*...................
   17 -- ................*..................
   18 -- .................*.................
   19 -- ..................*................
   20 -- ...................*...............
   21 -- ....................*..............
   22 -- .....................*.............
   23 -- ......................*............
   24 -- .......................*...........
   25 -- ........................*..........
   26 -- .........................*.........
   27 -- ..........................*........
   28 -- ...........................*.......
   29 -- ............................*......
   30 -- .............................*.....
   31 -- ..............................*....
   32 -- ...............................*...
   33 -- ................................*..
   34 -- .................................*.
   35 -- ..................................*
   36 -- ..**...............................
   37 -- ............***********************
   38 -- .........................***..**...
   39 -- ......................**...........
   40 -- .......***.........................
   41 -- ...............**..................
   42 -- ...........................*..**...
   43 -- ..............................**...
   44 -- ........**.........................
   45 -- ...................**..............
   46 -- ..*********************************
   47 -- .....................*..*..........
   48 -- ..........**.......................
   49 -- ..............****.................
   50 -- ..............*******..............
   51 -- ....*******************************
   52 -- ......*...*************************
   53 -- ....**.............................
   54 -- ......*****************************
   55 -- .....................****..........
   56 -- ..............***********..........
   57 -- ............**.....................
   58 -- ..............****.**..............
   59 -- ............**...........****.**...
   60 -- ............*****************.**...
   61 -- ............**..............*......
   62 -- ..........*************************
   63 -- ............********************...
   64 -- .................................**
   65 -- .........................**........
   66 -- ................................***
   67 -- ..............*..*.................
   68 -- ...............***.................
   69 -- ............********************.**
   70 -- .........................*.*..**...
   -----------------------------------------

   Summary statistics for informative taxon bipartitions
      (saved to file "Gal10AA.align_copy1.nex.tstat"):

   ID   #obs    Probab.     Sd(s)+      Min(s)      Max(s)   Nruns
   ----------------------------------------------------------------
   36  7502    1.000000    0.000000    1.000000    1.000000    2
   37  7502    1.000000    0.000000    1.000000    1.000000    2
   38  7502    1.000000    0.000000    1.000000    1.000000    2
   39  7502    1.000000    0.000000    1.000000    1.000000    2
   40  7502    1.000000    0.000000    1.000000    1.000000    2
   41  7502    1.000000    0.000000    1.000000    1.000000    2
   42  7502    1.000000    0.000000    1.000000    1.000000    2
   43  7502    1.000000    0.000000    1.000000    1.000000    2
   44  7502    1.000000    0.000000    1.000000    1.000000    2
   45  7502    1.000000    0.000000    1.000000    1.000000    2
   46  7502    1.000000    0.000000    1.000000    1.000000    2
   47  7502    1.000000    0.000000    1.000000    1.000000    2
   48  7502    1.000000    0.000000    1.000000    1.000000    2
   49  7502    1.000000    0.000000    1.000000    1.000000    2
   50  7502    1.000000    0.000000    1.000000    1.000000    2
   51  7502    1.000000    0.000000    1.000000    1.000000    2
   52  7502    1.000000    0.000000    1.000000    1.000000    2
   53  7502    1.000000    0.000000    1.000000    1.000000    2
   54  7502    1.000000    0.000000    1.000000    1.000000    2
   55  7502    1.000000    0.000000    1.000000    1.000000    2
   56  7496    0.999200    0.001131    0.998400    1.000000    2
   57  7406    0.987203    0.018097    0.974407    1.000000    2
   58  7377    0.983338    0.001697    0.982138    0.984537    2
   59  7304    0.973607    0.037325    0.947214    1.000000    2
   60  7278    0.970141    0.036194    0.944548    0.995734    2
   61  7250    0.966409    0.035817    0.941082    0.991736    2
   62  7184    0.957611    0.003016    0.955479    0.959744    2
   63  7089    0.944948    0.043546    0.914156    0.975740    2
   64  6508    0.867502    0.012442    0.858704    0.876300    2
   65  6013    0.801520    0.022810    0.785391    0.817649    2
   66  4586    0.611304    0.036948    0.585177    0.637430    2
   67  4039    0.538390    0.002828    0.536390    0.540389    2
   68  3141    0.418688    0.001697    0.417489    0.419888    2
   69  2213    0.294988    0.034498    0.270595    0.319381    2
   70  1489    0.198480    0.022810    0.182351    0.214609    2
   ----------------------------------------------------------------
   + Convergence diagnostic (standard deviation of split frequencies)
     should approach 0.0 as runs converge.


   Summary statistics for branch and node parameters
      (saved to file "Gal10AA.align_copy1.nex.vstat"):

                                           95% HPD Interval
                                         --------------------
   Parameter      Mean       Variance     Lower       Upper       Median     PSRF+  Nruns
   --------------------------------------------------------------------------------------
   length[1]     0.040022    0.000074    0.023547    0.056695    0.039573    1.000    2
   length[2]     0.032640    0.000067    0.016888    0.048512    0.032027    1.000    2
   length[3]     0.136293    0.000282    0.105042    0.168291    0.135952    1.000    2
   length[4]     0.184986    0.000347    0.147495    0.220117    0.184406    1.002    2
   length[5]     0.161044    0.000310    0.124144    0.193398    0.160069    1.000    2
   length[6]     0.113091    0.000253    0.084418    0.146232    0.112356    1.000    2
   length[7]     0.290725    0.000718    0.237144    0.341728    0.290009    1.000    2
   length[8]     0.169327    0.000414    0.129359    0.209303    0.168060    1.003    2
   length[9]     0.079794    0.000187    0.054619    0.106630    0.078658    1.000    2
   length[10]    0.126962    0.000253    0.097780    0.159918    0.126446    1.000    2
   length[11]    0.097339    0.000239    0.069849    0.130076    0.096327    1.000    2
   length[12]    0.098097    0.000256    0.068775    0.130288    0.097570    1.000    2
   length[13]    0.295850    0.000738    0.246819    0.352152    0.295037    1.006    2
   length[14]    0.176941    0.000489    0.133668    0.220497    0.176453    1.000    2
   length[15]    0.082212    0.000174    0.057067    0.108180    0.081850    1.000    2
   length[16]    0.109948    0.000195    0.083140    0.137903    0.109737    1.000    2
   length[17]    0.073962    0.000147    0.051103    0.097869    0.073366    1.000    2
   length[18]    0.093260    0.000182    0.066363    0.119158    0.092776    1.000    2
   length[19]    0.190445    0.000364    0.154578    0.229021    0.190192    1.000    2
   length[20]    0.085478    0.000184    0.059735    0.112954    0.084692    1.001    2
   length[21]    0.129142    0.000247    0.097596    0.157879    0.128564    1.000    2
   length[22]    0.128821    0.000259    0.099043    0.161897    0.128353    1.000    2
   length[23]    0.088270    0.000171    0.063921    0.114431    0.087848    1.000    2
   length[24]    0.128782    0.000230    0.102083    0.161805    0.128849    1.000    2
   length[25]    0.252243    0.000520    0.207587    0.295672    0.251326    1.000    2
   length[26]    0.227440    0.000463    0.183532    0.266894    0.226416    1.000    2
   length[27]    0.146777    0.000312    0.111197    0.179101    0.146141    1.001    2
   length[28]    0.212892    0.000455    0.171482    0.254716    0.212796    1.000    2
   length[29]    0.263075    0.000599    0.214345    0.309432    0.262453    1.000    2
   length[30]    0.240299    0.000571    0.196949    0.289931    0.239557    1.000    2
   length[31]    0.080880    0.000162    0.056362    0.105189    0.079675    1.001    2
   length[32]    0.040239    0.000099    0.021473    0.059584    0.039826    1.000    2
   length[33]    0.452376    0.002702    0.351351    0.549399    0.451565    1.003    2
   length[34]    0.803790    0.009663    0.623819    1.002903    0.799260    1.002    2
   length[35]    1.461624    0.014574    1.222128    1.696674    1.457558    1.000    2
   length[36]    0.055599    0.000159    0.030350    0.078773    0.054792    1.000    2
   length[37]    0.152133    0.000867    0.095514    0.208778    0.151208    1.001    2
   length[38]    0.092896    0.000259    0.062559    0.124552    0.091710    1.001    2
   length[39]    0.054886    0.000141    0.031390    0.077033    0.054320    1.000    2
   length[40]    0.232824    0.000581    0.185617    0.278102    0.232021    1.000    2
   length[41]    0.034071    0.000106    0.013644    0.053618    0.033563    1.000    2
   length[42]    0.067794    0.000238    0.039509    0.098590    0.066912    1.000    2
   length[43]    0.289423    0.000643    0.239190    0.337012    0.288864    1.000    2
   length[44]    0.129810    0.000338    0.093313    0.165176    0.129605    1.000    2
   length[45]    0.115466    0.000261    0.085516    0.147008    0.114801    1.000    2
   length[46]    0.127544    0.000270    0.094176    0.157791    0.126909    1.001    2
   length[47]    0.057293    0.000153    0.033823    0.081120    0.056698    1.000    2
   length[48]    0.299336    0.000801    0.244611    0.354720    0.298667    1.000    2
   length[49]    0.115625    0.000265    0.086246    0.149698    0.114468    1.001    2
   length[50]    0.059010    0.000166    0.035927    0.085548    0.058536    1.000    2
   length[51]    0.059197    0.000182    0.034957    0.086988    0.057857    1.000    2
   length[52]    0.084390    0.000330    0.050748    0.120495    0.083628    1.000    2
   length[53]    0.094055    0.000238    0.063710    0.123850    0.093490    1.000    2
   length[54]    0.056334    0.000225    0.027850    0.085725    0.055394    1.000    2
   length[55]    0.062513    0.000173    0.038717    0.089981    0.061462    1.000    2
   length[56]    0.091399    0.000276    0.058832    0.122696    0.090924    1.000    2
   length[57]    0.150005    0.000559    0.112148    0.197477    0.150114    1.005    2
   length[58]    0.038227    0.000114    0.017598    0.058909    0.037307    1.001    2
   length[59]    0.064905    0.000209    0.037789    0.092563    0.064051    1.000    2
   length[60]    0.067945    0.000260    0.038103    0.099957    0.067333    1.000    2
   length[61]    0.053668    0.000220    0.026386    0.084151    0.052803    1.000    2
   length[62]    0.061304    0.000299    0.029911    0.096441    0.060152    1.000    2
   length[63]    0.070870    0.000561    0.024140    0.118108    0.070069    1.000    2
   length[64]    0.182057    0.005371    0.041515    0.324495    0.178658    1.004    2
   length[65]    0.040678    0.000151    0.019062    0.065815    0.039274    1.000    2
   length[66]    0.063763    0.001109    0.002071    0.124606    0.060542    1.000    2
   length[67]    0.020384    0.000057    0.007166    0.035325    0.019732    1.000    2
   length[68]    0.022639    0.000075    0.006340    0.038728    0.022134    1.000    2
   length[69]    0.052383    0.000907    0.000842    0.108897    0.049560    1.009    2
   length[70]    0.041507    0.000174    0.018819    0.069368    0.040202    0.999    2
   --------------------------------------------------------------------------------------
   + Convergence diagnostic (PSRF = Potential Scale Reduction Factor; Gelman
     and Rubin, 1992) should approach 1.0 as runs converge. NA is reported when
     deviation of parameter values within all runs is 0 or when a parameter
     value (a branch length, for instance) is not sampled in all runs.


   Summary statistics for partitions with frequency >= 0.10 in at least one run:
       Average standard deviation of split frequencies = 0.008882
       Maximum standard deviation of split frequencies = 0.043546
       Average PSRF for parameter values (excluding NA and >10.0) = 1.001
       Maximum PSRF for parameter values = 1.009


   Clade credibility values:

   Subtree rooted at node 61:

        /----------------------------------------------------- Lachancea_ferme~ (7)
        |
        |                                               /----- Kluyveromyces_~ (11)
        |     /-------------------100-------------------+
        |     |                                         \----- Kluyveromyces_~ (12)
        |     |
        |     |                                         /----- Brettanomyces_~ (13)
        |     |                                   /--99-+
        |     |                                   |     \----- Brettanomyces_~ (14)
        |     |                         /----97---+
        |     |                         |         \----------- Clavispora_lus~ (29)
   --100+     |                         |
        |     |                         |               /----- Schizosaccharo~ (26)
        |     |              /----97----+    /----80----+
        |     |              |          |    |          \----- Debaryomyces_f~ (27)
        |     |              |          |    |
        |     |              |          \-100+    /----------- Schizosaccharo~ (28)
        |     |              |               |    |
        |     |              |               \-100+     /----- Schizosaccharo~ (31)
        |     |              |                    \-100-+
        |     |              |                          \----- Schizosaccharo~ (32)
        |     |              |
        \--96-+              |                          /----- Candida_margit~ (15)
              |              |                    /--54-+
              |         /-97-+                    |     \----- Candida_paraps~ (18)
              |         |    |               /-100+
              |         |    |               |    |     /----- Candida_theae (16)
              |         |    |               |    \-100-+
              |         |    |          /-98-+          \----- Candida_metaps~ (17)
              |         |    |          |    |
              |         |    |          |    |          /----- Candida_jiufen~ (20)
              |         |    |     /-100+    \----100---+
              |         |    |     |    |               \----- Candida_pseudo~ (21)
              |         |    |     |    |
              |    /-94-+    |     |    \--------------------- Candida_oxycet~ (19)
              |    |    |    \-100-+
              |    |    |          |                    /----- Candida_subhas~ (22)
              |    |    |          |              /-100-+
              |    |    |          |              |     \----- Scheffersomyce~ (25)
              |    |    |          \------100-----+
              |    |    |                         |     /----- Candida_albica~ (23)
              \-100+    |                         \-100-+
                   |    |                               \----- Candida_viswan~ (24)
                   |    |
                   |    \------------------------------------- Candida_railen~ (30)
                   |
                   |                              /----------- Purpureocilliu~ (33)
                   |                              |
                   \--------------61--------------+     /----- Gonapodya_sp. (34)
                                                  \--87-+
                                                        \----- Rhizopus_azygo~ (35)

   Root part of tree:

   /---------------------------------------------------------- Saccharomyces_c~ (1)
   |
   |---------------------------------------------------------- Saccharomyces_p~ (2)
   |
   |                                               /---------- Kazachstania_un~ (3)
   +         /-----------------100-----------------+
   |         |                                     \---------- Kazachstania_ex~ (4)
   |         |
   |         |                                     /---------- Torulaspora_del~ (5)
   \---100---+        /-------------100------------+
             |        |                            \---------- Zygotorulaspora~ (6)
             |        |
             \---100--+         /----------------------------- (61)
                      |         |
                      \---100---+         /------------------- Zygosaccharomyc~ (8)
                                |         |
                                \---100---+        /---------- Zygosaccharomyc~ (9)
                                          \---100--+
                                                   \---------- Zygosaccharomy~ (10)


   Phylogram (based on average branch lengths):

   /- Saccharomyces_c~ (1)
   |
   |- Saccharomyces_p~ (2)
   |
   |    /--- Kazachstania_un~ (3)
   |  /-+
   |  | \----- Kazachstania_ex~ (4)
   |  |
   +  |   /---- Torulaspora_del~ (5)
   |  | /-+
   |  | | \--- Zygotorulaspora~ (6)
   |  | |
   |  | |  /-------- Lachancea_ferme~ (7)
   |  | |  |
   |  | |  |         /-- Kluyveromyces_~ (11)
   |  | |  | /-------+
   \--+ |  | |       \-- Kluyveromyces_~ (12)
      | |  | |
      | |  | |             /-------- Brettanomyces_~ (13)
      | |  | |          /--+
      | |  | |          |  \----- Brettanomyces_~ (14)
      | |  | |        /-+
      | |  | |        | \------ Clavispora_lus~ (29)
      | |/-+ |        |
      | || | |        |   /----- Schizosaccharo~ (26)
      | || | |      /-+  /+
      | || | |      | |  |\--- Debaryomyces_f~ (27)
      \-+| | |      | |  |
        || | |      | \--+/------ Schizosaccharo~ (28)
        || | |      |    ||
        || | |      |    \+       /-- Schizosaccharo~ (31)
        || | |      |     \-------+
        || | |      |             \- Schizosaccharo~ (32)
        || | |      |
        || \-+      |        /-- Candida_margit~ (15)
        ||   |      |       /+
        ||   |     /+       |\-- Candida_paraps~ (18)
        ||   |     ||    /--+
        ||   |     ||    |  |/--- Candida_theae (16)
        ||   |     ||    |  \+
        ||   |     ||   /+   \-- Candida_metaps~ (17)
        ||   |     ||   ||
        ||   |     ||   ||  /--- Candida_jiufen~ (20)
        ||   |     ||  /+\--+
        ||   |     ||  ||   \---- Candida_pseudo~ (21)
        \+   |     ||  ||
         |   |   /-+|  |\----- Candida_oxycet~ (19)
         |   |   | |\--+
         |   |   | |   |  /--- Candida_subhas~ (22)
         |   |   | |   |/-+
         |   |   | |   || \------ Scheffersomyce~ (25)
         |   |   | |   \+
         |   |   | |    | /-- Candida_albica~ (23)
         |   \---+ |    \-+
         |       | |      \--- Candida_viswan~ (24)
         |       | |
         |       | \------ Candida_railen~ (30)
         |       |
         |       |/------------ Purpureocilliu~ (33)
         |       ||
         |       \+    /--------------------- Gonapodya_sp. (34)
         |        \----+
         |             \-------------------------------------- Rhizopus_azygo~ (35)
         |
         |     /----- Zygosaccharomyc~ (8)
         |     |
         \-----+   /-- Zygosaccharomyc~ (9)
               \---+
                   \--- Zygosaccharomy~ (10)

   |-----------| 0.500 expected changes per site

   Calculating tree probabilities...

   Credible sets of trees (257 trees sampled):
      50 % credible set contains 3 trees
      90 % credible set contains 35 trees
      95 % credible set contains 69 trees
      99 % credible set contains 182 trees


