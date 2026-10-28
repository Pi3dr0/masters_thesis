
### Biologicky zaklad: co vlastne nastroj hlada?
- Preco je [[CpG]] v genome relativne malo?
	- Biologicka motivacia clanku vychadza z metylacie Cytozinu. Metylacia Cytozinu, konkretne 5-metylcytozin, sa moze spontannou deaminaciou zmenit na tymin. Ak sa takato zmena neopravi a stabilizuje sa ako mutiacia, povodny CpG sa moze zmenit na TpG. Pocas evolucie tym klesa zastupenie CpG v genome. Clanok uvadza, ze v cicavcich genomoch je frekvencia CpG priblizne patinova oproti ocakavaniu zalezenemu na zastupeni jednotlovych baz.

- [[CpG ostrovceky]] su vy vynimkou z tohto vseobecneho ochudovnenia. Caso sa nachadzaju pri promotoroch a prvych exonoch, a preto moze pomahat pri identifikacii genov a regulacnych oblasti.
- CpG ostrovcek nie je to site, ako nemetylovana oblast.

- Pri interpretacii nastoja je preto zasande:
	- GC-Profile 2.0 predikuje [[CpG ostrovceky]] zo sekvencia DNA. Nemeria metylaciu a samotnou predikciou nedokazuje aktivitu genu
	- Jeho vstupnou informaciou je sekvencne zalozenie, nie experimentalny metylacny stav konkretneho tkaniva alebo bunky

### Ako sa definuje CpG Ostrovcek
- definicia v [[CpG ostrovceky]]
- Preco nestaci iba pocet [[CpG]]?
	- Ak sekvencia obsahuje vela C a G, urcity pocet [[CpG]] vznikne aj nahodne. Preto sa pozorovany pocet porovnava s ocakavanim pri nezavislom vyskyte baz.
	- L - dlzka sekvencie
	- $N_C$ - pocet Cytozinov
	- $N_G$ - pocet Guaninov
	- $N_\mathrm{CpG}$ - dinukleotidov [[CpG]]

$$
\mathrm{CpG}_{O/E} \approx \frac{N_{\mathrm{CpG}} L}{N_C N_G}
$$
- Ak by sme mali  L = 100, $N_C = N_G = 250$ a $N_{\mathrm{CpG}} = 50$ dostaneme:
$$
GC = 50\,\%, \qquad \mathrm{CpG}_{O/E} \approx 0{,}8
$$

### Informaticke jadro: rekurzivna segmentacia DNA
- Povodny GC-Profile analyzoval zmeny nukleotidoveho zlozenia. Nova verzia sustreduje segmentaciu na dve kategorie:
1. [[CpG]] denukleotidy
2. ostatne dinukleotidy
- Pre vysvetlenie si ich mozeme reprezentovat binarnym signalom:
$$
x_i =
\begin{cases}
1, & \text{Ak na pozicii } i \text{ zacina CpG, } \\
0, & \text{inak.}
\end{cases}
$$
- Uloha sa tym meni na hladanie intervalov, v ktorych sa meni frekvencia jednotiek
- Z pohladu CS je problem detekcie bodov zmeny: kde sa sekvencia rozdeluje na useky s odlisnou hustotou [[CpG]]?

- ==🔵**CpG order index**:
	- Autori zavadzaju index:
	- Kde *p* je frekvencia CpG a *1 - p* frekvencia ostatnych dinukleotidov. Ide o dvojkategoriovu verziu povodneho idnexu (vzorec pod):
$$
S(P) = p^2 + (1 - p)^2
$$
$$
a^2 + t^2 + c^2 + g^2
$$
	- Clanok ho pouziva na vyhodnotenie rozdielu medzi lavou a pravou castou sekvencie. Samotny index vsak nie je priamym skore "ostrovcekov". Je symetricky voci zamene *p* a *1 - p*. Jeho hlavnou ulohou v algoritme je pomoct identifikovat kompozicne hranice; biologicke kriteria sa uplatnuju osobitne

- ==🔵Ako algoritmus vyberie miesto rozdelenia?
	- Pre kanditatny bod rozdelenia sa vypocita
		- $p_l$: frekvencia CpG vlavo
		- $p_r$: frekvencia CpG vpravo
		- $w_l, w_r$ : relativne dlzky oboch casti
$$
\Delta S = w_l S(p_l) + w_r S(p_r) - S(w_l p_l + w_r p_r)
$$
	- Algoritmus zvoli miesto s najvacsou hodnotu $\Delta S$ a postupne opakuje na vzniknutnych podsekvenciach
	- Dosadime $P = (p, 1 - p)$ sa da odvodit:
$$
\Delta S = 2 w_l w_r (p_l-p_r)^2
$$
- ==🔵Podobnost s decision tree:
	- Gini impure binarnej distribucie:
$$
G(P) = 1 - [p^2 + (1-p)^2]
$$
	- Pokles tejto impure pri rozdeleni je algebraicky rovnaky ako uvedene $\Delta S$. Rozdiel je v ulohe: tu sa nerozdeluju vzorky podla features na zaklade znamych tried, ale jedna usporiadana sekvencia podla pozicie.
	- Metoda je teda blizsia rekurzivnej binarnej segmentacii nez supervised klasifikatoru.

- Windowless
	- Algoritmus nepotrebuje najpr zvolit pevnu velkost posuvneho okna, napriklad 200 alebo 500 bp. Hranice hlada priamo cez porovnavanie lavych a pravych podsekvancii. To odstranuje jednu dolezitu volbu, od ktrorej mozu zavisiet vysledky window metody.
	- Neznamena to vsak, ze je bez parametrov. Vysledok nadalej zavisi od minimalnej dlzky, GC obsahu, pomeru observed/expected a pripadneho maskovania repeticii. Navyse doplnkovy graf hustoty [[CpG]] uz pouziva posuvne okno velkosti 100bp.


- Implementacia zlozitosti:
	- 