###Desarrollo ejercicios unidades 1 y 2
Aquí se desarrollan las actividades descritas en las unidades 1 y 2 del curso alojado en [el repositorio del curso de bioinformática](https://github.com/u-genoma/BioinfinvRepro/) en el contexto de la tercera pasantía del curso de "Técnicas y Metodologías en Genética" de la escuela de postgrado de la Facultad de Medicina de la Universidad de Chile.

###Unidad 1
___
####Introducción a la línea de comandos y la terminal
Los primeros comandos son `date` y `echo`, los cuales tienen los siguientes outputs en la terminal:

```
$ date
Thu Jul  7 20:43:34 -04 2022
```

```
$ echo algo
algo

```
Los comandos `R`
y `quit()`permiten iniciar el software R en la terminal y cerrarlo respectivamente.

```
$ R

R version 4.1.3 (2022-03-10) -- "One Push-Up"
Copyright (C) 2022 The R Foundation for Statistical Computing
Platform: x86_64-apple-darwin17.0 (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.

> quit()
```
####Navegación y manejo básico de archivos y datos
El comando `pwd` entrega la ubicación del directorio actual.
Con el comando `cd` podemos cambiar de directorio. El comando `cd` más el nombre de un subdirectorio del directorio en que nos encontramos nos permite movernos a ese directorio, mientras ese comando más la ruta de un directorio (aunque no sea un subdirectorio inmediato del directorio en que nos encontramos) nos permite movernos a ese directorio. Ejemplo:

```
$ pwd
/Users/camilo
$ cd Desktop 
$ pwd
/Users/camilo/Desktop
$ cd /Users/camilo/Desktop/"Documentos fase 2 microbioma"/"Documentos traducidos"
$ pwd
/Users/camilo/Desktop/Documentos fase 2 microbioma/Documentos traducidos
```
El comando `cd ..` permite moverse al directorio que esté encima del cual nos encontramos.

El comando `ls` enlista los documentos presentes en el directorio en que nos encontramos. El comando `ls` con el argumento -l (`ls -l`) enlista los mismos archivos pero entregando información sobre los permisos de edición y lectura, fecha de modificación, etc.

```
$ ls -l
total 15880
-rw-r--r--@ 1 camilo  staff    37K Jun 13 20:38 10) consentimiento_final.doc
-rw-r--r--@ 1 camilo  staff    24K Jun 13 21:51 11) Lista de verificacio??n de participantes CRC_final.docx
-rw-r--r--@ 1 camilo  staff    24K Jun 13 21:51 12) Lista de verificacio??n voluntarios sanos_final.docx
-rw-r--r--@ 1 camilo  staff   7.5M Jun 14 12:27 4) Recoleccio??n de muestras pacientes_final .docx
-rw-r--r--@ 1 camilo  staff    29K Jun 13 20:33 5) Hoja de informacio??n al participante_final.docx
-rw-r--r--@ 1 camilo  staff    29K Jun 12 19:02 6) Cuestionario_final.docx
-rw-r--r--@ 1 camilo  staff    14K Jun 10 21:41 7) excel_questionnaire_responses_final.updated.xlsx
-rw-r--r--@ 1 camilo  staff   108K Jun 12 19:30 Cuestionario heces.docx
-rw-r--r--@ 1 camilo  staff    25K Jun 14 12:23 Protocolo de estudio.docx
```
El comando `man` muestra el manual de cualquier comando, para salir de esa ventana se debe presionar "q".

`mkdir` crea un directorio

`cp` copia un archivo

`mv` Mueve un archivo de un directorio a otro

`rm` Elimina un archivo o directorios

###Comando `tar`
El comando `tar` permite realizar compresión de archivos.

```
$ tar cvzf Maiz.tar.gz Maiz
a Maiz
a Maiz/nuevos_final.log
a Maiz/nuevos_final.bim
a Maiz/nuevos_final.bed
a Maiz/nuevos_final.fam
$ ls -lhS
total 2552
-rw-r--r--  1 camilo  staff   1.2M Jul  7 21:46 Maiz.tar.gz
-rw-r--r--@ 1 camilo  staff   1.2K Jan 17  2020 example_script_runadmixture.sh
-rw-r--r--@ 1 camilo  staff   370B Jan 17  2020 getsecsNCBI.sh
drwxr-xr-x@ 6 camilo  staff   192B Jan 17  2020 Maiz
drwxr-xr-x@ 6 camilo  staff   192B Jan 17  2020 Tomates
drwxr-xr-x@ 3 camilo  staff    96B Jan 17  2020 Manzanas
drwxr-xr-x@ 3 camilo  staff    96B Jan 17  2020 Peras
```
los argumentos `cvzf` permiten crear un nuevo archivo .tar, mostrar el progreso de la compresión, indicar que se quiere un archivo `.gzip` y cual es el nombre del archivo que se quiere como resultado, respectivamente.

Para extraer un archivo se deben agregar los argumentos `-xvf`, los cuales dan la instrucción de extraer los datos, mostrar el progreso e indicar el archivo desde el cual quieren ser extraídos los datos respectivamente.

```
$ ls
Maiz.tar.gz                    Tomates
Manzanas                       example_script_runadmixture.sh
Peras                          getsecsNCBI.s

$ tar -xvf Maiz.tar.gz
x Maiz/
x Maiz/nuevos_final.log
x Maiz/nuevos_final.bim
x Maiz/nuevos_final.bed
x Maiz/nuevos_final.fam

$ ls
Maiz                           Tomates
Maiz.tar.gz                    example_script_runadmixture.sh
Manzanas                       getsecsNCBI.sh
Peras
```
Para visualizar el contenido de un archivo tar sin descomprimirlo se debe reemplazar `x` por `t` en el argumento anterior.

```
$ tar -tvf Maiz.tar.gz
drwxr-xr-x  0 camilo staff       0 Jan 17  2020 Maiz/
-rw-r--r--  0 camilo staff    1825 Jan 17  2020 Maiz/nuevos_final.log
-rw-r--r--  0 camilo staff 1109078 Jan 17  2020 Maiz/nuevos_final.bim
-rw-r--r--  0 camilo staff 1551105 Jan 17  2020 Maiz/nuevos_final.bed
-rw-r--r--  0 camilo staff    3604 Jan 17  2020 Maiz/nuevos_final.fam
```

Esto puede ser de utilidad en caso de que se necesite corroborar la existencia de un archivo en particular dentro de un archivo ya comprimido antes de descomprimirlo, por ejemplo.

###Crear archivos desde la terminal
Los comando `vi`, `nano` y `touch` permiten crear archivos desde la terminal.

El comando`touch` crea un archivo vacío, mientras que `nano` y `vi` abren "ventanas" que permiten ingresar texto, aunque `vi` requiere de aprenderse los atajos del teclado para usarlo.

El comando `curl` permite descargar archivos desde internet, ejemplo: 

```
curl -s "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&rettype=fasta&id=AB080944.1"
>AB080944.1 Pinus patula chloroplast matK gene for maturase, complete cds
ATGGATGAGTTCCATAGATGCGGAAAGGAAGATAGCTTTTGGCAACAATGCTTTTTATATCCACTCTTTT
TTCAGGAAGATCTTTACGCAATTTCTCATGATCATTATTTGGATGTATCAAGTTCCTCCAGACCGATGGA
ACATTTAAGTTCCAATGATCAATTAAGTTTCCTAACTGTAAAACGTTTGATTGGTCAAATACGTCAACAA
AATCATTCAATTGTTTTATTCGTGAATTGCGATCCAAATCCATTAGCTGATCGCAAGAAGAGTTTCTATT
CTGAATCGGTACTAGAAGCACTTACATTGGTCCTGGAAGTTCCGTTCTCTATATGGTCAAAATATTCTGT
GGAAGGGATGAATGAATCGAAGAGTTTCCGGTCGATCCATTCAATATTTCCCTTCTTAGAGGATAAATTC
CCGCATTCAAATTCTATATTAGATGCACGAATACCCTATTCTATTCATCCGGAAATTTTGGTTCGAACCT
TTCGTCGCTGGATCCGAGATGCTCCCTCCTTGCACCCATTACGATCTGTTCTCTATGAATATAGAAATAG
TCCAGATAATTTACAAAGATCAATTATTGTCGTCCCAAGAGTAAATACGAGATTCTTCCTGTTCCTGTGG
AATTATTATGTCTGTGAATGCGAATCCATTTTATTTTCCCGTCTTAAACGATCCTCTCATTCACGATCGT
TGACTCATGGATCTTTCCCTCAGCGAACTCATTTTCATCGAAAGATAAAACATATTATCATATTTTCTCG
TCGAAATTCACTGAAAAGTATCTGGTCGTTGAAGGATCCTAAAATTCACTATGTTAGATATGGCGAAAGA
CCTATTATAGCTATAAAGGGTGCTCATCTCCTAGTTAAAAAATGTAGATATTATCTTCTAATTTTTCGGC
AATTTTATTTCCATCTTTGGTCCGAACCGTATAGGGTCTGTTCTCATCAATTATCCAAGAATTGTTCTTC
TTCTCCAGGTTATTTTTTGAGGGTTCGGATGAACCCTATTTTGGTCAGAACCAAAATGCTCGATGAGTTA
TTCATCGCCGATCTTATTACCGATGAAATTGATCCAATAGTTCCGATTGTACCAATAATTGGATTATTGG
CTACAGAAAAATTCTGTGACATATCAGGGCGGCCAATTAGTAAATTGTCTTGGACCAGTCTAACAGATGA
TGATATCCTCGATCGATTCGATCAAATTTGGAGAAATCTTTTTCATTACTACAGTGGATCCTTTGATCGA
GATGGTTTATATCGTATAAAGTATATACTTTCATTATCATGTGCTAAAACTTTAGCCTGTAAACATAAAA
GTACGATACGTGTAGTTCGGAAGGAATTAGGTCCAGAACTCTTTAAAAAATCGTTTTCAAAAGAACGAGA
ATTTTATTCTCTGCGCTTTTCATCAAAAGCGGCGGCCCGTTCGCAGAGAGAACGAATTTGGCATTCAGAT
ATTTCCCAGATAAATCCCCTAGCTAATTCCTGGCAAAAGATACAGGATCTGAAAATAGAAAACTTATTTG
ACCAATGAAATGCTCTTTGAGTAATTGCCTCGATTCAGAATCATTTTTATTTTTCTATCCGAGAACTAAA
ATGATTAGGAAATAGATACATTACATGGGGAAAGCCGTGTGCAATGAGAAT
```
###Uso de `*``?``[]`

**Ejercicio: Necesitamos crear más archivos .bed y .fam para los ejemplos de abajo. Queremos qué se llamen `ejemplo_final.bed` y `ejemplo_final.fam`. ¿Cómo hacerlo?**

Podemos utilizar el comando `touch` de la siguiente manera: 

```
$ touch ejemplo_final.bed
$ touch ejemplo_final.fam
$ ls -l
total 5224
-rw-r--r--  1 camilo  staff     0B Jul  7 22:23 ejemplo_final.bed
-rw-r--r--  1 camilo  staff     0B Jul  7 22:23 ejemplo_final.fam
-rw-r--r--  1 camilo  staff     9B Jul  7 22:22 ejemplonano.txt
-rw-r--r--@ 1 camilo  staff   1.5M Jan 17  2020 nuevos_final.bed
-rw-r--r--@ 1 camilo  staff   1.1M Jan 17  2020 nuevos_final.bim
-rw-r--r--@ 1 camilo  staff   3.5K Jan 17  2020 nuevos_final.fam
-rw-r--r--@ 1 camilo  staff   1.8K Jan 17  2020 nuevos_final.log
```
El comodín `*` permite buscar archivos que calcen con los caracteres indicados antes o después del asterisco, completando los que falten después o antes respectivamente, ejemplo: 

```
$ ls nuevo*
nuevos_final.bed nuevos_final.bim nuevos_final.fam nuevos_final.log
$ ls *.bed
ejemplo_final.bed nuevos_final.bed
```
El comodín `?` es similar a `*` pero permite reemplazar un solo caracter.

```
$ ls *.b??
ejemplo_final.bed nuevos_final.bed  nuevos_final.bim
```

###Funciones de búsqueda de archivos

Los comandos `less` y `more` permiten abrir archivos una línea o página a la vez. Para salir se debe presionar "q". `less` permite abrir más tipos de archivos.

El comando `head` muestra por defecto las primeras 10 líneas de un archivo.

```
$ less nuevos_final.fam
$ head nuevos_final.fam
1 maiz_3 0 0 0 -9
2 maiz_68 0 0 0 -9
3 maiz_91 0 0 0 -9
4 maiz_39 0 0 0 -9
5 maiz_12 0 0 0 -9
6 maiz_41 0 0 0 -9
7 maiz_35 0 0 0 -9
8 maiz_58 0 0 0 -9
9 maiz_51 0 0 0 -9
10 maiz_82 0 0 0 -9
```
`tail` muestra las últimas lineas de un archivo, lo que puede ser útil para verificar el largo del archivo, cual fue la última fila agregada, etc.

El comando `wc` cuenta el número de líneas, palabras y caracteres de un archivo.

```
$ wc nuevos_final.fam
     165     990    3604 nuevos_final.fam
```
Por otro lado, el comando `cat` sirve para *concatenar* o pegar archivos uno después del otro. Si no se especifica un segundo archivo, `cat` "imprimirá" el contenido del archivo en la terminal.

```
$ cat nuevos_final.fam *log
1 maiz_3 0 0 0 -9
2 maiz_68 0 0 0 -9
3 maiz_91 0 0 0 -9
4 maiz_39 0 0 0 -9
5 maiz_12 0 0 0 -9
6 maiz_41 0 0 0 -9
7 maiz_35 0 0 0 -9
8 maiz_58 0 0 0 -9
9 maiz_51 0 0 0 -9
10 maiz_82 0 0 0 -9
11 maiz_67 0 0 0 -9
12 maiz_93 0 0 0 -9
13 maiz_21 0 0 0 -9
14 maiz_6 0 0 0 -9
15 maiz_101 0 0 0 -9
16 maiz_27 0 0 0 -9
17 maiz_43 0 0 0 -9
18 maiz_1 0 0 0 -9
19 maiz_33 0 0 0 -9
20 maiz_100 0 0 0 -9
21 maiz_24 0 0 0 -9
22 maiz_103 0 0 0 -9
23 maiz_72 0 0 0 -9
24 maiz_10 0 0 0 -9
25 maiz_28 0 0 0 -9
26 maiz_49 0 0 0 -9
27 maiz_56 0 0 0 -9
28 maiz_66 0 0 0 -9
29 maiz_52 0 0 0 -9
30 maiz_47 0 0 0 -9
31 maiz_80 0 0 0 -9
32 maiz_65 0 0 0 -9
33 maiz_94 0 0 0 -9
34 maiz_36 0 0 0 -9
35 maiz_26 0 0 0 -9
36 maiz_105 0 0 0 -9
37 maiz_30 0 0 0 -9
38 maiz_16 0 0 0 -9
39 maiz_42 0 0 0 -9
40 maiz_4 0 0 0 -9
41 maiz_31 0 0 0 -9
42 maiz_17 0 0 0 -9
43 maiz_46 0 0 0 -9
44 maiz_5 0 0 0 -9
45 maiz_32 0 0 0 -9
46 maiz_19 0 0 0 -9
47 maiz_50 0 0 0 -9
48 maiz_8 0 0 0 -9
49 maiz_34 0 0 0 -9
50 maiz_23 0 0 0 -9
51 maiz_54 0 0 0 -9
52 maiz_14 0 0 0 -9
53 maiz_37 0 0 0 -9
54 maiz_25 0 0 0 -9
55 maiz_55 0 0 0 -9
56 maiz_40 0 0 0 -9
57 maiz_29 0 0 0 -9
58 maiz_60 0 0 0 -9
59 maiz_44 0 0 0 -9
60 maiz_74 0 0 0 -9
61 maiz_89 0 0 0 -9
62 maiz_64 0 0 0 -9
63 maiz_83 0 0 0 -9
64 maiz_75 0 0 0 -9
65 maiz_92 0 0 0 -9
66 maiz_69 0 0 0 -9
67 maiz_84 0 0 0 -9
68 maiz_76 0 0 0 -9
69 maiz_97 0 0 0 -9
70 maiz_70 0 0 0 -9
71 maiz_85 0 0 0 -9
72 maiz_77 0 0 0 -9
73 maiz_71 0 0 0 -9
74 maiz_86 0 0 0 -9
75 maiz_78 0 0 0 -9
76 maiz_102 0 0 0 -9
77 maiz_73 0 0 0 -9
78 maiz_88 0 0 0 -9
79 maiz_79 0 0 0 -9
80 maiz_106 0 0 0 -9
81 maiz_119 0 0 0 -9
82 maiz_148 0 0 0 -9
83 maiz_108 0 0 0 -9
84 maiz_120 0 0 0 -9
85 maiz_151 0 0 0 -9
86 maiz_134 0 0 0 -9
87 maiz_123 0 0 0 -9
88 maiz_153 0 0 0 -9
89 maiz_135 0 0 0 -9
90 maiz_124 0 0 0 -9
91 maiz_184 0 0 0 -9
92 maiz_140 0 0 0 -9
93 maiz_125 0 0 0 -9
94 maiz_141 0 0 0 -9
95 maiz_131 0 0 0 -9
96 maiz_189 0 0 0 -9
97 maiz_57 0 0 0 -9
98 maiz_126 0 0 0 -9
99 maiz_113 0 0 0 -9
100 maiz_138 0 0 0 -9
101 maiz_63 0 0 0 -9
102 maiz_127 0 0 0 -9
103 maiz_114 0 0 0 -9
104 maiz_139 0 0 0 -9
105 maiz_99 0 0 0 -9
106 maiz_129 0 0 0 -9
107 maiz_116 0 0 0 -9
108 maiz_142 0 0 0 -9
109 maiz_110 0 0 0 -9
110 maiz_132 0 0 0 -9
111 maiz_118 0 0 0 -9
112 maiz_144 0 0 0 -9
113 maiz_133 0 0 0 -9
114 maiz_121 0 0 0 -9
115 maiz_111 0 0 0 -9
116 maiz_137 0 0 0 -9
117 maiz_109 0 0 0 -9
118 maiz_146 0 0 0 -9
119 maiz_164 0 0 0 -9
120 maiz_157 0 0 0 -9
121 maiz_171 0 0 0 -9
122 maiz_149 0 0 0 -9
123 maiz_165 0 0 0 -9
124 maiz_159 0 0 0 -9
125 maiz_172 0 0 0 -9
126 maiz_150 0 0 0 -9
127 maiz_166 0 0 0 -9
128 maiz_160 0 0 0 -9
129 maiz_173 0 0 0 -9
130 maiz_152 0 0 0 -9
131 maiz_167 0 0 0 -9
132 maiz_161 0 0 0 -9
133 maiz_174 0 0 0 -9
134 maiz_154 0 0 0 -9
135 maiz_169 0 0 0 -9
136 maiz_162 0 0 0 -9
137 maiz_176 0 0 0 -9
138 maiz_156 0 0 0 -9
139 maiz_170 0 0 0 -9
140 maiz_163 0 0 0 -9
141 maiz_177 0 0 0 -9
142 maiz_178 0 0 0 -9
143 maiz_192 0 0 0 -9
144 maiz_185 0 0 0 -9
145 maiz_201 0 0 0 -9
146 maiz_179 0 0 0 -9
147 maiz_193 0 0 0 -9
148 maiz_186 0 0 0 -9
149 maiz_202 0 0 0 -9
150 maiz_180 0 0 0 -9
151 maiz_195 0 0 0 -9
152 maiz_187 0 0 0 -9
153 maiz_181 0 0 0 -9
155 maiz_197 0 0 0 -9
156 maiz_188 0 0 0 -9
157 maiz_182 0 0 0 -9
158 maiz_198 0 0 0 -9
159 maiz_190 0 0 0 -9
160 maiz_200 0 0 0 -9
161 maiz_183 0 0 0 -9
162 maiz_191 0 0 0 -9
163 teos_96 0 0 0 -9
164 teos_203 0 0 0 -9
163 teos_911 0 0 0 -9
164 teos_9107 0 0 0 -9

@----------------------------------------------------------@
|        PLINK!       |     v1.07      |   10/Aug/2009     |
|----------------------------------------------------------|
|  (C) 2009 Shaun Purcell, GNU General Public License, v2  |
|----------------------------------------------------------|
|  For documentation, citation & bug-report instructions:  |
|        http://pngu.mgh.harvard.edu/purcell/plink/        |
@----------------------------------------------------------@

Web-based version check ( --noweb to skip )
Recent cached web-check found... OK, v1.07 is current

+++ PLINK 1.9 is now available! See above website for details +++ 

Writing this text to log file [ nuevos_final.log ]
Analysis started: Wed May 06 12:19:25 2015

Options in effect:
	--file nuevos_final
	--out nuevos_final
	--recodeA

36931 (of 36931) markers to be included from [ nuevos_final.map ]
Warning, found 165 individuals with ambiguous sex codes
Writing list of these individuals to [ nuevos_final.nosex ]
165 individuals read from [ nuevos_final.ped ] 
0 individuals with nonmissing phenotypes
Assuming a disease phenotype (1=unaff, 2=aff, 0=miss)
Missing phenotype value is also -9
0 cases, 0 controls and 165 missing
0 males, 0 females, and 165 of unspecified sex
Before frequency and genotyping pruning, there are 36931 SNPs
165 founders and 0 non-founders found
Total genotyping rate in remaining individuals is 0.990151
0 SNPs failed missingness test ( GENO > 1 )
0 SNPs failed frequency test ( MAF < 0 )
After frequency and genotyping pruning, there are 36931 SNPs
After filtering, 0 cases, 0 controls and 165 missing
After filtering, 0 males, 0 females, and 165 of unspecified sex
Writing recoded file to [ nuevos_final.raw ] 

Analysis finished: Wed May 06 12:19:30 2015
```
En este caso `cat`concatenó el archivo nuevos_final.fam con cualquier archivo que termine en "log".

**Ejercicio ¿Cómo concatenar tres o más archivos a la vez?**

Se debe utilizar el comando `cat` y poner aquellos archivos que se desea concatenar separados por un espacio, ejemplo:

```
$ cat nuevos_final.fam ejemplo_final.bed ejemplo_final.fam
1 maiz_3 0 0 0 -9
2 maiz_68 0 0 0 -9
3 maiz_91 0 0 0 -9
4 maiz_39 0 0 0 -9
5 maiz_12 0 0 0 -9
6 maiz_41 0 0 0 -9
7 maiz_35 0 0 0 -9
8 maiz_58 0 0 0 -9
9 maiz_51 0 0 0 -9
10 maiz_82 0 0 0 -9
11 maiz_67 0 0 0 -9
12 maiz_93 0 0 0 -9
13 maiz_21 0 0 0 -9
14 maiz_6 0 0 0 -9
15 maiz_101 0 0 0 -9
16 maiz_27 0 0 0 -9
17 maiz_43 0 0 0 -9
18 maiz_1 0 0 0 -9
19 maiz_33 0 0 0 -9
20 maiz_100 0 0 0 -9
21 maiz_24 0 0 0 -9
22 maiz_103 0 0 0 -9
23 maiz_72 0 0 0 -9
24 maiz_10 0 0 0 -9
25 maiz_28 0 0 0 -9
26 maiz_49 0 0 0 -9
27 maiz_56 0 0 0 -9
28 maiz_66 0 0 0 -9
29 maiz_52 0 0 0 -9
30 maiz_47 0 0 0 -9
31 maiz_80 0 0 0 -9
32 maiz_65 0 0 0 -9
33 maiz_94 0 0 0 -9
34 maiz_36 0 0 0 -9
35 maiz_26 0 0 0 -9
36 maiz_105 0 0 0 -9
37 maiz_30 0 0 0 -9
38 maiz_16 0 0 0 -9
39 maiz_42 0 0 0 -9
40 maiz_4 0 0 0 -9
41 maiz_31 0 0 0 -9
42 maiz_17 0 0 0 -9
43 maiz_46 0 0 0 -9
44 maiz_5 0 0 0 -9
45 maiz_32 0 0 0 -9
46 maiz_19 0 0 0 -9
47 maiz_50 0 0 0 -9
48 maiz_8 0 0 0 -9
49 maiz_34 0 0 0 -9
50 maiz_23 0 0 0 -9
51 maiz_54 0 0 0 -9
52 maiz_14 0 0 0 -9
53 maiz_37 0 0 0 -9
54 maiz_25 0 0 0 -9
55 maiz_55 0 0 0 -9
56 maiz_40 0 0 0 -9
57 maiz_29 0 0 0 -9
58 maiz_60 0 0 0 -9
59 maiz_44 0 0 0 -9
60 maiz_74 0 0 0 -9
61 maiz_89 0 0 0 -9
62 maiz_64 0 0 0 -9
63 maiz_83 0 0 0 -9
64 maiz_75 0 0 0 -9
65 maiz_92 0 0 0 -9
66 maiz_69 0 0 0 -9
67 maiz_84 0 0 0 -9
68 maiz_76 0 0 0 -9
69 maiz_97 0 0 0 -9
70 maiz_70 0 0 0 -9
71 maiz_85 0 0 0 -9
72 maiz_77 0 0 0 -9
73 maiz_71 0 0 0 -9
74 maiz_86 0 0 0 -9
75 maiz_78 0 0 0 -9
76 maiz_102 0 0 0 -9
77 maiz_73 0 0 0 -9
78 maiz_88 0 0 0 -9
79 maiz_79 0 0 0 -9
80 maiz_106 0 0 0 -9
81 maiz_119 0 0 0 -9
82 maiz_148 0 0 0 -9
83 maiz_108 0 0 0 -9
84 maiz_120 0 0 0 -9
85 maiz_151 0 0 0 -9
86 maiz_134 0 0 0 -9
87 maiz_123 0 0 0 -9
88 maiz_153 0 0 0 -9
89 maiz_135 0 0 0 -9
90 maiz_124 0 0 0 -9
91 maiz_184 0 0 0 -9
92 maiz_140 0 0 0 -9
93 maiz_125 0 0 0 -9
94 maiz_141 0 0 0 -9
95 maiz_131 0 0 0 -9
96 maiz_189 0 0 0 -9
97 maiz_57 0 0 0 -9
98 maiz_126 0 0 0 -9
99 maiz_113 0 0 0 -9
100 maiz_138 0 0 0 -9
101 maiz_63 0 0 0 -9
102 maiz_127 0 0 0 -9
103 maiz_114 0 0 0 -9
104 maiz_139 0 0 0 -9
105 maiz_99 0 0 0 -9
106 maiz_129 0 0 0 -9
107 maiz_116 0 0 0 -9
108 maiz_142 0 0 0 -9
109 maiz_110 0 0 0 -9
110 maiz_132 0 0 0 -9
111 maiz_118 0 0 0 -9
112 maiz_144 0 0 0 -9
113 maiz_133 0 0 0 -9
114 maiz_121 0 0 0 -9
115 maiz_111 0 0 0 -9
116 maiz_137 0 0 0 -9
117 maiz_109 0 0 0 -9
118 maiz_146 0 0 0 -9
119 maiz_164 0 0 0 -9
120 maiz_157 0 0 0 -9
121 maiz_171 0 0 0 -9
122 maiz_149 0 0 0 -9
123 maiz_165 0 0 0 -9
124 maiz_159 0 0 0 -9
125 maiz_172 0 0 0 -9
126 maiz_150 0 0 0 -9
127 maiz_166 0 0 0 -9
128 maiz_160 0 0 0 -9
129 maiz_173 0 0 0 -9
130 maiz_152 0 0 0 -9
131 maiz_167 0 0 0 -9
132 maiz_161 0 0 0 -9
133 maiz_174 0 0 0 -9
134 maiz_154 0 0 0 -9
135 maiz_169 0 0 0 -9
136 maiz_162 0 0 0 -9
137 maiz_176 0 0 0 -9
138 maiz_156 0 0 0 -9
139 maiz_170 0 0 0 -9
140 maiz_163 0 0 0 -9
141 maiz_177 0 0 0 -9
142 maiz_178 0 0 0 -9
143 maiz_192 0 0 0 -9
144 maiz_185 0 0 0 -9
145 maiz_201 0 0 0 -9
146 maiz_179 0 0 0 -9
147 maiz_193 0 0 0 -9
148 maiz_186 0 0 0 -9
149 maiz_202 0 0 0 -9
150 maiz_180 0 0 0 -9
151 maiz_195 0 0 0 -9
152 maiz_187 0 0 0 -9
153 maiz_181 0 0 0 -9
155 maiz_197 0 0 0 -9
156 maiz_188 0 0 0 -9
157 maiz_182 0 0 0 -9
158 maiz_198 0 0 0 -9
159 maiz_190 0 0 0 -9
160 maiz_200 0 0 0 -9
161 maiz_183 0 0 0 -9
162 maiz_191 0 0 0 -9
163 teos_96 0 0 0 -9
164 teos_203 0 0 0 -9
163 teos_911 0 0 0 -9
164 teos_9107 0 0 0 -9
```

###Expresiones regulares y búsqueda de patrones

El comando `grep` permite buscar expresiones regulares en uno o más archivos.

**Pregunta ¿Cómo buscar el manual de grep en la Terminal?**

Con el comando `man`

####Usos comunes de `grep`
Leer el archivo tomatesverdes.fasta con el comando `less`

```
$ less tomatesverdes.fasta

>gi|156628893|gb|EF438894.1| Physalis philadelphica isolate P050 maturase K (matK) gene, partial cds; chloroplast
TAGGTCGATTTTGTTGGAAAATCCAGGTTATAACAATAAATTTAGTTTCCTAATTGTGAAACGTTTAATT
ACTCGAATGTATCAACAGAATCATTTTATTATTTCTACTAATGATTCTAACAAAAATCCATTTTTGGGGT
GCAACAAGAGTTTGTATTCTCAAATGATATCAGAGGGATTTGCATTTATTGTGGAAATTCCGTTTTCTCT
ACGATTAATATCTTCTTTATCTTCTTTCGAAGGCAAAAAGATTTTAAAATCTCATAATTTACGATCAATT
CATTCAACATTTCCTTTTTTAGAGGACAATTTTTCACATCTAAATTATGTATTAGATATACTAATACCCT
ACCCCGTTCATCTGGAAATCTTGGTTCAAACTCTTCGCTATTGGGTAAAAGATGCCTCTTCTTTACATTT
ATTACGATTCTTTCTCCACGAATATTGGAATTTGAATAGTCTTATTACTTCAAAGAAGCCCGGTTACTCC
TTTTCAAAAAAAAATCAAAGATTCTTCTTCTTCTTATATAATTCTTATGTATATGAATGGGAATCCACTT
TCGTCTTTCTACGGAACCAATCTTCTCATTTACGATCAACATCTTTTGGAGCCCTTCTTGAACGAATATA
TTTCTATGGAAAAATAGAACGTCTTGTAGAAGTCTTTGCTAAGGATTTTCAGGTTACCTTATGGTTATTC
AAGGATCCTTTCATGCATTATGTTAGGTATCAAGGAAAATCAATTCTGGCTTCAAAAGGGACGTTTCTTT
TGATGAATAAATGGAAATTTTACCTTGTCAATTTTTGGCAATGTCATTTTTTTCTGTGCTTTCACACAGG
AAGGATCCATATAAACCAATTATCCAATCATTTACGTGACTTTATGGGCTATCTTTCAAGTGTGCGACTA
AATCATTCAATGGTACGTAGTCAAATGTTAGAAAA
>gi|156629011|gb|EF438953.1| Physalis philadelphica isolate P060 maturase K (matK) gene, partial cds; chloroplast
TAGGTCGATTTTGTTGGAAAATCCAGGTTATAACAATAAATTTAGTTTCCTAATTGTGAAACGTTTAATT
ACTCGAATGTATCAACAGAATCATTTTATTATTTCTACTAATGATTCTAACAAAAATCCATTTTTGGGGT
GCAACAAGAGTTTGTATTCTCAAATGATATCAGAGGGATTTGCATTTATTGTGGAAATTCCGTTTTCTCT
ACGATTAATATCTTCTTTATCTTCTTTCGAAGGCAAAAAGATTTTAAAATCTCATAATTTACGATCAATT
CATTCAACATTTCCTTTTTTAGAGGACAATTTTTCACATCTAAATTATGTATTAGATATACTAATACCCT
ACCCCGTTCATCTGGAAATCTTGGTTCAAACTCTTCGCTATTGGGTAAAAGATGCCTCTTCTTTACATTT
ATTACGATTCTTTCTCCACGAATATTGGAATTTGAATAGTCTTATTACTTCAAAGAAGCCCGGTTACTCC
TTTTCAAAAAAAAATCAAAGATTCTTCTTCTTCTTATATAATTCTTATGTATATGAATGGGAATCCACTT
TCGTCTTTCTACGGAACCAATCTTCTCATTTACGATCAACATCTTTTGGAGCCCTTCTTGAACGAATATA
TTTCTATGGAAAAATAGAACGTCTTGTAGAAGTCTTTGCTAAGGATTTTCAGGTTACCTTATGGTTATTC
AAGGATCCTTTCATGCATTATGTTAGGTATCAAGGAAAATCAATTCTGGCTTCAAAAGGGACGTTTCTTT
TGATGAATAAATGGAAATTTTACCTTGTCAATTTTTGGCAATGTCATTTTTTTCTGTGCTTTCACACAGG
AAGGATCCATATAAACCAATTATCCAATCATTTACGTGACTTTATGGGCTATCTTTCAAGTGTGCGACTA
AATCATTCAATGGTACGTAGTCAAATGTTAGAAAA
```
**1) ¿Qué tipo de archivo es?** 

Un archivo tipo fasta 

**2) ¿Cuántas secuencias contiene?**

5 Secuencias

**3) Cuál es el encabezado de las secuencias?**

Cada secuencia está encabezada por una línea de texto que indica cosas como la especie a la que pertenece y el gen al que corresponde y que se identifica con el signo ">".

El comando `grep` permite buscar expresiones regulares y mostrar las líneas en qué aparece dicha expresión.

```
$ grep ">" tomatesverdes.fasta
>gi|156629013|gb|EF438954.1| Physalis philadelphica isolate P061 maturase K (matK) gene, partial cds; chloroplast
>gi|156629009|gb|EF438952.1| Physalis philadelphica isolate P059 maturase K (matK) gene, partial cds; chloroplast
>gi|156628921|gb|EF438908.1| Physalis philadelphica isolate P056 maturase K (matK) gene, partial cds; chloroplast
>gi|156628893|gb|EF438894.1| Physalis philadelphica isolate P050 maturase K (matK) gene, partial cds; chloroplast
>gi|156629011|gb|EF438953.1| Physalis philadelphica isolate P060 maturase K (matK) gene, partial cds; chloroplast
(base) 
```
**Pregunta: ¿Por qué está ">" entre comillas?**

Está entre comillas para que sea reconocido como símbolo y no como "comando" por la terminal.

**Ejercicio En el mismo directorio hay otro archivo fasta. Utiliza `grep` y algo más para ver el encabezado de tomatesverdes.fasta y jitomate.fasta. ¿Qué diferencia hay con el output anterior?**

Se puede utilizar `grep` y separar los nombres de los archivos por un espacio.

```
$ grep ">" tomatesverdes.fasta jitomate.fasta
tomatesverdes.fasta:>gi|156629013|gb|EF438954.1| Physalis philadelphica isolate P061 maturase K (matK) gene, partial cds; chloroplast
tomatesverdes.fasta:>gi|156629009|gb|EF438952.1| Physalis philadelphica isolate P059 maturase K (matK) gene, partial cds; chloroplast
tomatesverdes.fasta:>gi|156628921|gb|EF438908.1| Physalis philadelphica isolate P056 maturase K (matK) gene, partial cds; chloroplast
tomatesverdes.fasta:>gi|156628893|gb|EF438894.1| Physalis philadelphica isolate P050 maturase K (matK) gene, partial cds; chloroplast
tomatesverdes.fasta:>gi|156629011|gb|EF438953.1| Physalis philadelphica isolate P060 maturase K (matK) gene, partial cds; chloroplast
jitomate.fasta:>gi|315140847|gb|HQ593449.1| Solanum lycopersicum voucher AP471 maturase K (matK) gene, partial cds; chloroplast
jitomate.fasta:>gi|385137316|gb|JQ412261.1| Solanum lycopersicum voucher BS0156 maturase K (matK) gene, partial cds; chloroplast
jitomate.fasta:>gi|315259972|gb|HQ619840.1| Solanum lycopersicum isolate LegMedMO_116 maturase K (matK) gene, partial cds; chloroplast
```
La diferencia con el output anterior es que muestra al inicio a qué archivo corresponde cada línea.

El comando `grep` con el argumento `-c` permite contar la cantidad de líneas en que aparece la expresión regular buscada.

``` 
$ grep -c ">" tomatesverdes.fasta
5

``` 
El argumento `-l` permite enlistar los documentos en que aparece la expresión regular buscada.

```
$ grep -l Physalis *.fasta
tomates.fasta
tomatesverdes.fasta
```
El argumento `-i` sirve para hacer la búsqueda sensible a mayúsculas/minúsculas.

```
$ grep -li physalis *.fasta
tomates.fasta
tomatesverdes.fasta
```
Argumento `-w` busca palabras completas.

```
$ grep iso tomatesverdes.fasta
>gi|156629013|gb|EF438954.1| Physalis philadelphica isolate P061 maturase K (matK) gene, partial cds; chloroplast
>gi|156629009|gb|EF438952.1| Physalis philadelphica isolate P059 maturase K (matK) gene, partial cds; chloroplast
>gi|156628921|gb|EF438908.1| Physalis philadelphica isolate P056 maturase K (matK) gene, partial cds; chloroplast
>gi|156628893|gb|EF438894.1| Physalis philadelphica isolate P050 maturase K (matK) gene, partial cds; chloroplast
>gi|156629011|gb|EF438953.1| Physalis philadelphica isolate P060 maturase K (matK) gene, partial cds; chloroplast
$ grep -w iso tomatesverdes.fasta
$
```
`grep -E` sirve para interpretar el texto entre comillas como una expresión regular completa, incluyendo operadores, cuantificadores y posicionadores. El argumento `-o` muestra la parte del texto que cumple con la expresión regular.

```
$ grep -oE "\| \w+ \w+" tomatesverdes.fasta
| Physalis philadelphica
| Physalis philadelphica
| Physalis philadelphica
| Physalis philadelphica
| Physalis philadelphica
```
**Ejercicio 1 Obtener el nombre de la especie Physalis philadelphica como en el ejemplo anterior, pero sin el "|" del principio.**

```
$ grep -oE "Physalis philadelphica" tomatesverdes.fasta
Physalis philadelphica
Physalis philadelphica
Physalis philadelphica
Physalis philadelphica
Physalis philadelphica
```
**Ejercicio 2 Obtener el nombre de las secuencias de los archivos tomatesverdes.fasta y jitomae.fasta y escribirlos a un archivo llamado secsIDs. No importa cómo escribas la expresión regular, pero el chiste es lograr que toda la operación sea en una sola línea de código.**

```
$ grep -oE ">\w+\|\w+\|\w+\|\w+\W\w+\|" tomatesverdes.fasta jitomate.fasta > "secsIDs.txt"
$ less secsIDs.txt
tomatesverdes.fasta:>gi|156629013|gb|EF438954.1|
tomatesverdes.fasta:>gi|156629009|gb|EF438952.1|
tomatesverdes.fasta:>gi|156628921|gb|EF438908.1|
tomatesverdes.fasta:>gi|156628893|gb|EF438894.1|
tomatesverdes.fasta:>gi|156629011|gb|EF438953.1|
jitomate.fasta:>gi|315140847|gb|HQ593449.1|
jitomate.fasta:>gi|385137316|gb|JQ412261.1|
jitomate.fasta:>gi|315259972|gb|HQ619840.1|
secsIDs.txt (END)
```
###Redirección con bash
**Pregunta ¿Qué son el Standard output y el Standard input?**

El standard output corresponde al output "normal" o "esperado" para un determinado comando, mientras que el standard input corresponde a los comandos ingresados en la terminal.

`>` y `>>` Redirigen el stdout a un archivo en lugar de mostrarlo en la terminal.

```
$ cat nuevos_final.fam *log > catejemplo.txt
$ head catejemplo.txt
1 maiz_3 0 0 0 -9
2 maiz_68 0 0 0 -9
3 maiz_91 0 0 0 -9
4 maiz_39 0 0 0 -9
5 maiz_12 0 0 0 -9
6 maiz_41 0 0 0 -9
7 maiz_35 0 0 0 -9
8 maiz_58 0 0 0 -9
9 maiz_51 0 0 0 -9
10 maiz_82 0 0 0 -9
$ tail catejemplo.txt
Total genotyping rate in remaining individuals is 0.990151
0 SNPs failed missingness test ( GENO > 1 )
0 SNPs failed frequency test ( MAF < 0 )
After frequency and genotyping pruning, there are 36931 SNPs
After filtering, 0 cases, 0 controls and 165 missing
After filtering, 0 males, 0 females, and 165 of unspecified sex
Writing recoded file to [ nuevos_final.raw ] 

Analysis finished: Wed May 06 12:19:30 2015
```
En caso que el archivo catejemplo.txt. exista, el comando `>` borrará el archivo preexistente, en cambio `>>` agregará el nuevo output al final de dicho archivo.

**Ejercicio utiliza sed para sustituir "Solanum lycopersicum" del archivo Tomates/tomates.fasta por "jitomate" y guarda el output en un nuevo archivo llamado "edited_tomates.fasta"**

```
$ sed 's/Solanum lycopersicum/Jitomate/g' tomates.fasta > edited_tomates.fasta
$ head edited_tomates.fasta
>gi|315140847|gb|HQ593449.1| Jitomate voucher AP471 maturase K (matK) gene, partial cds; chloroplast
TTGCACATCTAAATTATGTATTAGATATACTAATACCCTACCCCGTTCATCTGGAAATCTTGGTTCAAAC
TCTTCGCTATTGGGTAAAAGATGCCTCTTCTTTACATTTATTACGATTCTTTCTCCACGAATATTGTAAT
TTGAATAGTCTTATTACTTCAAAGAAGCCCGGTTACTCCTTTTCAAAAAAAAATCAAAGATTCTTCTTCT
TCTTATATAATTCTTATGTATATGAATGCGAATCCACTTTCGTCTTTCTACGGAACCAATCTTCTCATTT
ACGATCAACATCTTTTGGAGCCCTTCTTGAACGAATATATTTCTATGGAAAAATAGAACGTCTTGTAGAA
GTCTTTGCTAAGGATTTTCAGGTTACCCTATGGTTATTCAAGGATCCTTTCATGCATTATGTTAGGTATG
AAGGAAAATCAATTCTGGCTTCAAAAGGGACGTTTCCTTTGATGAATAAATGGAAATTTTACCTTGTCAA
TTTTTGGCAATGTCATTTTTCTATGTACTTTCACACAGGAAGGATCCATATAAACCAATTATCCAACCAT
TCCCGTGACTTTATGGGCTATCTTTCAAGTGTGCGACTAAATCATTCAATGGTACGTAGTCAAATGTTAG
```
El comando `|` transforma el stout de un comando y lo transforma en el input de otro.

**Ejercicio Primero explora qué hace el comando `history`. ¿Cómo lo combinarías con `grep` para buscar cuáles líneas hemos corrido con `less`?**

```
$ history | grep -c "less"
22
```
**Ejercicio ¿Cómo concatenar tres o más archivos a la vez? ¿Y si quisiéramos tener el resultado en un archivo nuevo?**

```
$ cat jitomate.fasta tomates.fasta secsIDs.txt >> concatenados.txt
$ ls
VerdesFritos         edited_tomates.fasta secsIDs.txt
catejemplo.txt       jitomate.fasta       tomates.fasta
concatenados.txt     less                 tomatesverdes.fasta
$ less concatenados
concatenados: No such file or directory
(base) 
```

###Loops en bash

**¿Cuándo debo usar comillas en la lista de elementos?**

Cuando quiero especificar que el elemento a tratar es todo el conjunto de palabras comprendidas entre los caracteres de modo que no trate cada elemento por separado.

**¿Qué hace `;`?**

Separa líneas de comando

**Pregunta ¿De qué manera sencilla borrarías esos 100 directorios que acabas de crear?**

`$ rm -df directorio*`

**Ejercicio Navega al directorio BioinfInvRepro/Unidad1/Prac_Uni1. Desde ahí (i.e. sin utilizar cd) utiliza un for loop para crear por lo menos cuatro directorios dentro del directorio Tomates/VerdesFritos. Tu for loop debe incluir una variable definida externamente.**

####Arreglos

```
$ a=( gato gatito gatnnn )
$ for i in ${a[@]}; do echo El $i hace miau; done
El gato hace miau
El gatito hace miau
El gatnnn hace miau
(base) 
```
Los arrays deben ser llamados con la notación `${a[@]}` y pueden ser el resultado de una función como `grep`

```
$ a=($(grep -oE "\w+_[0-9]*" nuevos_final.fam))
$ for i in ${a[@]}; do echo Hacer algo con la muestra $i; done
Hacer algo con la muestra maiz_3
Hacer algo con la muestra maiz_68
Hacer algo con la muestra maiz_91
Hacer algo con la muestra maiz_39
Hacer algo con la muestra maiz_12
Hacer algo con la muestra maiz_41
Hacer algo con la muestra maiz_35
Hacer algo con la muestra maiz_58
Hacer algo con la muestra maiz_51
Hacer algo con la muestra maiz_82
Hacer algo con la muestra maiz_67
Hacer algo con la muestra maiz_93
Hacer algo con la muestra maiz_21
Hacer algo con la muestra maiz_6
Hacer algo con la muestra maiz_101
Hacer algo con la muestra maiz_27
Hacer algo con la muestra maiz_43
Hacer algo con la muestra maiz_1
Hacer algo con la muestra maiz_33
Hacer algo con la muestra maiz_100
Hacer algo con la muestra maiz_24
Hacer algo con la muestra maiz_103
Hacer algo con la muestra maiz_72
Hacer algo con la muestra maiz_10
Hacer algo con la muestra maiz_28
Hacer algo con la muestra maiz_49
Hacer algo con la muestra maiz_56
Hacer algo con la muestra maiz_66
Hacer algo con la muestra maiz_52
Hacer algo con la muestra maiz_47
Hacer algo con la muestra maiz_80
Hacer algo con la muestra maiz_65
Hacer algo con la muestra maiz_94
Hacer algo con la muestra maiz_36
Hacer algo con la muestra maiz_26
Hacer algo con la muestra maiz_105
Hacer algo con la muestra maiz_30
Hacer algo con la muestra maiz_16
Hacer algo con la muestra maiz_42
Hacer algo con la muestra maiz_4
Hacer algo con la muestra maiz_31
Hacer algo con la muestra maiz_17
Hacer algo con la muestra maiz_46
Hacer algo con la muestra maiz_5
Hacer algo con la muestra maiz_32
Hacer algo con la muestra maiz_19
Hacer algo con la muestra maiz_50
Hacer algo con la muestra maiz_8
Hacer algo con la muestra maiz_34
Hacer algo con la muestra maiz_23
Hacer algo con la muestra maiz_54
Hacer algo con la muestra maiz_14
Hacer algo con la muestra maiz_37
Hacer algo con la muestra maiz_25
Hacer algo con la muestra maiz_55
Hacer algo con la muestra maiz_40
Hacer algo con la muestra maiz_29
Hacer algo con la muestra maiz_60
Hacer algo con la muestra maiz_44
Hacer algo con la muestra maiz_74
Hacer algo con la muestra maiz_89
Hacer algo con la muestra maiz_64
Hacer algo con la muestra maiz_83
Hacer algo con la muestra maiz_75
Hacer algo con la muestra maiz_92
Hacer algo con la muestra maiz_69
Hacer algo con la muestra maiz_84
Hacer algo con la muestra maiz_76
Hacer algo con la muestra maiz_97
Hacer algo con la muestra maiz_70
Hacer algo con la muestra maiz_85
Hacer algo con la muestra maiz_77
Hacer algo con la muestra maiz_71
Hacer algo con la muestra maiz_86
Hacer algo con la muestra maiz_78
Hacer algo con la muestra maiz_102
Hacer algo con la muestra maiz_73
Hacer algo con la muestra maiz_88
Hacer algo con la muestra maiz_79
Hacer algo con la muestra maiz_106
Hacer algo con la muestra maiz_119
Hacer algo con la muestra maiz_148
Hacer algo con la muestra maiz_108
Hacer algo con la muestra maiz_120
Hacer algo con la muestra maiz_151
Hacer algo con la muestra maiz_134
Hacer algo con la muestra maiz_123
Hacer algo con la muestra maiz_153
Hacer algo con la muestra maiz_135
Hacer algo con la muestra maiz_124
Hacer algo con la muestra maiz_184
Hacer algo con la muestra maiz_140
Hacer algo con la muestra maiz_125
Hacer algo con la muestra maiz_141
Hacer algo con la muestra maiz_131
Hacer algo con la muestra maiz_189
Hacer algo con la muestra maiz_57
Hacer algo con la muestra maiz_126
Hacer algo con la muestra maiz_113
Hacer algo con la muestra maiz_138
Hacer algo con la muestra maiz_63
Hacer algo con la muestra maiz_127
Hacer algo con la muestra maiz_114
Hacer algo con la muestra maiz_139
Hacer algo con la muestra maiz_99
Hacer algo con la muestra maiz_129
Hacer algo con la muestra maiz_116
Hacer algo con la muestra maiz_142
Hacer algo con la muestra maiz_110
Hacer algo con la muestra maiz_132
Hacer algo con la muestra maiz_118
Hacer algo con la muestra maiz_144
Hacer algo con la muestra maiz_133
Hacer algo con la muestra maiz_121
Hacer algo con la muestra maiz_111
Hacer algo con la muestra maiz_137
Hacer algo con la muestra maiz_109
Hacer algo con la muestra maiz_146
Hacer algo con la muestra maiz_164
Hacer algo con la muestra maiz_157
Hacer algo con la muestra maiz_171
Hacer algo con la muestra maiz_149
Hacer algo con la muestra maiz_165
Hacer algo con la muestra maiz_159
Hacer algo con la muestra maiz_172
Hacer algo con la muestra maiz_150
Hacer algo con la muestra maiz_166
Hacer algo con la muestra maiz_160
Hacer algo con la muestra maiz_173
Hacer algo con la muestra maiz_152
Hacer algo con la muestra maiz_167
Hacer algo con la muestra maiz_161
Hacer algo con la muestra maiz_174
Hacer algo con la muestra maiz_154
Hacer algo con la muestra maiz_169
Hacer algo con la muestra maiz_162
Hacer algo con la muestra maiz_176
Hacer algo con la muestra maiz_156
Hacer algo con la muestra maiz_170
Hacer algo con la muestra maiz_163
Hacer algo con la muestra maiz_177
Hacer algo con la muestra maiz_178
Hacer algo con la muestra maiz_192
Hacer algo con la muestra maiz_185
Hacer algo con la muestra maiz_201
Hacer algo con la muestra maiz_179
Hacer algo con la muestra maiz_193
Hacer algo con la muestra maiz_186
Hacer algo con la muestra maiz_202
Hacer algo con la muestra maiz_180
Hacer algo con la muestra maiz_195
Hacer algo con la muestra maiz_187
Hacer algo con la muestra maiz_181
Hacer algo con la muestra maiz_197
Hacer algo con la muestra maiz_188
Hacer algo con la muestra maiz_182
Hacer algo con la muestra maiz_198
Hacer algo con la muestra maiz_190
Hacer algo con la muestra maiz_200
Hacer algo con la muestra maiz_183
Hacer algo con la muestra maiz_191
Hacer algo con la muestra teos_96
Hacer algo con la muestra teos_203
Hacer algo con la muestra teos_911
Hacer algo con la muestra teos_9107
```
**Pregunta: Si `some_array=($(command))` sirve para crear un arreglo a partir del resultado de un comando ¿Cómo puedes crear una variable a partir de un comando?**

Puede crearse con el comando entre los signos ' '

```
$ fecha='date'
$ $fecha
Sun Jul 10 20:37:46 -04 2022
```

###Unidad 2
---
####Organización de un proyecto bioinformático

Un proyecto bioinformático puede organizarse utilizando la plataforma "Github" la cual hace uso de la herramienta `git`.
`git config --global user.mail "email@example.com"`

Permite editar el correo de usuario.

`git config --global user.name "Mi_nombre"`

Permite editar el nombre de usuario.

`git clone`

Permite copiar un repositorio que ya existe.

`git status`

Permite identificar el branch en que se está trabajando y si hay archivos por "guardar".

```
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   changedname.txt

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    newfile.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	Unidades_1_2.md
```

`git add` Permite agregar un archivo que no existía en el repositorio o prepara las modificaciones realizadas a archivos existentes (no las guarda).

```
$ git add Unidades_1_2.md
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   Unidades_1_2.md
	new file:   changedname.txt

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    newfile.txt
```

`git commit` confirma y agrega los cambios a la branch en la que se trabaja.

```
$ git commit -m "agregar archivo unidades 1 y 2"
[main 6a822d5] agregar archivo unidades 1 y 2
 2 files changed, 2995 insertions(+)
 create mode 100644 Unidades_1_2.md
 create mode 100644 changedname.txt
```
El argumento `-m` permite agregar un comentario al respecto.

`git diff` para ver los cambios realizados a un archivo.

`git rm` permite borrar archivos que ya habían sido agregados al git (tanto de git como del pc).

`git push` Permite integrar cambios a una rama.



