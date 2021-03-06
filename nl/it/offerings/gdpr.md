---

copyright:
  years: 2018
lastupdated: "2018-06-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Acrolinx: 2018-04-28 -->

# Regolamento generale sulla protezione dei dati  (GDPR, General Data Protection Regulation)

Il GDPR cerca di creare un quadro normativo armonizzato in materia di protezione dei dati
in tutta l'Unione Europea e mira a restituire ai cittadini il controllo dei propri dati personali,
imponendo nel contempo regole rigide a coloro che ospitano ed "elaborano" questi dati, in qualsiasi parte del mondo. Il
regolamento introduce anche regole relative alla libera circolazione dei dati personali all'interno e all'esterno
dell'Unione Europea. 

Con il Regolamento generale sulla protezione dei dati, noto in inglese come [General Data Protection Regulation![Icona link esterno](../images/launch-glyph.svg "Icona link esterno")](https://www.eugdpr.org/){:new_window},
{{site.data.keyword.cloudantfull}} i clienti possono contare sulla comprensione e la conformità del team {{site.data.keyword.cloudant_short_notm}} agli standard e alla legislazione emergenti in materia di riservatezza dei dati e anche alla più ampia capacità di {{site.data.keyword.IBM}} di fornire una suite completa di soluzioni per assistere le attività commerciali di tutte le dimensioni con i loro requisiti di governance dei dati interna.

## Come controllo l'accesso a {{site.data.keyword.cloudant_short_notm}}?

Puoi trovare informazioni sul controllo in [Registrazione di controllo](../offerings/audit.html#audit-logging){:new_window}. 

## Classificazioni supportate dei dati personali

Le seguenti categorie di dati personali sono supportate da {{site.data.keyword.cloudant_short_notm}}
per GDPR:

**Dati personali**, ad esempio:
 * Identità/stato civile
 * Vita personale
 * Vita professionale
 * Informazioni economiche e finanziarie
 * Dati relativi alla posizione
 * Connettività/dati sul dispositivo

**Dati personali sensibili**, limitati a:
  * Dati sulla salute; si applicano delle condizioni supplementari da trattare in una descrizione del servizio

Se stai archiviando dati di assistenza sanitaria, *devi* completare le seguenti attività:
 - Informare {{site.data.keyword.cloudant_short_notm}} prima di scrivere eventuali dati.
 - Richiedere un cluster dedicato conforme a HIPAA.

Per ulteriori informazioni sulle classificazioni supportate di dati personali, consulta i
[requisiti di sistema dettagliati di {{site.data.keyword.cloudant_short_notm}} in 2. Personal Data ![Icona link esterno](../images/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=2EBB5860B34311E7A9EB066095601ABB){:new_window}.

## Dati su di me

{{site.data.keyword.cloudant_short_notm}} registra alcuni dati sui suoi utenti ed è un controller dei dati per tali dati di informazioni personali (PI, Personal Information). I dati da noi registrati dipendono dal tipo di account che hai.

Se hai un cluster {{site.data.keyword.cloudant_short_notm}} dedicato/cluster {{site.data.keyword.cloudant_short_notm}}
Enterprise, registriamo i dati sul tuo conto e siamo considerati un controller dei dati per i tuoi dati nel contesto di GDPR.
Se hai un cluster {{site.data.keyword.cloudant_short_notm}} dedicato/cluster {{site.data.keyword.cloudant_short_notm}}
Enterprise, abbiamo i tuoi:

 * Nome
 * Email

I dati che conserviamo possono essere visualizzati e aggiornati tramite il dashboard {{site.data.keyword.cloudant_short_notm}}.

Se hai un account di cui viene eseguito il provisioning da {{site.data.keyword.cloud_notm}} (compresa un'istanza dedicata),
{{site.data.keyword.cloudant_short_notm}} _non_ raccoglie i dati personali precedentemente menzionati. Questi dati vengono conservati da {{site.data.keyword.cloud_notm}}.

{{site.data.keyword.cloudant_short_notm}} elabora delle informazioni personali del cliente limitate nel corso dell'esecuzione del servizio e dell'ottimizzazione dell'esperienza utente a esso relativa. Utilizziamo l'email per contattare i clienti come appropriato. Il monitoraggio delle interazioni dei clienti con il dashboard {{site.data.keyword.cloudant_short_notm}} è l'altro modo in cui elaboriamo le informazioni personali.

### Limitazioni dell'elaborazione

Inviamo le interazioni con il dashboard a Segment. È possibile chiedere a {{site.data.keyword.cloudant_short_notm}} di limitare l'elaborazione delle informazioni personali del cliente in questo modo mediante una [richiesta di supporto {{site.data.keyword.cloudant_short_notm}}](mailto:support@cloudant.com). Alla ricezione di una richiesta di questo tipo, {{site.data.keyword.cloudant_short_notm}} elimina le informazioni associate al cliente così come sono inviate a Segment ed impedisce l'invio di ulteriori dati. Abbiamo bisogno di continuare a poter contattare i clienti dedicati tramite email e fornire un'interfaccia ai clienti per tenere aggiornate queste informazioni direttamente o tramite la configurazione dei clienti dei loro dettagli di contatto tramite i loro dettagli dell'account {{site.data.keyword.cloud_notm}}.

## Il nostro database {{site.data.keyword.cloudant_short_notm}} è crittografato?

Tutti i cluster hanno un file system crittografato (crittografia dei dati inattivi) utilizzando LUKS (Linux Unified Key Setup), I dati nel database sono visibili ai nostri team operativi e di supporto (vedi di seguito).

Per i dati sensibili, che tu indichi che devono rimanere invisibili a {{site.data.keyword.cloudant_short_notm}},
devi crittografare o proteggere in altro modo (pseudonomizzare) i tuoi dati prima di inviarceli. Devi evitare di utilizzare informazioni personali per un `_id` documento poiché sono sempre visibili e scritti nei log di accesso.

## Ubicazioni dei dati

Le ubicazioni dove {{site.data.keyword.cloudant_short_notm}} elabora i dati personali saranno rese disponibili, e mantenute aggiornate, tramite il Data Sheet Addendum (DPA).

Per ulteriori informazioni sulle ubicazioni dei dati, consulta i
[requisiti di sistema dettagliati di {{site.data.keyword.cloudantfull}} in 7. {{site.data.keyword.IBM_notm}} Hosting and Processing Locations ![Icona link esterno](../images/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=2EBB5860B34311E7A9EB066095601ABB){:new_window}.

## Sicurezza del servizio

### Utilizzo di {{site.data.keyword.cloudant_short_notm}} in modo sicuro

In quanto utente di {{site.data.keyword.cloudant_short_notm}}, devi:

 * Utilizzare la configurazione CORS predefinita per evitare accessi imprevisti.
 * Utilizzare le chiavi API in ampia misura, in modo che i componenti possano avere un 'accesso meno privilegiato' associato al log di controllo. Questa prassi ti consente di comprendere chi ha eseguito l'accesso e a quali dati.
 * Crittografare o proteggere in altro modo (pseudonomizzare) qualsiasi dato sensibile prima di inviarcelo.

### Misure di sicurezza fisiche ed ambientali

La sicurezza fisica dei nostri data center è gestita dai nostri provider dell'infrastruttura: SoftLayer,
AWS e 21Vianet. Tutti detengono certificazioni controllate esternamente per la loro sicurezza fisica. Non forniremo
ulteriori dettagli dei controlli di sicurezza fisici implementati presso i nostri data center.

La sicurezza fisica delle ubicazioni degli uffici utilizzata dal nostro personale è gestita da {{site.data.keyword.IBM_notm}} Corporate.
I dettagli della certificazione e i rapporti delle attestazioni (ossia ISO e SOC2) possono essere forniti al cliente su richiesta.

### Misure tecniche e organizzative

Le misure tecniche e organizzative (TOM, Technical and Organisational Measures) sono adottate da {{site.data.keyword.cloudant_short_notm}}
per garantire la sicurezza dei dati personali. Siamo in possesso di certificazioni controllate esternamente per i controlli da noi adottati.
I dettagli della certificazione e i rapporti delle attestazioni (ossia ISO e SOC2) possono essere forniti al cliente su richiesta.

### Accesso di servizio ai dati

Le operazioni di {{site.data.keyword.cloudant_short_notm}} e lo staff di supporto hanno accesso ai dati del cliente e possono accedervi durante operazioni di routine. Tale accesso viene eseguito solo come necessario al fine di operare e supportare il servizio.
L'accesso è anche limitato in base al principio dell'*esigenza di sapere* ed è registrato, monitorato e controllato.

## Eliminazione dei dati

### Eliminazione di un documento

Quando un documento viene eliminato, il database crea un indicatore di rimozione definitiva, detto 'tombstone'. Quello che il tombstone contiene dipende da come esegui tale eliminazione.

 - Se hai eseguito una chiamata `DELETE`, questo indicatore include i campi `_id`, `_rev` e `_deleted`.
 - Se esegui l'eliminazione aggiornando il documento con un campo `_deleted: true` ed eseguendone il `PUT` o il `POST`, il tombstone include quanto da te impostato nel corpo del documento. Questa prassi può essere utile in alcune circostanze, ad esempio quando si registra perché un documento è stato eliminato nel relativo tombstone.

Per ulteriori informazioni sull'eliminazione di tombstone, consulta il documento relativo alla [semplice rimozione di documenti 'tombstone'](../api/document.html#-tombstone-documents){:new_window}.

### Quando viene rimosso un documento eliminato?

La compattazione viene eseguita automaticamente e rimuove periodicamente le vecchie revisioni (eliminate o altro) dal database scrivendo solo le revisioni 'foglia' in un nuovo file. Conserviamo una cronologia di `_id` e `_rev` per abilitare la replica ma non i corpi dei vecchi documenti.

> **Nota**: {{site.data.keyword.cloudant_short_notm}} non espone l'API di compattazione CouchDB.

Non garantiamo che un database sarà compattato a un momento specifico. I cluster possono ospitare
10000+ account, ciascuno dei quali contenente molti database. La compattazione viene eseguita come un processo di background nell'intero cluster e per i database è sempre in corso la compattazione; semplicemente non c'è alcuna garanzia che si tratti dei dati da te appena eliminati/modificati.

{{site.data.keyword.cloudant_short_notm}} accetta le richieste di *Diritto all'oblio* tramite
il DPO (Data Privacy Office) [{{site.data.keyword.IBM_notm}} ![Icona link esterno](../images/launch-glyph.svg "Icona link esterno")](http://w3-03.ibm.com/ibm/privacy/index.html){:new_window}.
Quando viene effettuata una richiesta di *Diritto all'oblio* dal DPO {{site.data.keyword.IBM_notm}}, verifichiamo la richiesta,
attiviamo esplicitamente la compattazione del database e verifichiamo che la compattazione sia stata eseguita.
Alla fine di questo processo, la sola versione del documento è il relativo tombstone
(`_id`, `_rev`, `_deleted`, e qualsiasi campo lì incluso dalla tua applicazione):

### Rimozione dei tombstone

{{site.data.keyword.cloudant_short_notm}} può rimuovere completamente tutti i riferimenti e i dati per un documento, quando richiesto. Questa attività è
un processo gestito dall'operatore denominato cancellazione (purge). Prima di richiedere la cancellazione (purge) dei documenti, è importante comprendere che i documenti cancellati (purge) *non possono essere ripristinati* da {{site.data.keyword.cloudant_short_notm}}, una volta completato il processo.

> **Nota**: la API di cancellazione (purge) CouchDB non è supportata da {{site.data.keyword.cloudant_short_notm}}.

Nel contesto di GDPR, la cancellazione (purge) è richiesta solo se i dati personali sono utilizzati in un ID documento. Un `_id` che memorizza informazioni personali è una cattiva idea per molti motivi ma ci sono alcuni casi d'uso parzialmente validi (ad esempio, un'email univoca). È possibile crittografare o pseudonomizzare i dati in modo che siano opachi per {{site.data.keyword.cloudant_short_notm}}.

Se è necessaria la rimozione di un documento tramite una richiesta di *Diritto all'oblio*:

1. Presenta una richiesta presso il DPO [{{site.data.keyword.IBM_notm}} ![Icona link esterno](../images/launch-glyph.svg "Icona link esterno")](http://w3-03.ibm.com/ibm/privacy/index.html){:new_window} per richiedere la cancellazione (purge) di specifici valori `_id` documento insieme al motivo.
1. Quando il DPO {{site.data.keyword.IBM_notm}} riceve una richiesta formale, il personale responsabile delle operazioni di {{site.data.keyword.cloudant_short_notm}}
verifica la richiesta per confermare che l'`id` contenga informazioni personali. Non cancelliamo (purge) i dati che non presentano informazioni personali nell'`_id`. 
1. {{site.data.keyword.cloudant_short_notm}} attiva l'azione di cancellazione (purge) per rimuovere permanentemente i dati richiesti.

Questo processo deve essere utilizzato solo per richieste di eliminazione di emergenza (ad esempio *diritto all'oblio*) e non si deve fare affidamento su di esso a lungo termine. Se la tua applicazione sta intenzionalmente utilizzando informazioni personali negli ID documento, deve essere modificata per pseudonomizzare tali informazioni personali oppure non deve utilizzare le informazioni personali negli ID documento. Non puoi contare sulla regolare esecuzione di cancellazioni (purge) da parte del team operativo di {{site.data.keyword.cloudant_short_notm}} per evitarlo.
{{site.data.keyword.cloudant_short_notm}} rifiuta pertanto le seguenti richieste di cancellazione (purge):

1. La richiesta è per una cancellazione (purge) regolare, ad esempio *ogni 30 giorni*.
1. La richiesta è per più di 100 documenti.

Anche con la cancellazione (purge), le informazioni personali nel campo `_id` possono andare a finire in posti dove non vuoi che compaiano, come ad esempio nei log {{site.data.keyword.cloudant_short_notm}} e, pertanto, tale situazione deve essere evitata. Abbiamo un motivo di business per conservare questi log e non rimuoveremo le righe del log che contengono i valori di `_id` documento.

### Cos'è l'eliminazione di un database?

L'eliminazione di un database lo mette in un cestino per un massimo di 48 ore, trascorse le quali viene rimosso dal file system. Il team {{site.data.keyword.cloudant_short_notm}} *non* esegue dei backup dei tuoi database; tale attività è *responsabilità del cliente*. Devi assicurarti che tutte le copie del tuo database vengano rimosse dal tuo sistema. Per ulteriori informazioni, consulta [Backup e ripristino di {{site.data.keyword.cloudant_short_notm}}](../guides/backup-cookbook.html#cloudant-nosql-db-backup-and-recovery){:new_window}. 

Se hai bisogno di ulteriore assistenza, contatta il [supporto {{site.data.keyword.cloudant_short_notm}} ![Icona link esterno](../images/launch-glyph.svg "Icona link esterno")](mailto:support@cloudant.com).

