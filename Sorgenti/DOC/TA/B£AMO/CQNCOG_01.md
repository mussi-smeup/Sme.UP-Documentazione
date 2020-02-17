# Scopo
 \* Gestione delle Non Conformità rilevate in fase di collaudo, produzione, post-vendita con apposite funzioni semplificate
 \* Classificazione delle Non Conformità
 \* Possibilità di indicare Quantità di scarto/rilavorazione selezione/deroga e Costi dei materiali, di lavorazione interna, esterna e macchina, in modo manuale e/o automatico.
 \* Stampa dei rapporti di non conformità
 \* Gestione delle attività per non conformità ricorrenti

# Tabelle utilizzate dal modulo : 
### CQY - TIPO GRIGLIA  CONTROLLI
Descrive il significato dei campi legati alla griglia. Collegare questi campi alle tabelle o ad archivi dati.
 :  : DEC T(ST) K(CQ§)

### CQB - Esito Lotto
identifica l'esito del collaudo al seguito della gestione della non conformità
 :  : DEC T(ST) K(CQB)

### CQC - Cause Difetti
Classifica le cause del difetto a fini statistici
 :  : DEC T(ST) K(CQC)

### CQD - Difetti
Raccogliere e codificare le difettosità rilevate. Associa ad ogni difetto una classe del difetto ed una  gravità che differenzia a parità di difetto, la gravità che questi assume nell'ambito del prodotto in esame.
 :  : DEC T(ST) K(CQD)

### CQE - Caratterizzazione della non conformità
Codifica le azioni intraprese a seguito di non xxnformità. Determina con i suoi campi : 
 - Il tipo costo a cui il programma si deve riferire nel collegamento con la 'Gestione Costì del Gestionale per la valorizzazione del particolare oggetto della non conformità.
 - Il tipo calcolo costo che permette di differenziare la valorizzazione del particolare non conforme in funzione della caratterizzazione della Non Conformità. Tale valorizzazione viene proposta in automatico nel campo 'Costo Unitario' della finestra 'Costì della 'Gestione delle Non Conformità'.
 - La forzatura nell'esito dei controlli
 :  : DEC T(ST) K(CQE)

### CQF Classi difetto
Stabilisce in funzione della classe di difetto il valore di demerito o parametro di danneggiamento che influenza l'indice di qualità del lotto.
 :  : DEC T(ST) K(CQF)

### CQN - Accertamento causa difetto
Individua a fronte di una causa difetto il grado di veridicità.
 :  : DEC T(ST) K(CQN)

### CQX - Stato dell'addebito/accredito
Classificare gli stati in cui si può trovare un'azione di accredito/addebito avviata a seguito della rilevazione di una non conformità
 :  : DEC T(ST) K(CQX)

### CNTT - Codici oggetti applicativi
Descrive il tipo di enti che gestiscono l'immissione delle non conformità, la     gestione della richiesta di intervento, ecc...
 :  : DEC T(ST) K(\*CNTT)

### CQ\*AD - Segno movimento addebito accredito
Codifica il tipo di addebito/accredito.
 :  : DEC T(ST) K(CQ\*AD)

### B£Y- Gruppo Flag
Codifica il gruppo flag. La sua compilazione è fondamentale e stabilisce tra le altre la configurazione della parte quantità/valori/date e le modalità di trattamento logistico e amministrativo della non conformità.
Per il dettaglio si rimanda alla documentazione flag.
 :  : DEC T(ST) K(B£Y)

# Processo di avviamento ed utilizzo
## Attività iniziale
 \* Classificazione Difetti
 \* Classificazione Cause difetti
 \* Classificazione Gravità difetto
 \* Classificazione Accertamento Causa
 \* Classificazione Tipo di non Conformità
 \* Classificazione Stato di Addebito Accredito
 \* Classificazione Tipo di Addebito Accredito
 \* Classificazione gruppo flag
 \* Inserimento tabelle

## Attività periodica
 \* Inserimento Non Conformità rilevate al collaudo
 \* Emissione richieste di deroga, azioni correttive, ecc..
 \* Gestione non conformità, addebito o accredito spese, dichiarazione quantità, ecc..
 \* Stampa osservazioni di collaudo

## Aspetti amministrativi
Nel caso di NC fornitore è possibile interagire con la contabilità per bloccare il pagamento della fattura.
Vedi utilizzo dei flag 18-19-20 del file CQNCOG0F e le tabelle contabili : 

 :  : DEC T(ST) K(C56)
 :  : DEC T(ST) K(C6N)

# Gestione Non Conformità (flusso funzionale)
![CQ_NCNF_01](https://doc.smeup.com/immagini/CQNCOG_01/CQ_NCNF_01.png)x
