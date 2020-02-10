
## Gli oggetti standard
## La tabella principale :  la B§Q

Per poter configurare correttamente una check-list, occorre compilare la tabella B§Q, nella quale si deve inserire l'elemento identificativo del questionario.
Un questionario infatti esiste se è stato codificato nella suddetta tabella.

 :  : DEC T(ST) K(B§Q)
![LOA34_04](http://doc.smeup.com/immagini/MBDOC_OGG-V2LOCOS342/LOA34_04.png)
L'elemento della tabella B§Q deve avere : 
**1)** Il nome del **configuratore** che serve per raccogliere i dati di input.
**2)** Il nome del **programma specifico** che serve all'estrazione e al caricamento dei capitoli, dei paragrafi e delle domande.
Nell'esempio della _Quality check-up_, il programma CQSER_25 si preoccupa di eseguire la ricerca e la scansione del ciclo di collaudo del lotto per determinare quali sono le fasi che devono essere dichiarate dagli operatori.

Impostati questi due campi, è possibile procedere con l'impostazione facoltativa degli altri : 
3) **Controllo accessi** :  serve per impedire che due o più utenti possano compilare lo stesso questionario contemporaneamente;
4) **Impostazione livelli** :  serve invece per impostare la modalità di visualizzazione del questionario, rendendo dinamica l'espansione dei capitoli e dei paragrafi. I capitoli possono comparire aperti (come in Figura 3) o chiusi in funzione di questo flag;
5) **Abilita informazioni a livello di questionario/capitolo/paragrafo/domanda** :  serve per definire le modalità di gestione delle note e dell' help ai vari livelli.
6) **Configurazione specifica** (in sviluppo) :  è una stringa di 20 caratteri che consente di influenzare la costruzione del questionario. A seconda del questionario e del programma specifico che si intende utilizzare, i 20 caratteri possono assumere significati diversi.
7) **Modello informativo** :  serve per determinare la gamma di colori da utilizzare nelle icone del questionario. Se il questionario è puramente informativo, i paragrafi le cui domande hanno ricevuto risposta, assumeranno un'icona di colore blu, segno che il paragrafo ha ricevuto una risposta. Se invece il questionario non è di natura informativa, le icone possono diventare verdi o rosse a seconda della conformità della risposta data a quella attesa.
8) **Refresh domande** :  determina un comportamento automatico di ricaricamento della videata a fronte di ogni risposta fornita;
9) **Posizionamento automatico capitolo** :  permette di avere un caricamento automatico della prima serie di domande alla quale si deve rispondere. Risposto a queste, il programma caricherà automaticamente la serie di domande relativa al paragrafo successivo.
10)**B£H per personalizzazioni** :  se compilato in modo opportuno (con l'aggancio alla B£J) è possibile inserire nella scheda delle personalizzaioni come chiamate a funzioni specifiche. Nello specifico, gli elementi del SS della B£J devono essere le funzioni da richiamare tramite opportuni bottoni dalla scheda.
11)**Suff. programma di aggiustamento** :  è la lettera che identifica il programma di exit utile per personalizzare ulteriormente le chiamate alle funzioni esplicitate nel SS della B£J.

Di tutte le voci elencate, quelle più importanti sono sicuramente quella del configuratore e quella del programma specifico. I richiami a questi due elementi (configuratore e programma) sono guidati da una scheda base (LOA34, SCP_SCH), la quale si preoccupa di richiedere attraverso un configuratore standard (LOA34, SCP_CFG) il nome del questionario e il relativo configuratore di input. All'interno di questa scheda, sarà poi il LOA34_SE (JASRC) a interfacciarsi con il programma specifico indicato in B§Q.
![LOA34_05](http://doc.smeup.com/immagini/MBDOC_OGG-V2LOCOS342/LOA34_05.png)
L'intero questionario viene elaborato quindi in un file di work che viene caricato dal LOA34_SE e gestito, nella scrittura, nell'aggiornamento, nella cancellazione nonché nella sua copia nel file_ definitivo_ dal programma specifico definito nella tabella B§Q, attraverso opportune chiamate : 

**A) Verifica e cancellazione del lock (chiamata con funzione LCK)**
Per poter limitare la compilazione del questionario su un oggetto a un singolo utente, è possibile attivare dei lock attraverso l'opportuno flag della tabella B§Q. Se attivata questa funzione, la generazione del lock viene pilotata dal programma di exit del configuratore specifico (exit del LOA08) che, attraverso la chiamata con funzione LCK.WRI al programma specifico, attiva il vincolo sul questionario che si intende compilare (frecce verdi dello schema). La rimozione di tale vincolo è invece guidato dal programma generico LOA34_SE che si preoccupa di rimuoverlo chiamando ancora il programma specifico (funzione LCK.DEL) prima della chiusura o abbandono del questionario stesso.

**B) Scrittura del questionario sul file di work (chiamata con funzione LIS)**
Attraverso questa chiamata da parte del LAO34_SE, il programma specifico si preoccupa di scrivere il file di work seguendo opportune logiche e regole di base che verranno spiegate in un'opportuna sezione.

**C) Scrittura delle risposte dal file di work al file definitivo (chiamata con funzione WRI)**
Attraverso questa chiamata il programma specifico si preoccupa di riportare nei file definitivi, tutte le risposte elaborate nel work durante la compilazione del questionario. Nel nostro caso il CQSER_25 si preoccupa di compilare i controlli di collaudo che sono stati eseguiti sul lotto.

**D) Controlli pre-aggiornamento (chiamata con funzione AFT)**
Può essere utile, durante la compilazione delle risposte, eseguire dei controlli specifici (valori compresi nei range, etc.). Attraverso questa chiamata, il programma specifico ha la possibilità di controllare le risposte date prima del loro salvataggio sul file di work. In questo modo è possibile respingere alcune risposte se queste non soddisfano dei criteri particolari definiti a livello di singola domanda.

**E) Aggiornamento (chiamata con funzione EXE)**
Nel caso in cui sia utile eseguire delle totalizzazioni da pubblicare nel titolo del questionario a fronte delle risposte date, è stata ideata questa chiamata che ha quindi lo scopo di aggiornare nuovamente alcuni campi del file di work secondo logiche o regole specifiche del questionario.



## I programmi, le schede e i configuratori standard
Le check-list utilizzano alcuni oggetti standard comuni che, interagendo con programmi specifici ed esxit, permettono di ottenere quanto esposto sopra.
**1) Il programma LOA34_SE (JASCR)** : 
Questo programma si preoccupa principalmente del caricamento e dell'aggiornamento del questionario in modalità provvisoria attraverso la lettura e l'aggiornamento del file di work. Oltre a questo però, il programma esegue : 
-  La costruzione di alcune sezioni della scheda LOA34, definendone in alcuni casi la dimensione e in altri il contenuto;
-  Il caricamento dei dati nelle varie sezioni;
-  L'aggiornamento delle risposte;
-  L'abbandono del questionario o la conferma delle risposte date e il relativo salvataggio globale.
**2) Il configuratore generale LOA34 (SCP_CFG) : **
Attraverso questo configuratore si procede alla scelta del tipo di questionario che si intende compilare. Nell'unico campo a disposizione, si deve quindi indicare l'elemento della tabella B§Q cui si riferisce il questionario specifico. A seconda di come viene configurata la chiamata a questo configuratore tramite la scheda LOA34, è possibile saltare questo passaggio e arrivare quindi direttamente al configuratore specifico del questionario (quello cioè indicato all'interno dell'elemento della tabella B§Q). Le possibili chiamate a questo configuratore sono : 
-  Chiamata con indicazione del questionario specifico :  F(EXD;\*SCO;) 1(TA;B§Q;CQRICO_LO) 2(MB;SCP_SCH;LOA34)
-  Chiamata senza indicazione del questionario specifico (e visualizzazione del configuratore LOA34) :  F(EXD;\*SCO;) 2(MB;SCP_SCH;LOA34)
**3) La scheda generale LOA34 (SCP_SCH) : **
È la scheda del questionario che si preoccupa di contenere le varie sezioni che abbiamo già avuto modo di vedere. All'interno di questa scheda, tutti i componenti sono caricati dall'unico servizio LOA34_SE :  non compare mai in modo esplicito un richiamo diretto ai programmi specifici (è infatti il LOA34_SE che guida le chiamate a questi programmi).

_BOTTONI NOTE e HELP_
La scheda del questionario può cambiare notevolmente aspetto a seconda che vengano abilitate o meno le gestioni delle note e degli Help utili alla corretta compilazione del questionario stesso. Sia le note che gli help possono essere gestiti a livello di : 
-  Questionario
-  Capitolo
-  Paragrafo
-  Singola domanda
Questi bottoni compariranno in scheda solo se opportunamente attivati in tabella B§Q.


## I programmi e i configuratori specifici standard
In questa famiglia rientrano tutti quei programmi che, in sintonia con il LOA34_SE, permettono la completa gestione del questionario. Parliamo di _famiglia di programmi_perché in realtà, oltre al programma specifico indicato in tabella B§Q, ne esiste almeno un altro che coincide con la exit del configuratore specifico (ovvero una exit del LOA08). È importante ricordare anche questo programma perché, in caso di gestione del lock sul questionario, l'attivazione del vincolo deve essere gestita proprio all'interno di questo programma in modo da impedire l'accesso alla scheda del questionario stesso in caso di vincolo già attivo.  Un esempio di quanto detto è il programma CQRICO_A08 che, attraverso la chiamata al programma specifico CQSER_25, gestisce il vincolo sulle dichiarazioni di collaudo dei lotti.


## Le exit personali
In questa famiglia rientrano tutti quei programmi che, in sintonia con il programma specifico standard, permettono la personalizzazione della scheda. La exit è quindi un programma che ha lo stesso nome del programma specifico standard con un suffisso finale costituito da __X_ (esempio :  CQSER_25_X), dove la X indica la lettera che deve essere specificata nell'apposito campo tabella B§Q. È stata poi prevista la possibilità di aggiungere dei bottoni personalizzati direttamente nelle tabelle B£H e B£J. Queste tabelle verranno scandite a partire dall'elemento di B£H inserito in B§Q e ogni elemento della B£J corrispondente verrà aggiunto dal programma specifico standard nella sezione dei bottoni personali. Le funzioni lanciate da questi bottoni possono essere aggiustate tramite la exit di cui sopra.



## La struttura del file di work
Il file di work che viene utilizzato per la gestione dei questionari è il B£WKXT0F.


 :  : PAR L(TAB)
BTTPK1|Costante definita dal programma specifico
BTKEY1|Numero del lavoro (£PDSJZ) + progressivo
BTRIG1|Numero di riga del questionario
BTCD01|Tipo e parametro della risposta. Le risposte che si possono fornire a una domanda devono essere di questa tipologia
BTCD02|Risposta fornita, scritta solo in update del file e da riportare poi sul file definitivo tramite il programma specifico.
BTCD03|Risposta attesa. Confrontata con il BTCD02, serve per determinare il colore dell'icona da attribuire al paragrafo (se il questionario non è di tipo informativo :  flag T£B§QA della tabella B§Q).
BTCD04|Valore di pre-aggiornamento alfabetico.
BTCD05|Riferimenti per recupero dell'help deai membridel DOC_VOC, da scrivere nella forma _VO;Membro VO; voce VO._
BTCD06|Campo usato per riportare il messaggio di errore da pubblicare nel caso di controlli specifici che hanno dato esito negativo. Il campo deve essere strutturato secondo la logica : _MSG-File;MSG-Code_ e quindi _BASxxxxMSGxx_
BTCD07|Variabile da usare nel messaggio di errore (MSG var)
BTCD08|_Libero_
BTCD09|_Libero_
BTCD10|_Libero_
BTCD11|_Libero_
BTCD12|_Libero_
BTCD13|_Libero_
BTCD14|Tipo informazione (C$TIPI)
BTCD15|Chaive 3 (C$KYC3)
BTCD16|Chiave 2 (C$KYC2)
BTCD17|Chiave 1 (C$KYC1)
BTCD18|Tipo contenuto note (C$TIPC)
BTCD19|Colore icona
BTCD20|Identificativo dell'oggetto relativo alla domanda
BTNR01|Lunghezza campo numerico
BTNR02|Numero di decimali della rispost anuemrica
BTNR03|Numero cid campi per oclonna (in caso si voglia impaginare diversamente le domande nell'input panel di dettaglio)
BTNR04|Campo in cui viene memorizzata l'ora in cui è stata data la risposta
BTDT01|Campo in cui viene memorizzata la data in cui è stata fornita la risposta
BTQT01|Limite inferiore considerato buono. In caso di risposte numeriche, questo campo definisce il limite inferiore dell'intervallo di accettabilità della risposta data)
BTQT02|Limite superiore considerato buono. In caso di risposte numeriche, questo campo definisce il limite superiore dell'intervallo di accettabilità della risposta data)
BTQT03|Risposta numerica fornita, scritta solo in update del file e da riportare poi sul file definitivo tramite il programma specifico. È la versione numerica del campo BTCD02.
BTQT04|Valore pre aggiornamento numerico
BTQT05|Valore per salvataggio valore numerico fuori range con forzatura. Se l'operatore conferma per due volte un valore numerico fuori range, la risposta viene comunque accettata.
BTFL01|Definisce la natura del record del file di work. Questo flag può assumere i seguenti significati :  0 = Record di testata; 1 = Record che identifica un capitolo; 2 = Record che identifica un paragrafo; 3 = Record di domanda (solo se multiple); 4 = Record di domanda da aggiungere anche ai paragrafi con risposte singole; 9 = record che identificano i bottoni specifici da aggiungere alla scheda nelle opportune sezioni
BTFL02|Tipo di domanda. Può assumere i seguenti valori :  \*blanks = Domanda singola (non prevede cioè domande con BTFL01='3'; al più può prevedere domande con BTFL01='4'), 1 = domanda multipla (ogni paragrafo con questo flag a '1' deve essere necessariamente seguito da record con BTFL01='3')
BTFL03|Risposta data. Può assumere i seguenti valori :  \*blanks = nessuna risposta fornita, 1 = risposta fornita, 2 = risposta impostata di default (forzata)
BTFL04|Se '1' indica che il record è in aggiornamento
BTFL05|Stato del capitolo per visualizzazione dinamica del questionario. Può assumere i seguenti valori :  A = Aperto, C = Chiuso, F = Fisso (non espandibile tramite dinamismi), H = Nascosto
BTFL06|Caratterizzazione della risposta per ciascuna domanda. Una domanda può avere una risposta :  O = obbligatoria, 2 = protetta, ovvero non modificabile, 3 = non visibile (in questo caso non si vede neanche la domanda)
BTFL07|Calcolo valori statistici relativi alle domande. In caso di paragrafi con domande numeriche, è possibile eseguire un calcolo immediato dei principali indicatori aritmetici della serie numerica fornita come risposta. Tali valori possono essere visualizzati in una delle labe della scheda LOA34 attraverso l'opportuno aggiornamento del campo del file di work.
BTFL08|Indica se devono essere aggiunti dei bottoni specifici. I valori gestiti sono :  \*blanks = nessun bottone specifico, 1= bottone a livello di paragrafo, 2= Bottone a livello di questionario












