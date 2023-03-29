Copied 20 fasta files from NCBI of GAL10 genes from separate yeast species
Decided Busco would be best for QC

Downloaded miniconda for busco installation
miniconda was unable to solve environment
uninstalled miniconda

Installed Anaconda via browser
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

Attempted to run >conda install -c bioconda busco< was given this error:
Solving environment: failed with initial frozen solve. Retrying with flexible solve.
Solving environment: -
Found conflicts! Looking for incompatible packages.
This can take several minutes.  Press CTRL-C to abort.
failed

UnsatisfiableError: The following specifications were found to be incompatible with each other:

Output in format: Requested package -> Available versions 

Attempted to type >conda info< to understand my conda package and was blessed with this error:
>>> conda info
  File "<stdin>", line 1
    conda info
          ^
SyntaxError: invalid syntax
  
  Used >quit()< to exit the interactive pyhton shell
  Now able to type in the anaconda prompt wihtout syntax errors
                  Retried >conda install -c "bioconda/label/cf201901" busco< and was given the same error
Ran >conda create -n BUSCO -c bioconda -c conda-forge busco=5.4.5 python=3.9.13 conda activate BUSCO< and was given this same error:
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
    
Ran >conda install -c conda-forge -c bioconda busco=5.4.4< and got this error:
Collecting package metadata (current_repodata.json): failed

CondaHTTPError: HTTP 000 CONNECTION FAILED for url <https://conda.anaconda.org/conda-forge/win-64/current_repodata.json>
Elapsed: -

An HTTP error occurred when trying to retrieve this URL.
HTTP errors are often intermittent, and a simple retry will get you on your way.
'https//conda.anaconda.org/conda-forge/win-64'
    
Forgot to turn the WI-FI on
Ran >conda install -c conda-forge -c bioconda busco=5.4.4< again
It was unable to understand the environment
    
I then attmpted this command >conda create -p /vol/bigdata/BUSCO< which gave me this:
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 22.9.0
  latest version: 23.1.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: C:\vol\bigdata\BUSCO



Proceed ([y]/n)?
To which I responded n and then proceeded to run this >conda update -n base -c defaults conda< which successfully updated conda
    
Then I attempted this command again >conda create -p /vol/bigdata/BUSCO< which gave me the same option as above but without the notification to update
Next I ran this >conda activate C:\vol\bigdata\BUSCO< which activated the busco specific environment
    I then ran this >conda install -p /vol/bigdata/BUSCO -c conda-forge -c bioconda busco=5.4.5< which gave me this error
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
    through this I was able to easily install clustalo using
    
sudo apt install clustalo
    
    and similarly for muscle I used
    
sudo apt install muscle
    I then added 20 sequences to my GAL10 data because I thought it would be cool to make a larger tree.
    then to align my data I used
>clustalo --in gal10dntp.fasta --out gal10dntp.align --force --outfmt clustal --wrap 80
    
    
In class we looked to create distance-based and parsimony-based trees for our data. Here are the commands I used for the parsimony tree in RStudio.
    
library(ape)
library(phangorn)
library(adegenet)
dna <- fasta2DNAbin(file="gal10aaaling.fasta")
dna2 <- as.phyDat(dna)
tre.ini <- nj(dist.dna(dna,model="raw"))
parsimony(tre.ini, dna2)
    
   I am unsure why, but once the parsiomny command is used, it gives those using AA sequences an error that crashes R. 
Here are the commands I used for the distance based tree. 
    
library(ape)
library(adegenet)
library(phangorn)
dna <- fasta2DNAbin(file="gal10aaaling.fasta")
D <- dist.dna(dna, model="TN93")
tre <- nj(D)
tre <- ladderize(tre)
plot(tre, cex=.6)
title("A simple NJ tree")

    This tree worked, but I think because we tried to convert Amino acids back into nucleotides the tree is trash. Everything is on the same line.
    
Now, we want to make trees from our alignments. 
I made a tree earlier, which will be in the data file, but the tips are all mislabeled and hard to understand so I redid the alignments as such.
    
Sudo apt install mafft
    
>mafft -h 
>mafft 
    which automatically asks
Input file? (FASTA format; Folder=/mnt/c/users/quaid)
>Gal10_AA.fasta 
Output file?
>Gal10AA.fasta
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
>3
Additional arguments? (--ep # --op # --kappa # etc)
>
command=
"/usr/bin/mafft"  --retree 2 --reorder "gal10_AA.fasta" > "gal10AA2.fasta"
Type Y or just enter to run this command.
>Y
    


