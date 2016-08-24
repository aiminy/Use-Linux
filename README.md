# Use-Linux

 * search file with pattern

 grep -r pattern /path 2> /dev/null

 ack-grep pattern /path 2> /dev/null
 
 Example: ack-grep "bcl2fastq*" ~/ 2>/dev/null
 
 * list UUID

 ls -l /dev/disk/by-uuid/

 * Kill all background jobs 

  kill -9 $(jobs -p)

 * Run job interactively on pegasus

  bsub -P bbc -Is -q interactive bash
  
 * Find Select_DE_gene_basd_on_Feature in R code
 
 ack-grep Select_DE_gene_basd_on_Feature ~/GOSJ/R/*.R
 
 * Find the file with .tiff extension
 
 find /media/H_driver/ -name  "*.tiff" 2>/dev/null
 
 * find empty directory and delete them
  
 find /media/H_driver/PJ/Results -depth -type d -empty -delete

 * find empty directory

 find /media/H_driver/PJ/Results -depth -type d -empty

 * Setup path for R installation(add the following settings to $HOME/.bashrc, then source $HOME/.bashrc) 

 export PATH=$HOME/packages/bin:$PATH

 export LD_LIBRARY_PATH=$HOME/packages/lib:$LD_LIBRARY_PATH 

 export CFLAGS="-I$HOME/packages/include" 

 export LDFLAGS="-L$HOME/packages/lib"

 export CPLUS_INCLUDE_PATH="$CPLUS_INCLUDE_PATH:$HOME/packages/include"
