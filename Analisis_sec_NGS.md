### Análisis de lecturas NGS
___

#### Control de calidad

Si bien las muestras se reciben *post* con el control de  calidad inicial realizado, se realiza una "corroboración" utilizando fastqc con los siguientes comandos: 

```
$ fastqc S10_R1_filter.fastq.gz -o .
Started analysis of S10_R1_filter.fastq.gz
Approx 5% complete for S10_R1_filter.fastq.gz
Approx 10% complete for S10_R1_filter.fastq.gz
Approx 15% complete for S10_R1_filter.fastq.gz
Approx 20% complete for S10_R1_filter.fastq.gz
Approx 25% complete for S10_R1_filter.fastq.gz
Approx 30% complete for S10_R1_filter.fastq.gz
Approx 35% complete for S10_R1_filter.fastq.gz
Approx 40% complete for S10_R1_filter.fastq.gz
Approx 45% complete for S10_R1_filter.fastq.gz
Approx 50% complete for S10_R1_filter.fastq.gz
Approx 55% complete for S10_R1_filter.fastq.gz
Approx 60% complete for S10_R1_filter.fastq.gz
Approx 65% complete for S10_R1_filter.fastq.gz
Approx 70% complete for S10_R1_filter.fastq.gz
Approx 75% complete for S10_R1_filter.fastq.gz
Approx 80% complete for S10_R1_filter.fastq.gz
Approx 85% complete for S10_R1_filter.fastq.gz
Approx 90% complete for S10_R1_filter.fastq.gz
Approx 95% complete for S10_R1_filter.fastq.gz
Analysis complete for S10_R1_filter.fastq.gz

$ fastqc S10_R2_filter.fastq.gz -o .
Started analysis of S10_R2_filter.fastq.gz
Approx 5% complete for S10_R2_filter.fastq.gz
Approx 10% complete for S10_R2_filter.fastq.gz
Approx 15% complete for S10_R2_filter.fastq.gz
Approx 20% complete for S10_R2_filter.fastq.gz
Approx 25% complete for S10_R2_filter.fastq.gz
Approx 30% complete for S10_R2_filter.fastq.gz
Approx 35% complete for S10_R2_filter.fastq.gz
Approx 40% complete for S10_R2_filter.fastq.gz
Approx 45% complete for S10_R2_filter.fastq.gz
Approx 50% complete for S10_R2_filter.fastq.gz
Approx 55% complete for S10_R2_filter.fastq.gz
Approx 60% complete for S10_R2_filter.fastq.gz
Approx 65% complete for S10_R2_filter.fastq.gz
Approx 70% complete for S10_R2_filter.fastq.gz
Approx 75% complete for S10_R2_filter.fastq.gz
Approx 80% complete for S10_R2_filter.fastq.gz
Approx 85% complete for S10_R2_filter.fastq.gz
Approx 90% complete for S10_R2_filter.fastq.gz
Approx 95% complete for S10_R2_filter.fastq.gz
Analysis complete for S10_R2_filter.fastq.gz
```
 El argumento `-o` indica que el directorio a continuación es el lugar de destino de los archivos de output de fastqc, mientras que `.` indica que el directorio es el mismo que en el que estamos trabajando.
 
 Los resultados de fastqc para la muestra S10_R1 fue:
 
 ![](/Users/camilo/Desktop/Pasantia_profesor_Verdugo/analisis_secuencias/S10_R1.png)
 
 Mostrando que practicamente todas las posiciones poseen un phred score mayor a 28 (a excepción de la última, pero aún así esta es >24), lo que indica lecturas de buena calidad.
 
 Por otro lado, los resultados para S10_R2 fueron:
 
  ![](/Users/camilo/Desktop/Pasantia_profesor_Verdugo/analisis_secuencias/S10_R2.png)
  
  Que si bien podrían considerarse de una calidad ligeramente inferior al read 1, siguen siendo de buena calidad (phred score >30 en practicamente todas las lecturas).
  
  Adicionalmente, no se observa contenido de adaptadores en ninguno de los read (gráficos no mostrados).
  
### Alineamiento de lecturas

Las secuencias se alinean contra el genoma de referencia, en este caso el hg19, con el software bwa, obteniendo un archivo sam.

```
$ bwa mem hg19_reference.fa S10_R1_filter.fastq.gz S10_R2_filter.fastq.gz > S10.sam
[M::bwa_idx_load_from_disk] read 0 ALT contigs
[M::process] read 44908 sequences (10000438 bp)...
[M::process] read 17162 sequences (3815080 bp)...
[M::mem_pestat] # candidate unique pairs for (FF, FR, RF, RR): (0, 21912, 0, 0)
[M::mem_pestat] skip orientation FF as there are not enough pairs
[M::mem_pestat] analyzing insert size distribution for orientation FR...
[M::mem_pestat] (25, 50, 75) percentile: (230, 246, 265)
[M::mem_pestat] low and high boundaries for computing mean and std.dev: (160, 335)
[M::mem_pestat] mean and std.dev: (247.10, 17.39)
[M::mem_pestat] low and high boundaries for proper pairs: (125, 370)
[M::mem_pestat] skip orientation RF as there are not enough pairs
[M::mem_pestat] skip orientation RR as there are not enough pairs
[M::mem_process_seqs] Processed 44908 reads in 7.637 CPU sec, 7.940 real sec
[M::mem_pestat] # candidate unique pairs for (FF, FR, RF, RR): (0, 8408, 0, 0)
[M::mem_pestat] skip orientation FF as there are not enough pairs
[M::mem_pestat] analyzing insert size distribution for orientation FR...
[M::mem_pestat] (25, 50, 75) percentile: (230, 246, 265)
[M::mem_pestat] low and high boundaries for computing mean and std.dev: (160, 335)
[M::mem_pestat] mean and std.dev: (247.18, 17.30)
[M::mem_pestat] low and high boundaries for proper pairs: (125, 370)
[M::mem_pestat] skip orientation RF as there are not enough pairs
[M::mem_pestat] skip orientation RR as there are not enough pairs
[M::mem_process_seqs] Processed 17162 reads in 2.270 CPU sec, 2.241 real sec
[main] Version: 0.7.17-r1188
[main] CMD: bwa mem hg19_reference.fa S10_R1_filter.fastq.gz S10_R2_filter.fastq.gz
[main] Real time: 12.589 sec; CPU: 11.831 sec
```
Luego el archivo es convertido de formato bam a sam para que sea compatible con el software GATK.

```
$ java -jar picard.jar SamFormatConverter I=S10.sam O=S10.bam
INFO	2022-07-13 21:02:02	SamFormatConverter	

********** NOTE: Picard's command line syntax is changing.
**********
********** For more information, please see:
********** 
https://github.com/broadinstitute/picard/wiki/Command-Line-Syntax-Transition-For-Users-(Pre-Transition)
**********
********** The command line looks like this in the new syntax:
**********
**********    SamFormatConverter -I S10.sam -O S10.bam
**********


21:02:04.159 INFO  NativeLibraryLoader - Loading libgkl_compression.dylib from jar:file:/Users/camilo/Desktop/Pasantia_profesor_Verdugo/analisis_secuencias/picard.jar!/com/intel/gkl/native/libgkl_compression.dylib
[Wed Jul 13 21:02:04 CLT 2022] SamFormatConverter INPUT=S10.sam OUTPUT=S10.bam    VERBOSITY=INFO QUIET=false VALIDATION_STRINGENCY=STRICT COMPRESSION_LEVEL=5 MAX_RECORDS_IN_RAM=500000 CREATE_INDEX=false CREATE_MD5_FILE=false GA4GH_CLIENT_SECRETS=client_secrets.json USE_JDK_DEFLATER=false USE_JDK_INFLATER=false
[Wed Jul 13 21:02:04 CLT 2022] Executing as camilo@MacBook-Pro-de-Camilo.local on Mac OS X 10.16 x86_64; OpenJDK 64-Bit Server VM 1.8.0_332-b09; Deflater: Intel; Inflater: Intel; Provider GCS is not available; Picard version: 2.27.4-SNAPSHOT
INFO	2022-07-13 21:02:04	SamFormatConverter	Seen many non-increasing record positions. Printing Read-names as well.
[Wed Jul 13 21:02:06 CLT 2022] picard.sam.SamFormatConverter done. Elapsed time: 0,03 minutes.
Runtime.totalMemory()=458752000
```
Luego, es necesario que las lecturas en el archivo bam sean ordenadas por posición de acuerdo con el genoma de referencia:

```
$ java -jar picard.jar SortSam I=S10.bam O=S10_sorted.bam SO=coordinate
INFO	2022-07-13 21:04:22	SortSam	

********** NOTE: Picard's command line syntax is changing.
**********
********** For more information, please see:
********** 
https://github.com/broadinstitute/picard/wiki/Command-Line-Syntax-Transition-For-Users-(Pre-Transition)
**********
********** The command line looks like this in the new syntax:
**********
**********    SortSam -I S10.bam -O S10_sorted.bam -SO coordinate
**********


21:04:23.477 INFO  NativeLibraryLoader - Loading libgkl_compression.dylib from jar:file:/Users/camilo/Desktop/Pasantia_profesor_Verdugo/analisis_secuencias/picard.jar!/com/intel/gkl/native/libgkl_compression.dylib
[Wed Jul 13 21:04:23 CLT 2022] SortSam INPUT=S10.bam OUTPUT=S10_sorted.bam SORT_ORDER=coordinate    VERBOSITY=INFO QUIET=false VALIDATION_STRINGENCY=STRICT COMPRESSION_LEVEL=5 MAX_RECORDS_IN_RAM=500000 CREATE_INDEX=false CREATE_MD5_FILE=false GA4GH_CLIENT_SECRETS=client_secrets.json USE_JDK_DEFLATER=false USE_JDK_INFLATER=false
[Wed Jul 13 21:04:23 CLT 2022] Executing as camilo@MacBook-Pro-de-Camilo.local on Mac OS X 10.16 x86_64; OpenJDK 64-Bit Server VM 1.8.0_332-b09; Deflater: Intel; Inflater: Intel; Provider GCS is not available; Picard version: 2.27.4-SNAPSHOT
INFO	2022-07-13 21:04:24	SortSam	Seen many non-increasing record positions. Printing Read-names as well.
INFO	2022-07-13 21:04:24	SortSam	Finished reading inputs, merging and writing to output now.
[Wed Jul 13 21:04:25 CLT 2022] picard.sam.SortSam done. Elapsed time: 0,03 minutes.
Runtime.totalMemory()=324534272
```
Posteriormente, es necesario añadir el campo ReadGroup al archivo bam:

```
$ java -jar picard.jar AddOrReplaceReadGroups I=S10_sorted.bam O=S10_sorted_RG.bam ID=sample LB=Paired-end PL=Illumina PU=Unknown SM=sample
INFO	2022-07-13 21:07:58	AddOrReplaceReadGroups	

********** NOTE: Picard's command line syntax is changing.
**********
********** For more information, please see:
********** 
https://github.com/broadinstitute/picard/wiki/Command-Line-Syntax-Transition-For-Users-(Pre-Transition)
**********
********** The command line looks like this in the new syntax:
**********
**********    AddOrReplaceReadGroups -I S10_sorted.bam -O S10_sorted_RG.bam -ID sample -LB Paired-end -PL Illumina -PU Unknown -SM sample
**********


21:07:59.107 INFO  NativeLibraryLoader - Loading libgkl_compression.dylib from jar:file:/Users/camilo/Desktop/Pasantia_profesor_Verdugo/analisis_secuencias/picard.jar!/com/intel/gkl/native/libgkl_compression.dylib
[Wed Jul 13 21:07:59 CLT 2022] AddOrReplaceReadGroups INPUT=S10_sorted.bam OUTPUT=S10_sorted_RG.bam RGID=sample RGLB=Paired-end RGPL=Illumina RGPU=Unknown RGSM=sample    VERBOSITY=INFO QUIET=false VALIDATION_STRINGENCY=STRICT COMPRESSION_LEVEL=5 MAX_RECORDS_IN_RAM=500000 CREATE_INDEX=false CREATE_MD5_FILE=false GA4GH_CLIENT_SECRETS=client_secrets.json USE_JDK_DEFLATER=false USE_JDK_INFLATER=false
[Wed Jul 13 21:07:59 CLT 2022] Executing as camilo@MacBook-Pro-de-Camilo.local on Mac OS X 10.16 x86_64; OpenJDK 64-Bit Server VM 1.8.0_332-b09; Deflater: Intel; Inflater: Intel; Provider GCS is not available; Picard version: 2.27.4-SNAPSHOT
INFO	2022-07-13 21:07:59	AddOrReplaceReadGroups	Created read-group ID=sample PL=Illumina LB=Paired-end SM=sample

[Wed Jul 13 21:08:00 CLT 2022] picard.sam.AddOrReplaceReadGroups done. Elapsed time: 0,03 minutes.
Runtime.totalMemory()=324534272
``` 
Indexar alineamiento

```
$ samtools index S10_sorted_RG.bam
```

Posteriormente, es posible realizar un análisis de calidad mediante el software Qualimap, mediante el siguiente comando:

```
$ qualimap bamqc -bam S10_sorted_RG.bam -gff regiones_blanco.bed -outdir ./S10_sorted_RG
Command line run, unsetting DISPLAY variable...
Display: 
Java memory size is set to 1200M
Launching application...

QualiMap v.2.2.2-dev
Built on 2016-12-11 14:41

Selected tool: bamqc
Available memory (Mb): 33
Max memory (Mb): 1258
Starting bam qc....
Loading sam header...
Loading locator...
Loading reference...
Number of windows: 400, effective number of windows: 492
Chunk of reads size: 1000
Number of threads: 8
Initializing regions from regiones_blanco.bed.....
Found 369 regions
Filling region references... 
Processed 50 out of 492 windows...
Processed 100 out of 492 windows...
Processed 150 out of 492 windows...
Processed 200 out of 492 windows...
Processed 250 out of 492 windows...
Processed 300 out of 492 windows...
Processed 350 out of 492 windows...
Processed 400 out of 492 windows...
Processed 450 out of 492 windows...
Total processed windows:492
Number of reads: 62077
Number of valid reads: 62031
Number of correct strand reads:0

Inside of regions...
Num mapped reads: 60258
Num mapped first of pair: 30248
Num mapped second of pair: 30010
Num singletons: 44
Time taken to analyze reads: 6
Computing descriptors...
numberOfMappedBases: 8903968
referenceSize: 3137161264
numberOfSequencedBases: 8899841
numberOfAs: 2379499
Computing per chromosome statistics...
Computing histograms...
Overall analysis time: 6
end of bam qc
Computing report...
Writing HTML report...
HTML report created successfully

Finished

$ ls
S10.bam                   S10_R2_filter_fastqc.html hg19_reference.fa.ann
S10.sam                   S10_R2_filter_fastqc.zip  hg19_reference.fa.bwt
S10_R1.png                S10_sorted.bam            hg19_reference.fa.pac
S10_R1_filter.fastq.gz    S10_sorted_RG             hg19_reference.fa.sa
S10_R1_filter_fastqc.html S10_sorted_RG.bam         picard.jar
S10_R1_filter_fastqc.zip  S10_sorted_RG.bam.bai     qualimap
S10_R2.png                hg19_reference.fa         qualimap_v2.2.1
S10_R2_filter.fastq.gz    hg19_reference.fa.amb     regiones_blanco.bed
```

El archivo "regiones_blanco.bed" corresponde a un archivo que indica cuales fueron las regiones blanco de secuenciación (panel dirigido).

El análisis con Qualimap muestra que la profundidad de cobertura de la corrida fue de 97,7169 (alineamientos "uno sobre otro"). 

Por otro lado, la amplitud de la cobertura para las distintas regiones fue como se indica en el gráfico a continuación:

 ![](/Users/camilo/Desktop/Pasantia_profesor_Verdugo/analisis_secuencias/genome_coverage_quotes.png)
 
### Procesamiento del alineamiento usando GATK



 