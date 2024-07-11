# Supporto Integrazione FSE
In questo repository sono definite le linee guida per l'interoperabilità con il middleware regionale
per il Fascicolo Sanitario Elettronico.

Il Middleware Regionale espone delle API basate su architettura REST.

Le API sono strutturate tramite URL orientati alle risorse, ritornano risorse in formato JSON e usano i codici di risposta e i metodi secondo standard HTTP.

Le linee guida per l'integrazione seguono quelle definite a livello nazionale per FSE 2.0.

## FSE 1.0
L'attuale versione del Fascicolo Sanitario Elettronico.

Le linee guida per l'interoperabilità riprendono quelle definite in FSE 2.0 in modo da allineare e rendere
più semplice il processo di integrazione.

## FSE 2.0
La nuova versione del Fascicolo Sanitario Elettronico.

Il middleware regionale segue le linee guida definite dal [Gateway Nazionale](https://github.com/ministero-salute/it-fse-support/tree/main/doc/integrazione-gateway).

## Risorse
* [Open API](./openapi)

## Limitazioni
Di seguito vengono elencate le limitazioni tecniche presenti.

* **[AuthN]** _Certificati_ - Manca la gestione dei certificati (creazione, rinnovo) per la firma dei token e per MTLS. Siamo in attesa di chiarimenti delle specifiche nazionali.
* **[FSE1]** _Aggiornamento Metadati_ - Non funziona correttamente, siamo in attesa di chiarimenti delle specifiche nazionali.
* **[FSE1]** _Cancellazione Metadati_ - Non funziona correttamente, siamo in attesa di chiarimenti delle specifiche nazionali.
* **[FSE2]** _Cancellazione Metadati_ - Non funziona correttamente, siamo in attesa di chiarimenti delle specifiche nazionali.

## SERVIZIO DI FIRMA REMOTA
Regione Umbria mette a disposizione delle aziende sanitarie pubbliche e dei MMG/PLS convenzionati un servizio di firma remota via web service SOAP.

Per la firma di documenti da inviare ad FSE è obbligatorio l'utilizzo della firma PAdES.

La firma remota è disponibile in due diverse modalità:
* **[FirmaOTP]**: per apporre la firma è necessario inserire il codice OTP generato da app mobile o da dispositivo fisico
* **[FirmaAutomatica]**: per apporre la firma non è necessario inserire il codice OTP. Questo tipo di firma è normalmente utilizzato per la firma dei referti di laboratorio e/o in altre situazioni in cui è necessario procedere alla firma "massiva" di documenti
Il tipo di firma da utilizzare viene concordato con ciascun fornitore prima dell'avvio delle attività.

Il servizio è fornito da Aruba e queste sono le [specifiche di integrazione](/firma/manuale_arss.pdf). Sono inoltre disponibili gli esempi, gli endpoint di test e le credenziali di test per i servizi:
* [Firma OTP](/firma/FirmaRemota.pdf)
* [Firma Automatica](/firma/FirmaAutomatica.pdf)

Gli esempi relativi alla firma PAdES sono indicati con *pdfsignatureV2*.

Per il servizio di firma OTP, oltre alla firma del singolo documento tramite il servizio *pdfsignaturev2*, è possibile procedere alla firma in sequenza di più documenti utilizzando un solo codice OTP; per effettuare questa operazione è necessario eseguire le seguenti operazioni:
1. Apertura sessione utilizzando credenziali ed OTP tramite il servizio *opensession* che restituisce l'id sessione
2. Esecuzione in sequenza di più firme invocando più volte il servizio *pdfsignaturev2* utilizzando l'id sessione ottenuto al punto 1
3. Chiusura sessione tramite il servizio *closesession* utilizzando l'id sessione ottenuto al punto 1
