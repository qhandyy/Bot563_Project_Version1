Copied 20 fasta files from NCBI of GAL10 genes from separate yeast species
Decided Busco would be best for QC

Downloaded miniconda for busco installation
miniconda was unable to solve environment
uninstalled miniconda

Installed Anaconda via browser
  Attmpted to run >conda install -c "bioconda/label/cf201901" busco< in the interface, but was given this error:
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
