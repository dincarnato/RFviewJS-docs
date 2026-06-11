# File formats

## Structure files

### Dot-bracket

```
>RNA#1
GGGAUAUAGCGUAUAGCGCGCGCGAUAUUAUAUCGGAUCGCGCCAUUCGCGCCC
(((.....(((.((.(((((..(((((...)))))...))))).)).))).)))
```

Multiple structures within the same file are allowed.


### Connectivity table (CT)

```
   54  RNA#1
    1 G       0    2   54    1
    2 G       1    3   53    2
    3 G       2    4   52    3
    4 A       3    5    0    4
    5 U       4    6    0    5
    6 A       5    7    0    6
    7 U       6    8    0    7
    8 A       7    9    0    8
    9 G       8   10   50    9
   10 C       9   11   49   10
   11 G      10   12   48   11
   12 U      11   13    0   12
   13 A      12   14   46   13
   14 U      13   15   45   14
   15 A      14   16    0   15
   16 G      15   17   43   16
   17 C      16   18   42   17
   18 G      17   19   41   18
   19 C      18   20   40   19
   20 G      19   21   39   20
   21 C      20   22    0   21
   22 G      21   23    0   22
   23 C      22   24   35   23
   24 G      23   25   34   24
   25 A      24   26   33   25
   26 U      25   27   32   26
   27 A      26   28   31   27
   28 U      27   29    0   28
   29 U      28   30    0   29
   30 A      29   31    0   30
   31 U      30   32   27   31
   32 A      31   33   26   32
   33 U      32   34   25   33
   34 C      33   35   24   34
   35 G      34   36   23   35
   36 G      35   37    0   36
   37 A      36   38    0   37
   38 U      37   39    0   38
   39 C      38   40   20   39
   40 G      39   41   19   40
   41 C      40   42   18   41
   42 G      41   43   17   42
   43 C      42   44   16   43
   44 C      43   45    0   44
   45 A      44   46   14   45
   46 U      45   47   13   46
   47 U      46   48    0   47
   48 C      47   49   11   48
   49 G      48   50   10   49
   50 C      49   51    9   50
   51 G      50   52    0   51
   52 C      51   53    3   52
   53 C      52   54    2   53
   54 C      53    0    1   54
```

Multiple structures within the same file are allowed.


### Stockholm

```
# STOCKHOLM 1.0
#=GF ID Glycine
#=GF AC RF00504
#=GF DE Glycine riboswitch aptamer
#=GF AU Moxon SJ; 0000-0003-4644-1816
#=GF GA 32.0
#=GF NC 31.9
#=GF TC 32.0
#=GF PI gcvT
#=GF SE Barrick JE, Breaker RR
#=GF SS Predicted; Barrick JE, Breaker RR
#=GF TP Cis-reg; riboswitch;
#=GF BM cmbuild -F CM SEED
#=GF CB cmcalibrate --mpi CM
#=GF SM cmsearch --cpu 4 --verbose --nohmmonly -T 30.00 -Z 2958934 CM SEQDB
#=GF CL CL00125
#=GF DR SO; 0000035; riboswitch;
#=GF DR GO; 0006545; glycine biosynthetic process;
#=GF RN [1]
#=GF RM 15472076
#=GF RT A glycine-dependent riboswitch that uses cooperative binding to control
#=GF RT gene expression.
#=GF RA Mandal M, Lee M, Barrick JE, Weinberg Z, Emilsson GM, Ruzzo WL, Breaker RR
#=GF RL Science 2004;306:275-279.
#=GF RN [2]
#=GF RM 29089431
#=GF RT In Vivo Behavior of the Tandem Glycine Riboswitch in Bacillus subtilis.
#=GF RA Babina AM, Lea NE, Meyer MM
#=GF RL MBio. 2017; [Epub ahead of print]
#=GF CC This family represents the bacterial glycine riboswitch. Glycine
#=GF CC riboswitches usually consist of two metabolite-binding aptamers domains
#=GF CC with similar structures in tandem. The aptamers cooperatively bind glycine
#=GF CC to regulate the expression of downstream genes. In Bacillus subtilis, this
#=GF CC riboswitch is found upstream of the gcvT operon which controls glycine
#=GF CC degradation. It is thought that when glycine is in excess it will bind to
#=GF CC both aptamers to activate these genes and facilitate glycine degradation
#=GF CC [1]. In vivo experiments demonstrated that glycine does not need to bind
#=GF CC both aptamers for regulation. Mutation to the first aptamer caused
#=GF CC greatest reduction in downstream gene expression, while mutation to the
#=GF CC second one had varying effects. Glycine-induced expression of the gcvT
#=GF CC operon is needed for B. subtilise growth, swarming motility and biofilm
#=GF CC formation (in high glycine enviroment).[2]
#=GF WK Glycine_riboswitch
#=GF SQ 44

AL766849.1/65640-65772     AGACGGACUU-CUGGAGAGACCUA----------------UAAGUAGCAACAUCUUUGUAUUGACACCAAGAUGUGCUCUAGG-CGCCGAAGGGGCAA-GAAGAGUAAAACAA----------------------CUCC-------------------------UCCAAUCUCUCAGGC---------------AAAAG-
AL766849.1/65560-65639     UGACGUCAUU-CAGGAGAAGAAAG----------------UUAGA----------------------------------CUUU-CGCCGAAGGAAUUA----------------------------------------------------------------------CACUCUCAGGU--------GUCUUAAGACAG-
CR522870.1/1448610-1448703 AUGAACAUAG-CAGGAGAGAUUUU----------------UCCCAUGGCAGUACGGAUGG-----------------GGAAGG-CACCGAAGAAGUAA----------------------------------------------------------------------AUCUUUCAGGU---------------CAAAG-
CR522870.1/1448704-1448793 -----AGCCU-CUGGAGAGUCUC-----------------AUUAU-----------------------------------GGG-CACCGAAGGAGCAA-GCCAGCGUGUA-------------------------GCUG-------------------------GUGAACCUCUCAGGU---------------ACAAGG
BX842577.1/344356-344453   CGCUCUAGUG-CGGGAGAGUUCUGUGGCUG----------CCAGC--------------------------------UACGGA-CGCCGAAGGAGCAAUACCUC-------------------------------UCC--------------------------GUCAACCUCUCAGGC---------------ACCCG-
BX842577.1/344457-344587   -----UGCCU-CUGGAAAGCGGUGGC--------------GACCCCUGGCGGUC-----------------------CUCACC-CGCCGAUGGGGAAA-GGCGAUU-----------------------------CACC-------UGACGGUGGACAGAGUCGCCGAAUCUCUCAGGCGCCUGGCGUGCAGGU--GAA-
AL939108.1/255539-255444   UGACCCCGCG-CGGGAGAGUCCUCCGGAC-----------AUCAC--------------------------------CGGAGG-CGCCGAAGGAGCAA-AUCCU-------------------------------CCCC-------------------------GG-AAUCUCUCAGGC---------------UCACG-
AL939108.1/255442-255325   -----UCACU-CUGGAAAGCAGGGCGGGU-----------GUCGACGGCUUC-------------------------CGCUCU-CACCGACGGUGAAA-GCCGGGCAGAGC------------------------UCCA--------------GGGCUCGCCCGGUGAAGCUCUCAGGU--------------UGAGAU-
AE000516.2/79275-79185     UGACGCGAUG-UGGGAGAA-CCUCC---------------AUGUC----------------------------------GAGG-CGCCGUAGGAGCAA-UCUCCU------------------------------CCCC-------------------------GAGAAUCUCUCAGGC---------------CCAAG-
AE017355.1/2242861-2242742 GGACGAAUCU-CUGGAGAGACUCCCUCUCGCU--------UUAAAUAGCGUAGAGGAA-------------------AACGAG-CACCGAAGGAGCAAAUCCGC-------------------------------UACU-------------------AUAGCGGAUAAUCUCUCAGGU---------------AAAAG-
AE017355.1/2242962-2242862 AUGAACCAUU-CAGGAGAA-GGUC----------------UAUU-----------------------------------GAUC-UACCGACGGGGCAA-AAAGUUGUUAACC-----------------------GACU-------------------------UUGAAACUCUCAGGU--------CUUGUUUACAAG-
AL596168.1/161626-161717   GUGAAUGUAA-ACAGAGAGACUG-----------------UGAAA--------------------------------AG-CAG-CGCCGACGGGGAAA-GCAUAAG-----------------------------UUAU-------------------------GUGAAACUCUCAGGC---------------AAAAG-
BX640445.1/160210-160126   ACGUGCAGUU-CGGGAGAGACCGU----------------CCAGC--------------------------------GGACGG-CGCCGACGGAGCAA-CCA---------------------------------CCCC-------------------------GG-AAACUCUCAGGC---------------AAAAG-
BX640445.1/160122-160016   -----AACAU-CUGGAGAGUGGCGCGCG------------GUAC---------------------------------GGCGCC-CACCGAAGGGGAU--CCCUG-------------------------------GCGC-------GUUUGCAGCGGCGCACGGGUGAAGCUCUCAGGU---------------AAAUG-
D84432.1/169999-170100     AUGACAGCAA-GGGGAGAGACCUGACC-------------GAAAACCUCGGGA------------------------UACAGG-CGCCGAAGGAGCAA-ACU---------------------------------GCGG------------------------AGUGAAUCUCUCAGGC---------------AAAAG-
BX640439.1/206443-206535   ACGCAUGUCG-CGGGAGAGAGCGGCCG-------------AUUGC--------------------------------GGCUGC-CGCCGAAGGCGCAA-UUC---------------------------------GCCC-------------------------GG-AAUCGCUCAGGU--------------AACCCA-
AL591978.1/212840-212931   GUGAAUGUAA-GCAGAGAGACUGC----------------GAAAA----------------------------------GCAG-CGCCGACGGGGAAA-GCAUA-------------------------------UAUU-----------------------AUGUGAAACUCUCAGGC---------------AAAAG-
CR543861.1/1990167-1990077 AUGAUUAUUG-CAGGAGAGAUAUUCU--------------UGCAA--------------------------------AGGAUA-CGCCGAAGGAGCAA-CG----------------------------------ACCC-------------------------CGGAAACUCUCAGGC---------------AGAAG-
CR543861.1/1990073-1989965 -----AUAAU-CUGGAGAGAAGUAUU--------------UCAAA--------------------------------AAUACU-CACCGAAGGGGAUG-GUACG-------------------------------UAGA-----UUUAUGGAAAUCUAUAGCUACCGAAGCUCUCAGGU---------------ACCCU-
CR378670.1/15794-15904     -----AGCCU-CUGGAGAGACCCG----------------UUAAA---------------------------------UCGGG-CGCCGAAGGAGCAA-GCUUU-------------------------------CCUUUUUGCUGUUUUAACAUGCAUGGAAAGUGAAACUCUCAGGC---------------AAAAG-
AJ312125.1/453-315         AGACGAUACU-CUGGAGAGACCA-----------------UAUA------------------------------------AGG-CACCGAAGGAGCAA-AUUUAAUUGAGAUCUUUAUAUAAAUAAAAAAGCUCAUCCC----UUUUUUAGAUCAAGCGAUUAAAUGAAUCUCUCAGGU---------------AAAAG-
AJ312125.1/523-454         AUGAAGGUGG-CAGGAGAGACCC------------------AUGA---------------------------------G-GGG-CGCCGAAGAAGUAA----------------------------------------------------------------------AGCUUUCAGGC--------------U--UAG-
AL939123.1/278145-278052   UGAAUCCGCG-CGGGAGAGUCCCCGG---------------CCGCG-------------------------------CCGGGG-CGCCGAAGGAGCAA-GUCCC-------------------------------UCCC-------------------------UUGAAUCUCUCAGGC---------------ACCGU-
AL939123.1/278050-277936   -----CACAU-CUGAAAAGCGGACCGCC------------CCCGACGG-----------------------------CGGUCC-CACCCAAGGUGCAA-GCCCUGA-----------------------------UCGC-------CGUACUCCGGUGGCCGUGGCGAACCUCUCAGGU--------------UCCGAU-
AJ301559.2/6878-7012       UUCGACAACU-CUGGAAAGUGGUGGGA-------------GCACC----------------------------------CACC-CGCCCAAGGGGAAA-GGUGCCGGU---------------------------GCGC--GCAUGUCAGCGCGCCGUGUUCUACCGAAUCUCUCAGGCGCACGCGUCAGCGAGCACAC-
AJ301559.2/6784-6876       CGCCUGCGCG---GGAGAGUUCCGAGGC------------AUCCAGU------------------------------CUCGGA-CGCCGAAGGAGCAAUACCUC-------------------------------CCC--------------------------GUCAAUCUCUCAGGC---------------ACACG-
BX572605.1/160670-160756   CUAAGUCGCGUCGGGAGAGAUCGGCC--------------GCAA---------------------------------GGCCGG-CGCCGAAGGAGCAA-CCG---------------------------------CCCC-------------------------GG-AAACUCUCAGGC---------------AAACG-
BX572605.1/160757-160849   CGACUGACAU-CUGGAAAGAGACCCUGCCGGGC-------GAUCCCGGGA---------------------------CGGGUC-CGCCGACGGGAUAA----------------------------------------------------------------------UGCUCUCAGGC---------------ACAGC-
AE016822.1/1714518-1714420 GAGGCCGAUG-CGGGAGAGCUGCGGG--------------GGAGAACCCG---------------------------CCCGCGGCACCGAAGGAGCAA-UCCUC-------------------------------CCC--------------------------GACAAUCUCUCAGGU---------------ACGCG-
BX897699.1/1435970-1435876 -----UUUUG-CGGGAGAGUGCAGGC--------------UGCAAGUUUUUGG------------------------GUCUGC-CGCCGAAGGGGAAA-AUA---------------------------------GCCC-------------------------GU-AAUCUCUCAGGC------------UCU--AAG-
BX897699.1/1435871-1435783 -----CAGAU-CUGGAAAGUCGG-----------------GAGG---------------------------------GG-CCG-CGCCGAAGGUGUAA-GCGAA-------------------------------AACU-------------------UUUUUCGCGAGUCUCUCAGGU--------------U--UGU-
BX950851.1/2645129-2645034 UUGAAGCCAA-CUGGAGAGAGGUUGC--------------GAUGC----------------------------------AACC-CACCGAAGGGGCAA-GCAGC-------------------------------UCUG---------------------CUGCGU-AAACUCUCAGGU--------------AAAGCG-
BX950851.1/2645260-2645133 CCGCUCCUCG-CAGGAGAGAGGGCGUGUACUCCAGCAUACUUCAAGCUACAUGUACGUUGGCAUAAAGUAUA-----ACGCUC-CGCCGAAGGCGCAA-AC----------------------------------UCCC-------------------------AU-AAUCGCUCAGGC--------------UACCCU-
AE008691.1/313165-313055   AUGAAGAUAG-CGAGAGAUUAUCUUCC-------------AUAAAUG------------------------------GAAGAU-AGCCGAAGGGGAAA-UACAAAG-----------------------------GCCC-------------GCCAAGCCUUUGUAGAAGCUCUCAGGC---------------GGCAG-
AE008691.1/1826306-1826220 -----AUAUC-CCGGAAAG-CCUC----------------UAAA-----------------------------------GAGG-CACCGAAGGAGCAA-UUCUUCUAU---------------------------AAAG-------------------------AAGAAUCUCUCAGGU---------------AAACA-
AE008923.1/1392465-1392356 -----CAACU-CUGGAGAGACCGGCC--------------GAUG-----------------------------------CCGG-CGCCGAAGGGGCAC-GAAACGCAGGCAG-----------------------GCCA---------CGCGCCAGGCCGCGUUUUUAAACUCUCAGGC---------------AAAAG-
AL591688.1/1674990-1674906 CGACCUCGUU--GGGAGAAACCGG----------------UUCGA---------------------------------UCCGG-UGCCGAAGGAGCAA-CCG---------------------------------CCCC-------------------------GG-AAACUCUCAGGC---------------CAAAG-
AE014292.2/713320-713218   UAAGACAACU-CUGGAAAGUCGGGGG---------------CAAC----------------------------------UCCG-CGCCGAAGGUGUAA-GUAUGGCUUUAUAUAUA-------------------GCCA------------------------UGCGAGUCUCUCAGGC--------------C--UGA-
AE004439.1/116056-116172   -----AACCC-UUGGAGAGAGCCG----------------UUAUAUUAAAAAGAGAUAA------------------AACGGC-CGCCGAAGGCGCAA-AAAGA-------------------------------GCGG---------UUAAUUUUUCCGUUUUUUCAAACGCUCAGGC---------------AAAAG-
AE008691.1/1826408-1826312 AUGAAGAAUG-CGGGAGAGACCC-----------------UAACC-----------------------------------GGG-CGCCGAAGGAGCAA-GCGGGUAUAUGGCCUGUAU-----------------ACUC-------------------------GUGAAACUCUCAGGC---------------AAAAG-
BX842572.1/79202-79095     -----CAACU-CUGGAGACAGGGACG--------------GUCGCACCGACC-------------------------GUGCCU-GACCGAAGGUGUAGAGCGGC-------------------------------GCCA-------------UGAUGCGACGCCGC-AGACUCUCAGGU---------------UUCAG-
AE008922.1/1299977-1299896 GUAACACGGU--GGGAGAA-GCGGC---------------ACUG-----------------------------------CCGC-UGCCGAAGGCGCAA-CA----------------------------------GCCC--------------------------GUAAUCGCUCAGGC--------------C--CGA-
CP000919.1/381215-381303   GGACGGAACU-CUGGAGAGACC------------------GUAAA------------------------------------GG-CACCGAAGGGGCAA-GGCAG-------------------------------GCAA----------------------CUGCUCAAACUCUCAGGU---------------AAAAG-
CP000262.1/1070832-1070913 UGAUGUCAUG-CAGGAGA--AGAA----------------UUUA-----------------------------------UUUU-CGCCGAAGGAGUUA----------------------------------------------------------------------UACUCUCAGGU---GUUCAGUUUUUGAACGG-
#=GC SS_cons               :::::(((((.(((,,,,,,<<<<__.............._____................................__>>>>.,<<<<<--<<<---.<<___...............................____.........................>>---->>>>>->>>...............,,,,,.
#=GC RF                    auaaaccccu.CgGGAGAGacccgcg..............uuaaa................................agcggg.CGCCGAAGGaGcAA.gcaua...............................uCcc.........................gcgAAuCuCUCAGGC...............AaaaG.

AL766849.1/65640-65772     GACAGAAGCUAAAAG
AL766849.1/65560-65639     GACUGAUUGAC----
CR522870.1/1448610-1448703 GACUGCUAUGGGACG
CR522870.1/1448704-1448793 GACAGAGUGUAGCAG
BX842577.1/344356-344453   GACCGCGCGAGACUA
BX842577.1/344457-344587   GACAGAGGGAGAGGG
AL939108.1/255539-255444   UACCGCACGGACGAG
AL939108.1/255442-255325   GACAGAGGGGGAGGC
AE000516.2/79275-79185     CACCACACCGCCGAG
AE017355.1/2242861-2242742 GACAGAGACAAGCGA
AE017355.1/2242962-2242862 UA--GAACUGCAUGG
AL596168.1/161626-161717   GAUGUUUACGGGACG
BX640445.1/160210-160126   GACCGACCUGC----
BX640445.1/160122-160016   GACAGAUGGGGUUGC
D84432.1/169999-170100     AACUCUUGCUCGACG
BX640439.1/206443-206535   UACCGCGACUGCAUC
AL591978.1/212840-212931   GAUGUUUACGGGACG
CR543861.1/1990167-1990077 GACUGUAAUAAUCGA
CR543861.1/1990073-1989965 GACAGAUGGGGCAAC
CR378670.1/15794-15904     GACAGAGGAGAUAAG
AJ312125.1/453-315         GACAGAGAACUGAAU
AJ312125.1/523-454         GACUGUCAUCA----
AL939123.1/278145-278052   UACCGCGCGGGCGAG
AL939123.1/278050-277936   GACAGAUGGGGAGGA
AJ301559.2/6878-7012       GACAGAGGGGGAGGA
AJ301559.2/6784-6876       GAC---GCGUGUGGG
BX572605.1/160670-160756   GACCGCGCGGC----
BX572605.1/160757-160849   GACAGAUGGGGCUCG
AE016822.1/1714518-1714420 UACCGCAUCGGACUG
BX897699.1/1435970-1435876 GACCGUAAAAGAAGA
BX897699.1/1435871-1435783 AACAGAGGGGUGCAG
BX950851.1/2645129-2645034 GACAGAGGGAGUGGC
BX950851.1/2645260-2645133 AACUGCGAAUU----
AE008691.1/313165-313055   GAUCGCUAUCGGAUA
AE008691.1/1826306-1826220 GACGGGGGAAUAAAA
AE008923.1/1392465-1392356 GACAGAGGGGCGCGA
AL591688.1/1674990-1674906 GACC-AGCAAGGUG-
AE014292.2/713320-713218   GACAGAGGGGCACGA
AE004439.1/116056-116172   GACAGGGGCAACAAG
AE008691.1/1826408-1826312 GACCGCAUUC-----
BX842572.1/79202-79095     GACAGAGCGGGGAGG
AE008922.1/1299977-1299896 UACC-AUCUUCAACA
CP000919.1/381215-381303   GACAGAGCUAGGAUA
CP000262.1/1070832-1070913 GACUGUUUGAU----
#=GC SS_cons               ,,)))))))):::::
#=GC RF                    GACcGagggggaaag
//
```

Alignments __must contain__ the `#=GC SS_cons` line.


## Reactivity

Reactivities must be provided as [RNA Framework's XML files](https://rnaframework-docs.readthedocs.io/en/latest/rf-norm/#output-xml-files):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<data>
	<transcript id="RNA#1" length="&0">
		<sequence>
			GGAUGGGGAUCUAUCAGAUUCUGGCGAUCUACUGGACUGUCGCCAGUUCACUGGUGCUUU
		</sequence>
		<reactivity>
			0.296,0.283,4.681,4.500,0.134,0.020,0.015,0.017,0.014,0.036,0.036,0.071,0.058,0.060,0.059,0.015,0.017,0.029,0.316,0.246,0.045,0.063,0.102,0.137,0.072,0.030,0.022,0.026,0.057,0.130,0.105,0.099,0.189,0.165,0.133,0.033,0.101,0.093,0.054,0.062,0.080,0.255,0.118,0.226,0.009,0.057,0.196,0.315,0.123,0.149,0.037,0.026,0.016,0.029,0.048,0.077,0.065,0.087,0.073,0.176
		</reactivity>
	</transcript>
</data>
```


## Base-pair &amp; helix-level annotations

Base-pair annotations can be provided either as __[R-scape](https://github.com/EddyRivasLab/R-scape)__'s `.cov` files:

```
#
# Method Target_E-val [cov_min,cov_max] [FP | TP True Found | Sen PPV F] 
# GTp    0.1         [-9.95,80.38]     [0 | 15 22 15 | 68.18 100.00 81.08] 
#
#       left_pos       right_pos        score          E-value           pvalue       substitutions      power
#--------------------------------------------------------------------------------------------------------------
*	      23	      81	80.37853	2.15392e-12	9.79054e-14	32		0.78
*	      21	      83	72.12266	5.45655e-11	2.48025e-12	22		0.66
*	      13	     204	69.35723	1.60115e-10	7.27796e-12	15		0.51
*	      22	      82	60.77186	4.6225e-09	2.10114e-10	22		0.66
*	      10	     206	56.73722	2.24691e-08	1.02132e-09	15		0.51
*	      24	      80	53.88919	6.82812e-08	3.10369e-09	30		0.76
*	       8	     208	44.77264	2.35282e-06	1.06947e-07	28		0.74
*	     101	     165	42.50258	5.62836e-06	2.55834e-07	24		0.69
*	       9	     207	40.40155	1.26841e-05	5.76552e-07	33		0.79
*	     100	     166	40.00270	1.48045e-05	6.7293e-07	31		0.77
*	      86	     179	34.90543	0.000105498	4.79538e-06	15		0.51
*	      94	     172	23.67098	0.00699781	0.000318082	16		0.54
*	      12	     205	21.10188	0.0177879	0.000808543	7		0.24
*	       6	     210	17.99025	0.0503432	0.00228833	36		0.81
*	      14	     203	17.58020	0.0577269	0.00262395	4		0.10

```

or as TSV files:

```tsv
22	  80	  type#1
20	  82	  type#1
12	  203	  type#2
8	  206	  type#2
```

In TSV format, the first two fields correspond to `i` and `j` base-pair positions (0-based), while the third field (optional) represents the __group ID__, which, when present, is used to define different colors for the base-pair groups.

Currently, helix-level annotations can only be provided as R-scape's `.helixcov` files:

```
# RMs = 7 L = 237

# RM_HELIX NESTED 42-44 53-55, nbp = 3 nbp_cov = 2
# pvals: 0.283613,1.97783e-07,0.000149597
# aggregated LANCASTER        E-value: 8.07703e-09 P-value: 1.15386e-09 *
NESTED  ::::::::::::::::::::<<<______>>>::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
        :::::::::::::::::::::<<______>>:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

# RM_HELIX NESTED 14-20 65-70, nbp = 5 nbp_cov = 5
# pvals: 2.34551e-10,8.99662e-16,4.00831e-12,6.14824e-12,2.74706e-11
# aggregated LANCASTER        E-value: 6.02847e-50 P-value: 8.61209e-51 *
NESTED  ::::::::::::<<<<<_____________________>>>>>:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
        ::::::::::::<<<<<_____________________>>>>>:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

# RM_HELIX NESTED 71-83 147-165, nbp = 10 nbp_cov = 6
# pvals: 1.52662e-07,0.00961031,0.445125,0.445125,0.445125,6.56332e-10,3.48256e-10,1.55891e-16,4.47543e-19,3.29459e-12
# aggregated LANCASTER        E-value: 2.51331e-78 P-value: 3.59044e-79 *
NESTED  :::::::::::::::::::::::::::::::::::::::::::<<<<-<<<<<<___________>>>>-->>>>>>:::::::::::::::::::::::::::::::::::::
        :::::::::::::::::::::::::::::::::::::::::::<-----<<<<<___________>>>>-->---->:::::::::::::::::::::::::::::::::::::

# RM_HELIX NESTED 178-183 216-222, nbp = 6 nbp_cov = 6
# pvals: 5.07931e-10,3.26901e-21,6.3265e-23,5.49811e-26,6.45275e-15,1.3215e-08
# aggregated LANCASTER        E-value: 3.44693e-91 P-value: 4.92418e-92 *
NESTED  :::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::<<<<<<______>>>>>>:::::::::::
        :::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::<<<<<<______>>>>>>:::::::::::

# RM_HELIX NESTED 170-170 227-227, nbp = 1 nbp_cov = 1
# pvals: 1.72192e-09
# aggregated LANCASTER        E-value: 1.20534e-08 P-value: 1.72192e-09 *
NESTED  ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::<________________________>::::::::
        ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::<________________________>::::::::

# RM_HELIX NESTED 1-9 229-114, nbp = 8 nbp_cov = 6
# pvals: 8.97714e-05,1.75872e-06,4.14908e-08,0.00222791,1.23242e-05,0.310495,0.299138,1.54874e-05
# aggregated LANCASTER        E-value: 2.53491e-21 P-value: 3.62129e-22 *
NESTED  <<<<<<<<__________________________________________________________________________________________________>>>>>>>>
        <<<<<--<__________________________________________________________________________________________________>-->>>>>

# RM_HELIX PK 48-51 171-176, nbp = 4 nbp_cov = 4
# pvals: 3.05913e-07,2.8265e-11,0.000139183,6.80035e-05
# aggregated LANCASTER        E-value: 4.41785e-21 P-value: 6.31122e-22 *
PK      :::::::::::::::::::::::::<<<<____________________________________________________>>>>:::::::::::::::::::::::::::::
        :::::::::::::::::::::::::<<<<____________________________________________________>>>>:::::::::::::::::::::::::::::
```