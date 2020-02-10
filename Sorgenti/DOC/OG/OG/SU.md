## Definizione.

Chiamiamo UPP l'insieme di tutti gli oggetti che nell'ecosistema applicativo di Sme.UP sono utili alla soluzione di un tema applicativo. Come per le APP avremo un nome, una icona, ecc.
L'obiettivo all'interno del sistema Sme.UP è quello di favorire la collaborazione di più persone con competenze diverse per raggiungere un obiettivo applicativo che possa anche essere un oggetto commerciale.

In Sme.UP l'oggetto SU, viene spesso indicato anche con lo termine "upp".

## Codifica

Un'istanza di upp ha un codice strutturato in modo significativo. E' infatti sempre definito nel seguente modo : 
-  Due caratteri che definiscono l'applicazione di appartenenza
-  Un underscore
-  3 caratteri alfanumerici univoci :  questi caratteri da soli identificano già di per se in modo univoco la "upp" e verrano come vedremo a seguire usati anche in tale accezione.

Avremo quindi codici simili a questi : 
-  A£_001
-  C5_002

E' importante rimarcare nuovamente che gli ultimi 3 caratteri sono univoci di per loro e che quindi non esisterà mai un upp C5_001, in quanto il codice 001 è stato già usato dall'upp A£_001.

I caratteri univoci possono essere sia numerici che alfa e non hanno un significato particolare, se non che il carattere inziale X :  esso infatti identifica il fatto che la upp è un upp custom di un cliente non un upp standard.

Esiste poi la UPP personale che esiste solo nella libreria W_utente che ha codice fisso A£_USR.

## Struttura Tecnica

Fisicamente l'upp esiste per effetto dell'esistenza di un membro del file SCP_UPP avente il medesimo codice.

Al fine di non incorrere in sovrapposizioni del codice univoco è fortemente consigliato di non operare direttamente sui membri ma di passare sempre dall'interfaccia grafica dell'oggetto SU che si occupa, fra le altre cose, di determinare il codice univoco.

## Dati collegati

Questa particolare codifica permette di definire un alto nmero di informazioni di informazioni riferibili ad una particolare UPP attraverso il riferimento al codice completo o al solo codice univoco (es. la scheda A£_000 e lo script SCP_SET/LOA37_000, sono entrambi riferiti in modo preciso all'UP A£_000).

Tali dati sono gestibili attraverso la voce "gestione copertura funzionale" sotto il titolo "sviluppare" del menù completo.

Chi fa gli sviluppi dovrebbe operare solo sugli oggetti che si chiamano come l'UPP, se deve fare qualcosa su altri oggetti/sorgenti, deve vedere con il laboratorio, ma questi non sono riconosciuti come sviluppi che appartengono direttamente UPP.

## Responsabile e Collaboratori

L'upp ha un responsabile intestatario e può avere una serie di collaboratori. Il responsabile è abilitato alla modifica di tutti i sorgenti, mentre i collaboratori sono abilitati ai sorgenti in funzione della responsabilità che gli viene attribuita. Se un utente non è ne responsabile ne collaboratore, non può fare alcuna modifica ai sorgenti.
Sia il responsabile che i collaboratori sono indicati nello script SCP_UPP (istruzioni UPP.ANA e UPP.COL).

I collaboratori possono assumere i seguenti ruoli : 
-  GEN Assistente Generale :  ha le stesse autorizzazioni del responsabile
-  TEC Assistente Tecnico :  può modificare script, programmi e tabelle
-  APP Assistente Applicativo :  può modificare gli script e le tabelle
-  DOC Responsabile Documentazione :  può modificare la documentazione
-  FOR Responsabile Formazione :  può modificare la documentazione
-  TST Responsabile Test :  non ha autorizzazioni particolari
-  RES Responsabile Informazione :  non ha autorizzazioni particolari

## Variabili da script

All'interno dello script SCP_UPP (istruzione UPP.VAR) è inoltre possibile fissare alcune variabili che possono essere poi essere prese in considerazione quando la UPP deve essere utilizzata nel sistema. Le variabili possono essere fruite nei programmi attraverso l'api £K45. Quando i valori di tali variabili vogliono essere personalizzati, lo script SCP_UPP, va spostato nella propria libreria di personalizzazione.

Le variabili da script ed il configuratore con sezione 0 (descritto a seguire) generano le variabili _&_KU.upp%codice, dove upp è il codice inteero della UPP e codice è il codice attribuito alla variabile nello script SCP_UPP o nello script di configurazione SCP_CFG.

Es. la variabile dello script di configurazione della UPP A£_000, avente codice D01, può essere impiegata in tutti gli altri script tramite la codifica _&_KU.A£_000%D01.

## Principali sorgenti collegati

Vediamo brevemente in rassegna alcuni dei principali sorgenti che è possibile abilitare sull'upp : 

-  Per l'utilizzo
- \* **Scheda** :  è possibile abilitare una scheda intestata all'upp. Naturalmente nulla vieta, applicando delle desinenze di creare più di una scheda collegata all'upp.
- \* **Servizi** :  è possibile abilitare uno o più servizi intestati all'upp, applicando una desinenza _nn al codice dell'UPP.
- \* **Configuratore** : E' uno script che permette la definizione di uno o più questionari che potranno essere utilizzati nel seguente modo : 
- \*\* definire sia richieste parametri da usare nell'UPP, tramite le istruzioni di scheda G.SUB.UCF/G.SET.UCF
- \*\* definire dei parametri di setup che potrammo essere poi usati nei programmi e negli script per condizionare il comportamento dell'UPP. Questo si ottiene implementando un particolare configuratore con codice upp/0. I dati qui descritti saranno poi reperibili tramite l'API £K45 nei programmi e tramite le variabili _&_KU negli script (è l'equivalente di una tabella xxn codice - , calata nella dimensione della singola UPP).
- \* Nel configuratore può essere impiegata una exit che permette di applicare logiche particolari di controllo e/o completamento che lo script del configuratore non permette di implementare.
- \* **Script di menù** :  permette di descrivere un elenco di funzioni da presentare come menù nell'impiego dell'UPP.
- \* **File** :  è possibile definire un file di database con i corrispondenti logici
- \* **Valori fissi** :  qualora sia necessario definire delle tabelle descrittive, sarà possibile farlo attraverso questo script.
- \* **Workflow** :  permette definire eventuali processi di workflow da impiegare nell'UPP.
- \* **Layout** :  qualora si impieghino input panel o box nell'upp, tramite questi script sarà possibile definirne il layout grafico
- \* **Report come pdf** :  tramite questo script sarà possibile definire dei layout di stampa
- \* **Costruttori** :  sono funzionalità complesse di carattere generale, che possono essere impiegate in diversi ambiti applicativi.

-  Per la formazione
- \* **Documentazione scheda** :  documentazione che descrive il funzionamento operativo della scheda intestataria
- \* **Scheda di Cruscotto** :  è possibile abilitare una scheda fatta per illustare le funzionalità dell'UPP
- \* **Glossario** :  permette di descrivere il significato di un elenco di termini la cui conoscenza è necessario per l'utilizzo dell'UPP.
- \* **Training** :  permette di descrivere una serie di passi da far eseguire al lettore, atti a consentire l'autoapprendimento
- \* **Corsi** :  descrive la scaletta del corso (qualora si previsto) di descrizione dell'UPP
- \* **Video** :  permette di settare il link ad un video che descrive l'UPP
- \* **FAQ** :  definisce le FAQ relative all'utilizzo dell'UPP.
- \* **Messaggi** :  permette di definire una serie di messaggi testuali che possono poi essere impiegati nell'utilizzo dell'UPP.
- \* **Figure Documentazione** :  permette di definire le immagini che potranno poi essere utilizzate nella documentazione

-  Per lo sviluppo
- \* **Prototipi** :  tramite gli script di prototipo è possibile costruire degli output grafici a partire da una semplice definizione di script. Questi prototipi permettono quindi di produrre dati prototipali, prima che siano sviluppati programmi che si occuperanno delle logiche complesse.
- \* **Scheda di Test** :  è possibile abilitare una scheda in cui verrà concentrata la possibilità di effettuare i test delle funzionalità dell'UPP
- \* **Scheda Esempi** :  ha una funzionalità simile alla precedente con la differenza che mentre la precedente lascia le scelte da effettuare libere, in questa le scelte vengono prefissate al fine di porre in evidenza alcune combinazioni significative per la verifica ed il test delle funzionalità dell'Upp.

-  Per la distribuzione
- \* **Documentazione applicativa** :   documentazione che descrive i passi di attivazione ed i prerequisti per il funzionamento dell'UPP.
- \* **Oggetti aggiuntivi** :  permette di definire gli oggetti impiegati nell'utilizzo dell'upp ma di cui l'upp non ne è proprietaria
- \* **Script di distribuzione** :  permetterà di definire istruzioni, prerequisiti ed elenco di sorgenti, necessari per installare l'upp in un ambiente in cui non è già installata.






