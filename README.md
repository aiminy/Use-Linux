# Use-Linux

## Search files with pattern

 grep -r pattern /path 2> /dev/null

 ack-grep pattern /path 2> /dev/null
 
 Example: ack-grep "bcl2fastq*" ~/ 2>/dev/null
 
Notes:
 
Normally you wouldn't want to actually search EVERYTHING on the system. Linux uses file nodes for everything, so some "files" are not things you would want to search. For example /dev/sda is the physical block device for your first hard drive. You probably want to search the mounted file systems not the raw disk device. Also there is /dev/random which spits out random data every time you read it. Searching that doesn't make a lot of sense. The /proc file system is also problematic in your case.
 
Don't search at root, only search the places that might be useful. Search /home or /usr or /etc separatly. The info you are looking for is likely of a specific type, so it's likely to be in a specific folder anyway. Configuration settings should be in /etc. Your personal data files should be in /home. Limiting search to a major area like this will greatly reduce your problems with recursive greps.
 
Exclude problematic areas using --exclude-dir and a set of things you know you don't needlike this:
grep -r --exclude-dir /proc --exclude-dir /dev --exclude-dir /tmp --exclude-dir /lost+found

-I to exclude binary
 
## List UUID

ls -l /dev/disk/by-uuid/

## Kill all background jobs 

kill -9 $(jobs -p)

## Run job interactively on pegasus

bsub -P bbc -Is -q interactive bash
  
## Find Select_DE_gene_basd_on_Feature in R code
 
ack-grep Select_DE_gene_basd_on_Feature ~/GOSJ/R/*.R
 
## Find the file with .tiff extension
 
find /media/H_driver/ -name  "*.tiff" 2>/dev/null
 
## Find empty directory and delete them
  
find /media/H_driver/PJ/Results -depth -type d -empty -delete

## Find empty directory

find /media/H_driver/PJ/Results -depth -type d -empty

## Setup path for R installation(add the following settings to $HOME/.bashrc, then source $HOME/.bashrc) 

 export PATH=$HOME/packages/bin:$PATH

 export LD_LIBRARY_PATH=$HOME/packages/lib:$LD_LIBRARY_PATH 

 export CFLAGS="-I$HOME/packages/include" 

 export LDFLAGS="-L$HOME/packages/lib"

 export CPLUS_INCLUDE_PATH="$CPLUS_INCLUDE_PATH:$HOME/packages/include"
 
## Check hard disk partitions and disk space on Linux
 
 df -h | grep ^/dev

## Check size of directory
 
 du -h | sort -rh | head
 
## Check size of all files
 
 du -ha | sort -h

## Pip install to certain directory

 pip install --install-option="--prefix=$HOME/3UTR-Seq/inst/RSeQC" RSeQC
 
## Update pysam module
 
 pip install --upgrade --user pysam

## Get disk usage information

sudo apt-get install di

di

## Mount ssh driver to your local Macs

1. brew install ssh-copy-id

2. ssh-copy-id -i .ssh/id_rsa.pub axy148@pegasus.ccs.miami.edu

3. download the latest version of FUSE for OS X at the FUSE for OS X web site

4. install FUSE for OS X on my laptop by double-clicking the disk image, then double-clicking on the installation package. There is pretty standard Mac OS X stuff; it went without a hitch.

5. download the latest version of SSHFS for OS X at the FUSE for OS X web site.

6. install SSHFS by double-clicking on the downloaded file. if you ran into an issue here where Mac OS X refused to install the package because SSHFS comes from an “unidentified developer.” To get around this, you need to override the Gatekeeper in Mac OS X, which can be as simple as right-clicking on the package and selecting “Open” from the context menu.

7. Both FUSE for OS X and SSFHS were now installed.

8. mkdir ~/pegasus

9. Type the following commands
```{bash}
sshfs -p 22 axy148@pegasus.ccs.miami.edu:/scratch/projects/bbc ~/pegasus -oauto_cache,reconnect,defer_permissions,noappledouble,negative_vncache,volname=pegasus

To mount another directory 

mkdir ~/MyHomeAtPegasus

sshfs -p 22 axy148@pegasus.ccs.miami.edu:/nethome/axy148 ~/MyHomeAtPegasus -oreconnect,defer_permissions,noappledouble,volname=MyHomeAtPegasus

```

10. if you want Unmounting, type "umount ~/pegasus"

## Mount ssh driver to your local linux machine

1. Type the following commands
```{bash}
ssh-copy-id -i .ssh/id_rsa.pub axy148@pegasus.ccs.miami.edu
mkdir /media/pegasus
sshfs axy148@pegasus.ccs.miami.edu:/scratch/projects/bbc /media/pegasus
```

## Make a soft link for "Dropbox (BBSR)"
```{bash}
ln -s "Dropbox (BBSR)" Dropbox
```
## Back up the files in pegasus Bropbox
```{bash}
# Show example
cd Dropbox
ln -s ~/MyHomeAtPegasus/Danny_chip3/sample_infor_Danny_chip3.txt
highligth sample_infor_Danny_chip3.txt file, right click, then select "Smart Sync" then select "Online Only"
After finish sync, you can 
umount ~/MyHomeAtPegasus
```

