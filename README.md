# Supporto Integrazione FSE
In questo repository sono definite le linee guida per l'interoperabilità con il middleware regionale
per il Fascicolo Sanitario Elettronico.

Il Middleware Regionale espone delle API basate su architettura REST.

Le API sono strutturate tramite URL orientati alle risorse, ritornano risorse in formato JSON e usano i codici di risposta e i metodi secondo standard HTTP.

Le linee guida per l'integrazione seguono quelle definite a livello nazionale per FSE 2.0.

## FSE 1.0
L'attuale versione del Fascicolo Sanitario Elettronico.

Le linee guida per l'interoperabilità riprendono quelle definite in FSE 2.0 in modo da allineare e rendere più semplice il processo di integrazione.

## FSE 2.0
La nuova versione del Fascicolo Sanitario Elettronico.

Il middleware regionale segue le linee guida definite dal [Gateway Nazionale](https://github.com/ministero-salute/it-fse-support/tree/main/doc/integrazione-gateway).

## Risorse
* [Open API](./openapi)

## Endpoint
Il base URL del **sistema di test** è:

  https://fse-api-test.regione.umbria.it

gli endpoint sono elencati nelle seguenti tabelle suddivisi tra endpoint per alimentazione FSE 1.0, alimentazione FSE 2.0 e comuni (servizi di interrogazione, gestione consenso, gestione deleghe, ecc.).


_Tabella 1: Endpoint delle funzionalità alimentazione FSE1.0_

<table>
  <tr>
   <td><strong>Endpoint URL</strong>
   </td>
   <td><strong>Metodo</strong>
   </td>
   <td><strong>Funzionalità</strong>
   </td>
  </tr>
  <tr>
   <td>/fse1/v1/repositories/{repositoryId}/documents</td>
   <td>POST</td>
   <td>Pubblica un documento nel circuito FSE 1.0</td>
  </tr>
  <tr>
   <td>/fse1/v1/repositories/{repositoryId}/documents/{documentId}</td>
   <td>DELETE</td>
   <td>Elimina un documento e i relativi metadati</td>
  </tr>
  <tr>
   <td>/fse1/v1/repositories/{repositoryId}/documents/{documentId}</td>
   <td>PUT</td>
   <td>Sostituisce un documento nel circuito FSE 1.0</td>
  </tr>
  <tr>
   <td>/fse1/v1/repositories/{repositoryId}/documents/{documentId}/metadata</td>
   <td>PUT</td>
   <td>Aggiorna i metadati del documento nel circuito FSE 1.0</td>
  </tr>
</table>


_Tabella 2: Endpoint delle funzionalità alimentazione FSE2.0_

<table>
  <tr>
   <td><strong>Endpoint URL</strong>
   </td>
   <td><strong>Metodo</strong>
   </td>
   <td><strong>Funzionalità</strong>
   </td>
  </tr>
  <tr>
   <td>/fse2/v1/documents/validation</td>
   <td>POST</td>
   <td>Validazione documenti</td>
  </tr>
  <tr>
   <td>/fse2/v1/repositories/{repositoryId}/documents</td>
   <td>POST</td>
   <td>Pubblicazione creazione documenti
  </tr>
  <tr>
   <td>/fse2/v1/repositories/{repositoryId}/documents/validate-and-create</td>
   <td>POST</td>
   <td>Pubblicazione creazione documenti</td>
  </tr>
  <tr>
   <td>/fse2/v1/repositories/{repositoryId}/documents/{documentId}</td>
   <td>PUT</td>
   <td>Sostituzione documenti</td>
  </tr>
  <tr>
   <td>/fse2/v1/repositories/{repositoryId}/documents/{documentId}</td>
   <td>DELETE</td>
   <td>Elimina un Documento</td>
  </tr>
  <tr>
   <td>/fse2/v1/repositories/{repositoryId}/documents/{documentId}/metadata</td>
   <td>PUT</td>
   <td>Aggiornamento metadati</td>
  </tr>
  <tr>
   <td>/fse2/v1/repositories/{repositoryId}/documents/validate-and-replace/{documentId}</td>
   <td>PUT</td>
   <td>Sostituzione documenti</td>
  </tr>
  <tr>
   <td>/fse2/v1/status/{workflowInstanceId}</td>
   <td>GET</td>
   <td>Recupero stato transazione</td>
  </tr>
  <tr>
   <td>/fse2/v1/status/search/{traceId}</td>
   <td>GET</td>
   <td>Recupero stato transazione</td>
  </tr>
</table>


_Tabella 3: Endpoint delle funzionalità comuni_

<table>
  <tr>
   <td><strong>Endpoint URL</strong>
   </td>
   <td><strong>Metodo</strong>
   </td>
   <td><strong>Funzionalità</strong>
   </td>
  </tr>
  <tr>
   <td>/fse1/v1/documents/metadata</td>
   <td>GET</td>
   <td>Recupera i metadati dei documenti</td>
  </tr>
  <tr>
   <td>/fse1/v1/repositories/{repositoryId}/documents/{documentId}</td>
   <td>GET</td>
   <td>Recupera un documento</td>
  </tr>
</table>

Per i test utilizzare:

<strong>repositoryId = 2.16.840.1.113883.2.9.2.100.4.5.2</strong>

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

## CATALOGO SPECIALISTICA AMBULATORIALE
Per l'implmentazione di alcuni CDA2 è necessario utilizzare il nomenclatore tariffario ed il catalogo di specialistica ambulatoriale di Regione Umbria:

[Catalogo specialistica ambulatoriale v3](/cataloghi/Catalogo_specialistica_Regione_Umbria_v3.xlsx)

Le versioni attuali del nomenclatore e del catalogo resteranno in vigore, a normativa vigente, fino al 31-12-2024; dal 01-01-2025 verranno sostituiti dal nuovo nomenclatore e nuovo catalogo:

[Catalogo specialistica ambulatoriale v5](/cataloghi/Catalogo_specialistica_Regione_Umbria_v5.xlsx)

## PARAMETRI DI INPUT

I parametri di input sono valorizzati secondo le regole del [gateway nazionale](https://github.com/ministero-salute/it-fse-support/blob/main/doc/integrazione-gateway/README.md#13-drilldown-parametri-di-input) e dell'[Affinity Domain Italia 2.5](https://www.fascicolosanitario.gov.it/sites/default/files/public/media/Specifiche%20interoperabilit%C3%A0/AffinityDomainItalia_v2-5_v20231212.pdf).

In questo paragrafo verranno descritti esclusivamente i campi aggiuntivi necessari per FSE 1.0 ed quelli per i quali è necessario fornire informazioni aggiuntive rispetto alle specifiche nazionali.

<table>
  <tr>
   <td colspan="2" ><strong>IDENTIFICATIVO DOCUMENTO</strong></td>
  </tr>
  <tr>
   <td><strong>PARAMETRO</strong></td>
   <td><code>identificativoDoc</code></td>
  </tr>
  <tr>
   <td><strong>DESCRIZIONE</strong></td>
   <td>Da Affinity Domain, come specificato al paragrafo 2.20: l’OID da utilizzare per il metadato uniqueId deve essere strutturato nel seguente modo: per i documenti gestiti da un sistema di FSE regionale, il valore deve essere 2.16.840.1.113883.2.9.2.[REGIONE].4.4^X, dove X rappresenta una specifica istanza di documento presente in regione.
Il valore [REGIONE] è il valore corrispondente alla regione indicato in Tabella 6.43 (la prima cifra numerica pari a 0 va omessa).
Vedi TABELLA ORGANIZZAZIONE per il codice della REGIONE.
Per Regione Umbria il codice istanza X deve essere generato come UUID.
</td>
  </tr>
  <tr>
   <td><strong>ESEMPIO</strong></td>
   <td>2.16.840.1.113883.2.9.2.100.4.4^9910967b-984d-4275-a7d2-0aeb7e0a37db</td>
  </tr>
  <tr>
   <td><strong>VALIDAZIONE</strong></td>
   <td>Obbligatorio</td>
  </tr>
</table>


<table>
  <tr>
   <td colspan="2" ><strong>IDENTIFICATIVO SOTTOMISSIONE</strong></td>
  </tr>
  <tr>
   <td><strong>PARAMETRO</strong></td>
   <td><code>identificativoSottomissione</code></td>
  </tr>
  <tr>
   <td><strong>DESCRIZIONE</strong></td>
   <td>Metadato che rappresenta l’identificativo univoco dell’oggetto XDSSubmissionSet.
Formato codifica conforme alla specifiche IHE (ITI TF-3), di tipo OID, strutturato nel seguente modo: 2.16.840.1.113883.2.9.2.[REGIONE oppure INI].4.3.X, dove X rappresenta una specifica istanza di XDSSubmissionSet..
Vedi TABELLA ORGANIZZAZIONE per il codice della REGIONE.
Per Regione Umbria il codice istanza X deve essere generato secondo il formato:
TIMESTAMP_MILLISECONDI.RANDOM_6_CIFRE
Per ottenere un OID valido ciascuna porzione di OID (sezione tra due punti) può valere "0" ma se composto da più cifre non può iniziare con "0" quindi il numero random va generato tra 100000 e 999999.
</td>
  </tr>
  <tr>
   <td><strong>ESEMPIO</strong></td>
   <td>2.16.840.1.113883.2.9.2.100.4.3.20240923082141123.123456</td>
  </tr>
  <tr>
   <td><strong>VALIDAZIONE</strong></td>
   <td>Obbligatorio</td>
  </tr>
</table>

Parametri aggiuntivi per FSE 1.0:


<table>
  <tr>
   <td colspan="2" ><strong>XDSDocumentEntry.creationTime</strong></td>
  </tr>
  <tr>
   <td><strong>PARAMETRO</strong></td>
   <td><code>creationTime</code></td>
  </tr>
  <tr>
   <td><strong>DESCRIZIONE</strong></td>
   <td>Data di creazione del documento. Formato codifica conforme alle specifiche IHE (ITI TF-3).
</td>
  </tr>
  <tr>
   <td><strong>ESEMPIO</strong></td>
   <td>20141020110012</td>
  </tr>
  <tr>
   <td><strong>VALIDAZIONE</strong></td>
   <td>Obbligatorio</td>
  </tr>
</table>


<table>
  <tr>
   <td colspan="2" ><strong>XDSDocumentEntry.confidentialityCode</strong></td>
  </tr>
  <tr>
   <td><strong>PARAMETRO</strong></td>
   <td><code>confidentialityCode</code></td>
  </tr>
  <tr>
   <td><strong>DESCRIZIONE</strong></td>
   <td>Questo metadato viene utilizzato per indicare il livello di riservatezza dei dati contenuti nel documento che deve essere indicizzato.
     Deve essere valorizzato come indicato in Affinity Domain Italia paragrafo 2.5.
</td>
  </tr>
  <tr>
   <td><strong>ESEMPIO</strong></td>
   <td>N</td>
  </tr>
  <tr>
   <td><strong>VALIDAZIONE</strong></td>
   <td>Obbligatorio</td>
  </tr>
</table>


<table>
  <tr>
   <td colspan="2" ><strong>XDSDocumentEntry.formatCode</strong></td>
  </tr>
  <tr>
   <td><strong>PARAMETRO</strong></td>
   <td><code>formatCode</code></td>
  </tr>
  <tr>
   <td><strong>DESCRIZIONE</strong></td>
   <td>Tale metadato viene utilizzato per indicare il formato del documento che viene indicizzato nella RDA. Questo metadato, insieme al metadato XDSDocumentEntry.typeCode, permette ad un XDS Document Consumer di comprendere la tipologia di documento (eventualmente interpretabile in modo automatico).
     Deve essere valorizzato come indicato in Affinity Domain Italia paragrafo 2.6.
</td>
  </tr>
  <tr>
   <td><strong>ESEMPIO</strong></td>
   <td>2.16.840.1.113883.2.9.10.1.1</td>
  </tr>
  <tr>
   <td><strong>VALIDAZIONE</strong></td>
   <td>Obbligatorio</td>
  </tr>
</table>


<table>
  <tr>
   <td colspan="2" ><strong>XDSDocumentEntry.languageCode</strong></td>
  </tr>
  <tr>
   <td><strong>PARAMETRO</strong></td>
   <td><code>languageCode</code></td>
  </tr>
  <tr>
   <td><strong>DESCRIZIONE</strong></td>
   <td>Metadato che indica la lingua del documento e deve essere codificato con il valore “it-IT”.
     Deve essere valorizzato come indicato in Affinity Domain Italia paragrafo 2.10.
</td>
  </tr>
  <tr>
   <td><strong>ESEMPIO</strong></td>
   <td>it-IT</td>
  </tr>
  <tr>
   <td><strong>VALIDAZIONE</strong></td>
   <td>Obbligatorio</td>
  </tr>
</table>


<table>
  <tr>
   <td colspan="2" ><strong>XDSDocumentEntry.mimeType</strong></td>
  </tr>
  <tr>
   <td><strong>PARAMETRO</strong></td>
   <td><code>mimeType</code></td>
  </tr>
  <tr>
   <td><strong>DESCRIZIONE</strong></td>
   <td>Tale metadato identifica il MIME type del documento indicizzato e ha lo scopo di fornire indicazione all’attore XDS Document Consumer sulla tipologia del documento.
     Deve essere valorizzato come indicato in Affinity Domain Italia paragrafo 2.11.
</td>
  </tr>
  <tr>
   <td><strong>ESEMPIO</strong></td>
   <td>application/pdf+text/x-cda-r2+xml</td>
  </tr>
  <tr>
   <td><strong>VALIDAZIONE</strong></td>
   <td>Obbligatorio</td>
  </tr>
</table>


<table>
  <tr>
   <td colspan="2" ><strong>XDSDocumentEntry.patientId</strong></td>
  </tr>
  <tr>
   <td><strong>PARAMETRO</strong></td>
   <td><code>patientId</code></td>
  </tr>
  <tr>
   <td><strong>DESCRIZIONE</strong></td>
   <td>Questo metadato permette di identificare il paziente a cui è correlato il documento prodotto, in particolare il codice fiscale se è un cittadino italiano assistito dal SSN.
     Questo metadato è codificato con un tipo di dato CX e può contenere solo le componenti Id e AssignedAuthority.
     Deve essere valorizzato come indicato in Affinity Domain Italia paragrafo 2.12.
</td>
  </tr>
  <tr>
   <td><strong>ESEMPIO</strong></td>
   <td>ZNRMA86L11B157N^^^&2.16.840.1.113883.2.9.4.3.2&ISO</td>
  </tr>
  <tr>
   <td><strong>VALIDAZIONE</strong></td>
   <td>Obbligatorio</td>
  </tr>
</table>


<table>
  <tr>
   <td colspan="2" ><strong>XDSDocumentEntry.title</strong></td>
  </tr>
  <tr>
   <td><strong>PARAMETRO</strong></td>
   <td><code>title</code></td>
  </tr>
  <tr>
   <td><strong>DESCRIZIONE</strong></td>
   <td>Tale metadato permette di specificare il titolo del documento a cui fa riferimento.
     Deve essere valorizzato come indicato in Affinity Domain Italia paragrafo 2.18.
</td>
  </tr>
  <tr>
   <td><strong>ESEMPIO</strong></td>
   <td>Referto di laboratorio</td>
  </tr>
  <tr>
   <td><strong>VALIDAZIONE</strong></td>
   <td>Non obbligatorio, raccomandata la compilazione</td>
  </tr>
</table>


<table>
  <tr>
   <td colspan="2" ><strong>XDSDocumentEntry.typeCode</strong></td>
  </tr>
  <tr>
   <td><strong>PARAMETRO</strong></td>
   <td><code>formatCode</code></td>
  </tr>
  <tr>
   <td><strong>DESCRIZIONE</strong></td>
   <td>Metadato che descrive la specifica tipologia di documento prodotto da indicizzare.
     Deve essere valorizzato come indicato in Affinity Domain Italia paragrafo 2.19.
</td>
  </tr>
  <tr>
   <td><strong>ESEMPIO</strong></td>
   <td>11502-2</td>
  </tr>
  <tr>
   <td><strong>VALIDAZIONE</strong></td>
   <td>Obbligatorio</td>
  </tr>
</table>


<table>
  <tr>
   <td colspan="2" ><strong>XDSDocumentEntry.Slot - documentSigned</strong></td>
  </tr>
  <tr>
   <td><strong>PARAMETRO</strong></td>
   <td><code>isDigitallySigned</code></td>
  </tr>
  <tr>
   <td><strong>DESCRIZIONE</strong></td>
   <td>Questo metadato obbligatorio è utilizzato per indicare se il documento associato al DocumentEntry è firmato digitalmente o meno.
     Deve essere valorizzato come indicato in Affinity Domain Italia paragrafo 2.22.
</td>
  </tr>
  <tr>
   <td><strong>ESEMPIO</strong></td>
   <td>true</td>
  </tr>
  <tr>
   <td><strong>VALIDAZIONE</strong></td>
   <td>Obbligatorio</td>
  </tr>
</table>

