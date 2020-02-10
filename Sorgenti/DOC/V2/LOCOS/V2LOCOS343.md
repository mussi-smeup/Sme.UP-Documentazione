
## Quality check-up
E' uno dei primi impieghi della check-list in ambito applicativo. Nello specifico, questo strumento viene utilizzato per la rilevazione dei dati di collaudo durante i vari controlli.
Per questo contesto sono stati predisposti diversi configuratori  specifici alternativi di partenza (ovvero alternative diverse di dati da cui partire per la compilazione dei rilievi) che si differenziano per il tipo di dati richiesti in input : 

**1) CQRICO_LO**
 :  : PAR L(TAB)
Lotto|Campo obbligatorio
Registrazione|Facoltativo e presente  solo se in tabella CRJ il flag _Solo un documento_ è blank
Tipo controllo|Facoltativo
Tipo ciclo|Facoltativo (presente solo se gestitoil parametro £Q1 del tipo lotto)

**2) CQRICO_OR**
 :  : PAR L(TAB)
Ordine di produzione|Obbligatorio
Lotto|Campo derivato in automatico dall'ordine di produzione
Registrazione|Facoltativo e presente  solo se in tabella CRJ il flag _Solo un documento_ è blank
Tipo controllo|Facoltativo
Tipo ciclo|Facoltativo (presente solo se gestito il **parametro £Q1** del tipo lotto :  si veda l'osservazione 2)

**3) CQRICO_RI**
 :  : PAR L(TAB)
Macchina|Obbligatorio
Lotto|Campo derivato in automatico dall'ordine di produzione
Registrazione|Facoltativo e presente  solo se in tabella CRJ il flag _Solo un documento_ è blank
Tipo controllo|Facoltativo
Tipo ciclo|Facoltativo (presente solo se gestitoil **parametro £Q1** del tipo lotto :  si veda l'osservazione 2)


_Alcune osservazioni : _
_1) Se le registrazioni dei rilievi vengono fatte tramite dispositivo mobile, è stata predisposta una tabella (B§M) che permette di associare il dispositivo (individuato da un codice che può essere la matricola dell'apparecchio) a una risorsa :  attraverso questa associazione diretta, il programma è in grado di dedurre in automatico quale ordine di produzione si trova in quel preciso momento sulla macchina e di conseguenza il lotto relativo.

_2) La scelta del tipo ciclo di collaudo ha senso nel momento in cui, nella definzione dei cicli di collaudo, si è deciso di associare a ogni articolo o famiglia, diverse tipologie di cicli di collaudo (elementi di CRJ). Questi legami vengono gestiti tramite il parametro standard A10 di categoria £Q1 legato al tipo lotto. Se quindi per un tipo lotto viene definito questo parametro multiplo, nella rispettiva cella Tipo ciclo troveremo esattamente i valori inseriti come parametri.

La scelta di un configuratore piuttosto che l'altro dipende esclusivamente dai dati che si hanno a disposizione nel momento in cui si stanno per eseguire i controlli. Una volta compilati i campi del configuratore, premendo invio o confermando con F6, si entra direttamente nel vivo del questionario che in questo caso coincide con le fasi del ciclo di collaudo che devono essere controllate. Le fasi del ciclo sono caricate nella parte di sinistra della scheda :  ogni fase compare in grassetto mentre le sue 4 caratteristiche compaiono immediatamente sotto. La presenza o meno del titolo in grassetto può essere pilotata dalla tabella B§Q così come anche il fatto che le 4 caratteristiche siano immediatamente visibili o no (flag T$B§Q4 :  si veda la documentazione di tabella).

**BOTTONI NOTE e HELP**
La scheda del questionario può cambiare notevolmente aspetto a seconda che vengano abilitate o meno le gestioni delle note e degli Help utili alla corretta compilazione del questionario. Sia le note che gli help possono essere gestiti a livello di : 
-  Questionario (oggetto LO)
-  Fase del ciclo di collaudo (Oggetto H1)
-  Caratteristica del ciclo (elemento di tabella CQK)
-  Singola domanda della caratteristica (può essere ancora lo stesso elemento della CQK o un altro oggetto se la caratteristica prevede la presenza di domande multiple; a tal proposito si veda sempre l'help della tabella CQK)
Questi bottoni compariranno in scheda solo se opportunamente attivati in tabella B§Q.
È tuttavia possibile introdurre altri bottoni (oltre a questi 8 potenziali) sempre attraverso il servizio CQSER_25 come già avviene pe i bottoni relativi alla carta X-R e alla gaussiana. Ovviamente tali bottoni appaiono solo per  le caratteristiche che prevedono una risposta di tipo numerico.

**COME AGGIUNGERE BOTTONI PERSONALI**
La struttura standard è stata pensata per permettere l'aggiunta di alcuni bottoni personalizzati (come per esempio un bottone per vedere la scheda del lotto,  per aprire direttamente una NC o per accedere ad altre informazioni).
Per poterli inserire occorre seguire la procedura : 
1) **Compilare in modo adeguato la tabella B§Q**. A questo proposito occorre indicare per il configuratore che si intende usare (CQRICO_LO, CQRICO_OR; CQRICO_RI) l'elemento della B£H in cui andremo a riportare tutte le nostre chiamate.
2) **Compilare in modo adeguato le tabelle B£H/B£Jss**. Ogni elemento che definiremo dovrà essere una funzione di Looc.UP del tipo  _F(EXD;\*SCO;) 1(LO;;&OG.K1) _ se l'obiettivo è agganciar el ascheda del lotto, oppure una J con il richiamo al CQLO01X se vogliamo far aprire una NC da bottone.
3) **Aggiungere in tabella B§Q il suffisso del programma di Exit** :  questo serve per poter intestare correttamente i bottoni del questionario (per esempio, sul bottone della scheda del lotto, far apparire il codice del lotto che si sta collaudando)
4) **Programma di exit** :  adeguare il programma di exit alle proprie necessita (partendo magari dal prototipo presente nello stadard).


## CONTROLLO PER VARIABILI E PER ATTRIBUTI
Come già sappiamo, i controlli possono essere divisi in due tipologie :  quelli per variabili e quelli per attributi. I primi sono di controlli che verificano delle grandezze numeriche, i secondi invece delle grandezze di tipo qualitativo. In entrambi i casi, si è provveduto a introdurre delle novità circa la gestione delle risposte. Nello specifico : 

**1. CONTROLLO PER VARIABILI : ** in tabella CQK è stato introdotto il flag _T$CQKD Tipo di forzatura del campione attraverso il quale è più o meno possibile autorizzare l'operatore a inserire i rilievi per un campione numericamente diverso da quello che è stato calcolato tramite il piano di campionamento. Questo flag assume una certa evidenza direttamente nella scheda del questionario dal momento che, in corrispondenza di rilievi numerici, appare una sezione dove compare, oltre alla dimensione del campione attesa, un campo relativo al campione che invece si intende dichiarare e il tipo di forzatura impostato in tabella (è il flag appena citato). Questi campi saranno opportunamente protetti in funzione del tipo di forzatura attivo per la caratteristica selezionata.
![LOA34_06](http://doc.smeup.com/immagini/MBDOC_OGG-V2LOCOS343/LOA34_06.png)**2. CONTROLLO PER ATTRIBUTI : **in tabella CQK è stato introdotto il flag _T$CQKB Risposte multiple attraverso il quale è possibile fare in modo che, per ciascuna delle 4 caratteristiche di una fase del ciclo di collaudo, sia possibile fornire più risposte. Questa possibilità è fruibile solo se si sceglie di registrare i rilievi in scheda e non attraverso la vecchia procedura in emulazione. Le risposte fornite vengono salvate come parametri della registrazione stessa (il file della registrazione prevede di gestire una sola risposta per caratteristica) secondo una logica di questo tipo : 

-  Tipo parametro :  H2
-  Codice 1 :  numero di registrazione che non deve essere confuso con il numero di documento (ricordiamo che l'oggetto H2 ha un doppio numeratore :  qui viene riportato esattamente il valore dell'oggetto H2)
-  Codice 2 :  numero della caratteristica (da 1 a 4) e domanda separati da /
-  Parametro :  1H2
-  Codice valore :  è la risposta fornita alla singola domanda
![LOA34_07](http://doc.smeup.com/immagini/MBDOC_OGG-V2LOCOS343/LOA34_07.png)Al momento la categoria di questi parametri è stata fissata a programma.
La consultazione di questi parametri può essere fatta tramite un preciso schema standard intitolato Q/DFTV (programma B£IQ2_H2 SMESRC/SMEDEV), attraverso i normali surf.



