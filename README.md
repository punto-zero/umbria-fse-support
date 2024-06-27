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
