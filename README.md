# DIAMOND-MEGAN
Diamond-Megan analysis: a practical case study
Journal Club
21.10.22
_____________________________

##  0- Login and data accessibility

    ls -lrth /media/D/util/DM/

## 1- Run Singularity
    singularity

## 2- Run the image with Singularity
    singularity shell /media/D/util/DM/DM.sif
    exit

## 3- Check the test dataset
    ls -lrth /media/D/util/DM/Test/

## 4- Create work folder and obtain the test dataset
    mkdir Jclub
    cd Jclub
    cp /media/D/util/DM/Test/* .
    ls -lrth

## 5- Map (or bind) the media drive and start with Fastq-Join
    export SINGULARITY_BINDPATH="/media/D/"
    singularity shell /media/D/util/DM/DM.sif
    fastq-join BIO9-13J_S7_L001_R1_001.fastq.gz BIO9-13J_S7_L001_R2_001.fastq.gz -o join_Bio_%.fastq
    ls -lrth

## 6- Merge the file and remove intermediates
    cat *.fastq > BIO_merged.fq
    rm *fastq
    ls -lrth

## 7- Run Diamond with nr database or other subset DBs
    time diamond blastx -q BIO_merged.fq -d /media/D/bank/nr/nr.dmnd -o D_nr_BIO.daa -f 100 -p 25
or  
    time diamond blastx -q BIO_merged.fq -d /media/D/bank/Diamond/Vref-gb.dmnd -o BIO_RG.daa -f 100 -p 5  
    exit

## 8- Link other DAA file to your folder
    ln -s /media/D/util/DM/DAA/* .
    ls -lrth

## 9- Run MEGAN and Start Meganization
    MEGAN
    /media/D/bank/nr/megan-map/megan-map-Feb2022.db

## 10- Optional: Meganization on command line
    daa-meganizer -i FILE.daa -t 50 -mdb /media/D/bank/nr/megan-map/megan-map-Feb2022.db
    
-----------------------------
Naser Poursalavati, 2022
