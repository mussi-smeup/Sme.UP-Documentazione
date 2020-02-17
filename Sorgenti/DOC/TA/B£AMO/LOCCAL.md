# Componente CAL

- [Abstract](Sorgenti/DOC/TA/B£AMO/LOCCAL_F00)

## Funzionalità
- [Modalita' di visualizzazione](Sorgenti/DOC/TA/B£AMO/LOCCAL_F01)
- [Personalizzazione eventi](Sorgenti/DOC/TA/B£AMO/LOCCAL_F02)
- [Dinamismi](Sorgenti/DOC/TA/B£AMO/LOCCAL_F03)

## Eventi gestiti
Il componente gestisce i seguenti eventi : 
- Click :  L'evento scatta al click sull'evento in un giorno
- Dateselect :  L'evento scatta al click su un giorno senza evento
- Drop :  L'evento scatta al drop di un evento da un giorno ad un altro

![LOCCAL_01](https://doc.smeup.com/immagini/LOCCAL/LOCCAL_01.png)
![LOCCAL_02](https://doc.smeup.com/immagini/LOCCAL/LOCCAL_02.png)
![LOCCAL_03](https://doc.smeup.com/immagini/LOCCAL/LOCCAL_03.png)
![LOCCAL_04](https://doc.smeup.com/immagini/LOCCAL/LOCCAL_04.png)
![LOCCAL_05](https://doc.smeup.com/immagini/LOCCAL/LOCCAL_05.png)
 XXG.SUB.CAL Tit="Calendario" Id="cal"

 XXG.SET.CAL DatCol="V£DATA" TitCol="AGEDES" Drag="Yes" IcoCol="AGEICO"

 XXG.DIN When="Click" Where="..."
- Click  :  al click sull'evento in un giorno
XXFIG M(LOCCAL) P(LOCCAL_06)

 XXG.DIN When="Dateselect" Where="..."
- Dateselect :  al click su un giorno senza evento
XXFIG M(LOCCAL) P(LOCCAL_07)

 XXG.DIN When="Drop" Where="..."
- Drop  :  al drop di un evento da un giorno ad un altro
XXFIG M(LOCCAL) P(LOCCAL_08)


- CAL.DAT - Data selezionata
- CAL.INI - Data inizio
- CAL.FIN - Data fine
FROM.T1 - T1 al Drag
FROM.P1 - P1 al Drag
FROM.K1 - K1 al Drag
TO.T1 - T1 al Drop
TO.P1 - P1 al Drop
TO.K1 - K1 al Drop

## Schede di esempio
Gli esempi del componente cal sono consultabili tramite due sezioni differenti : 
- una sezione generale, che contiene esempi validi per Looc.UP e per Web.UP,
- una sezione più specifica per il web.

 :  : DEC K(Esempi) D(Sezione generale) X(F(EXD;\*SCO;) 1(V2;JAGRA;CAL) 2(MB;SCP_SCH;J1GRA) 4(;;ESE)) L(1)
 :  : DEC K(Esempi) D(Sezione specifica per il web) X(F(EXD;\*SCO;) 1(V2;JAGRA;CAL) 2(MB;SCP_SCH;WETEST_CAL)) L(1)
