Questo documento contiene le informazioni necessarie per creare un nuovo ambiente sui server del laboratorio di sviluppo.

- Decidere la sigla dell'ambiente (di 3 lettere, ad esempio XYZ)
- Creare la libreria UP_XYZ copiandola dalla libreria SMEUP_FIL
- Creare la libreria PER_XYZ (o XPER_XYZ in base al fatto che la si voglia salvare o meno) copiandola dalla libreria SME_XXX
- Rivolgersi al responsabile sistemistico per la creazione (ove necessaria) degli utenti "utilizzatori". Tali utenti andranno creati con la codifica XYZ_nn (con nn progressivo) come copia dall'utente XXX_01
-- Questi utenti sono indispensabili in caso ci siano persone esterne con la necessità di collegarsi a tale ambiente
- Mediante il comando UP UT5 è poi necessario : 
-- Definire la lista librerie dell'ambiente appena creato (opzione 2)
-- Associare il nuovo ambiente agli utenti interessati (opzione 1)
- Tutti gli eventuali oggetti sistemistici che verranno creati (code lavori, stampanti ecc.) dovranno comunque avere la codifica XYZ_xxx
- Aggiungere l'utente o gli utenti nella B£U del nuovo ambiente

Alcuni documenti utili : 
- [Lab. Sviluppo - Nomenclatura librer](Sorgenti/DOC/TA/B£AMO/A£BASE_01E)
- [Gestione applicazioni utente](Sorgenti/DOC/OJ/PGM/B£UT55)



