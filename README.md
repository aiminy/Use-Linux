# linux,git,dropbox 101

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

## Find the file with *.bai extension and delete with asking for permission 
```{bash}
find  /scratch/projects/bbc/Project/DI/Output_rMATS_filtered -type f -name "*.bai" -exec rm -i {} \;
```
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
```{bash}

 du -h | sort -rh | head
 
 du -h /media/H_driver/Aimin_project/ | sort -rh | head
  
 or
 
 du -sh ~/pegasus/aiminy_project
``` 
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

mkdir ~/pegasus2
sshfs -p 22 axy148@pegasus.ccs.miami.edu:/projects2/med/bbc ~/pegasus2 -oauto_cache,reconnect,defer_permissions,noappledouble,negative_vncache,volname=pegasus2

mkdir HomeAtCluster
sshfs -p 22 ay64w@ghpcc06.umassrc.org:/home/ay64w HomeAtCluster -oauto_cache,reconnect,defer_permissions,noappledouble,negative_vncache,volname=HomeAtCluster

mkdir ProjectAtCluster
sshfs -p 22 ay64w@ghpcc06.umassrc.org:/project ProjectAtCluster -oauto_cache,reconnect,defer_permissions,noappledouble,negative_vncache,volname=ProjectAtCluster
```

10. if you want Unmounting, type "umount ~/pegasus"

## Mount ssh driver to your local linux machine

1. Type the following commands
```{bash}
ssh-copy-id -i .ssh/id_rsa.pub axy148@pegasus.ccs.miami.edu
mkdir /media/pegasus
sshfs axy148@pegasus.ccs.miami.edu:/scratch/projects/bbc /media/pegasus
```
2. If you have an erro like the following:
```{bash}
sshfs axy148@pegasus.ccs.miami.edu:/scratch/projects/bbc /media/pegasus
fuse: mountpoint is not empty
fuse: if you are sure this is safe, use the 'nonempty' mount option
```

try this:
```{bash}
aiminyan@aiminyan-Precision-Tower-5810:~$ sshfs axy148@pegasus.ccs.miami.edu:/scratch/projects/bbc /media/pegasus -o nonempty
```

## Make a soft link for "Dropbox (BBSR)"
```{bash}
ln -s "Dropbox (BBSR)" Dropbox
```
## Back up the files in pegasus to Dropbox
```{bash}
# Show example
cd Dropbox
ln -s ~/MyHomeAtPegasus/Danny_chip3/sample_infor_Danny_chip3.txt
highligth sample_infor_Danny_chip3.txt file, right click, then select "Smart Sync" then select "Online Only"
After finish sync, you can 
umount ~/MyHomeAtPegasus
```

## Kill all processes that their name includes "download"
```bash
ps aux | grep -ie download | awk '{print $2}' | xargs kill -9
```

## To mount H drive, edit your /etc/fstab file 
### note : make a smbcredentials file with your usr name and passpord included in

```
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/sda3 during installation
UUID=fb33babc-a08c-4387-bf77-72bc46ccc66b /               ext4    errors=remount-ro 0       1
//scccresfs.cgcent.miami.edu/Bioinformatics /media/H_driver cifs iocharset=utf8,credentials=/home/aiminyan/.smbcredentials,uid=1000,user 0 0
//sccceqfs.cgcent.miami.edu/BBSR$ /media/bbc_driver cifs iocharset=utf8,credentials=/home/aiminyan/.smbcredentials,uid=1000,user 0 0
//umeqstor-nas.cgcent.miami.edu/LOCKHART /media/Lockhart cifs iocharset=utf8,credentials=/home/aiminyan/.smbcredentials,uid=1000,user 0
/swapfile none swap sw 0 0
```

## set docker
```
sudo apt install docker.io

sudo usermod -aG docker $USER

```
 ## To deal with "system() call from RStudio does not find path"
```
system("echo $PATH") on rstudio Console, copy

emacs .Renviron
add
 
PATH = usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/usr/lib/jvm/java-8-oracle/bin:/usr/lib/jvm/java-8-oracle/db/bin:/usr/lib/jvm/java-8-oracle/jre/bin:/home/aiminyan/miniconda3/bin

restart rstudio,
then it should work
 ```

## To install Oracle Java from conda
```
conda install -c cyclus java-jdk
```

## To install openjdk from conda
```
conda install -c anaconda openjdk 
```

## To Install gatk4 on pegasus

```
module unload python/2.7.3
conda install -c bioconda gatk4 
gatk-launch
```

## Use tar to create a *.tar.gz file
```
tar -pczvf /root/etc.tar.gz /etc
```
## to mount , add the following line to /etc/fstab
```
//scccresfs.cgcent.miami.edu/bioinformatics_2 /media/H_driver2 cifs iocharset=utf8,credentials=/home/aiminyan/.smbcredentials,uid=1000,user 0 0
```

## check cpu and memory of your linux system
```
sudo lshw -short -C cpu
sudo lshw -short -C memory
```
