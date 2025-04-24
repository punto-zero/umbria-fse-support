# Supporto Integrazione FSE
In questo repository sono definite le linee guida per l'interoperabilità con il middleware regionale
per il Fascicolo Sanitario Elettronico.

## REST API
* [Open API](./openapi)
* [Documentazione](https://github.com/punto-zero/umbria-fse-support/wiki/Documentazione-REST-API)

## Servizio di Firma Remota

> [!NOTE]
>
> Endpoint Test SOAP: https://arss.demo.firma-automatica.it/ArubaSignService/ArubaSignService
> 
> Endpoint Produzione SOAP: https://puntozero.enterpriseatp.cloud/ArubaSignService/ArubaSignService
>
> Endpoint Test REST: https://arss.demo.firma-automatica.it/ArubaSignService/rest/ArubaSignService/pdfsignatureV2
> 
> Endpoint Produzione REST: https://puntozero.enterpriseatp.cloud/ArubaSignService/rest/ArubaSignService/pdfsignatureV2

Regione Umbria mette a disposizione delle aziende sanitarie pubbliche e dei MMG/PLS convenzionati un servizio di firma remota via web service SOAP e REST.

Per la firma di documenti da inviare ad FSE è obbligatorio l'utilizzo della firma PAdES.

La firma remota è disponibile in due diverse modalità:
* **[FirmaOTP]**: per apporre la firma è necessario inserire il codice OTP generato da app mobile o da dispositivo fisico
* **[FirmaAutomatica]**: per apporre la firma non è necessario inserire il codice OTP. Questo tipo di firma è normalmente utilizzato per la firma dei referti di laboratorio e/o in altre situazioni in cui è necessario procedere alla firma "massiva" di documenti
Il tipo di firma da utilizzare viene concordato con ciascun fornitore prima dell'avvio delle attività.

Il servizio è fornito da Aruba:
* [Specifiche di integrazione](/firma/manuale_arss.pdf)

Sono inoltre disponibili gli esempi, gli endpoint di test e le credenziali di test per i servizi:
* [Firma OTP (SOAP)](/firma/FirmaRemota.pdf)
* [Firma Automatica (SOAP)](/firma/FirmaAutomatica.pdf)
* [Firma OTP (REST)](/firma/FirmaRemota_REST.pdf)
* [Firma Automatica (REST)](/firma/FirmaAutomatica_REST.pdf)

Gli esempi relativi alla firma PAdES sono indicati con *pdfsignatureV2*.

Per il servizio di firma OTP, oltre alla firma del singolo documento tramite il servizio *pdfsignaturev2*, è possibile procedere alla firma in sequenza di più documenti utilizzando un solo codice OTP; per effettuare questa operazione è necessario eseguire le seguenti operazioni:
1. Apertura sessione utilizzando credenziali ed OTP tramite il servizio *opensession* che restituisce l'id sessione
2. Esecuzione in sequenza di più firme invocando più volte il servizio *pdfsignaturev2* utilizzando l'id sessione ottenuto al punto 1
3. Chiusura sessione tramite il servizio *closesession* utilizzando l'id sessione ottenuto al punto 1

Il parametro *typeOtpAuth* deve essere valorizzato con il dominio di rilascio delle firme:
* **typeOtpAuth = frPuntozero** per le firme remote
* **typeOtpAuth = faPuntozero** per le firme automatiche

## Catalogo Specialistica Ambulatoriale
Per l'implmentazione di alcuni CDA2 è necessario utilizzare il nomenclatore tariffario ed il catalogo di specialistica ambulatoriale di Regione Umbria:

[Catalogo specialistica ambulatoriale v9](/cataloghi/Catalogo_specialistica_Regione_Umbria_v9.xlsx)
