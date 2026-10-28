- **CpG ostrovceky** je dlhsi usek DNA v vysokym obsahom **G** a **C **s relativne vysokym zastupeim** [[CpG]] **dinukleotidov

- GC obsah opisuje, kolko nukleotidov je G alebo C
- CpG hustota opisuje, ako casto po C bezprostredne nasleduje G

- sekvencie s rovnakym GC obsahom preto nemusia mat rovnaky pocet CpG. Napriklad `CCCCGGGG` a `CGCGCGCG` obsahuje iba C a G, ale prva ma jeden CpG a druha 4.

- ==🟠Mozeme ich definovat nasledovne
	- **Dlzka** - aspon 200bp
	- **GC obsah** - aspon 50%
	- **Pomer pozorovanych a ocakavanych [[CpG]]** - aspon 0.6

- ==🔵Mozne pouzit aj prisnejsiu definiciu:
	- **Dlzka** - minimalne 500bp
	- **GC obsah** - aspon 55%
	- **pomer CpG** - aspon 0.65

- Su to najma regulacne znacky: typicky lezia pri starte genu a pomahaju urcit, ci sa gen bude transkribovat

- Aku ulohu hraju:
	- Casto sa nachadzaju v [[promotor]]. Ich metylacia (pridanie metylovej skupiny na cytozin) moze znizovat alebo uplne vypnut [[expresia genu]]

- `Nemetylovany` = Promotor je pristupnejsi, gen sa casto transkibuje
- `Metylovany` = Moze dojst k represii/silencovanie genu
- napr.: abnormalna metylacia pri BRCA1 ci MLH1 suvisi s rakovinou

- Ako pomahaju najst geny
	- Uzitocne ako **genomicke orientacne body**
	- Ak v sekvencii najdeme CpG ostrovcek, je pravdepodobne, ze sa v okoli nachadza zaciatok genu, [[promotor]] alebo prvy [[exon]].
	- Studia ludskych genov zistila, ze identifikovane CpG ostrovceky boli takmer vsetky asociovane s genmi a vacsina prekryvala aspon cast [[exon]] (https://www.ensembl.org/help/articles/non-vertebrate-genome-annotation)

- Pomahaju najst:
	- Oznacia kadidatny [[promotor]] a transkipcny start (TSS)
	- Casto sa prekryvaju s 5'UTR alebo prvym [[exon]], takze naznacia, kde hladat zaciatok genovej struktruy
	- Po najdeni kadidatneho genu sa [[exon]] urcuje hlavne z inych dokazov: zarovnanie RNA-seq readov, cDNA/EST, splice-site motivy a predikcia otvoreneho citacieho ramca