# Use-Linux

 * search files with pattern

 grep -r pattern /path 2> /dev/null

 ack-grep pattern /path 2> /dev/null
 
 Example: ack-grep "bcl2fastq*" ~/ 2>/dev/null
 
 Notes:
 
 Normally you wouldn't want to actually search EVERYTHING on the system. Linux uses file nodes for everything, so some "files" are not things you would want to search. For example /dev/sda is the physical block device for your first hard drive. You probably want to search the mounted file systems not the raw disk device. Also there is /dev/random which spits out random data every time you read it. Searching that doesn't make a lot of sense. The /proc file system is also problematic in your case.
 
 Don't search at root, only search the places that might be useful. Search /home or /usr or /etc separatly. The info you are looking for is likely of a specific type, so it's likely to be in a specific folder anyway. Configuration settings should be in /etc. Your personal data files should be in /home. Limiting search to a major area like this will greatly reduce your problems with recursive greps.
 
 Exclude problematic areas using --exclude-dir and a set of things you know you don't needlike this:
 grep -r --exclude-dir /proc --exclude-dir /dev --exclude-dir /tmp --exclude-dir /lost+found
 
 -I to exclude binary
 
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
 
 
 # Check size of directory
 
 du -h | sort -rh | head
 
