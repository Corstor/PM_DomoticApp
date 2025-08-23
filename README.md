# Project Management - DomoticApp

## Simulazione di progetto

Lo scopo del progetto software DomoticApp è il seguente: 

Creare una web app per gestire una casa domotica. In tale web app, è possibile registrarsi e fare login, e, una volta autenticati, gli utenti possono vedere i dispositivi che sono presenti e registrati nel server locale di casa (idealmente un PC che è sempre acceso in casa o un qualche altro dispositivo elettronico in grado di tenere attivo un server di dimensioni ridotte), cambiare il loro username e password, e creare script per automatizzare dei lavori con i dispositivi (per esempio spegnere tutte le luci di una stanza con un click solo, o far alzare le tapparelle se c'è luce fuori).

Gli admin possono aggiungere dispositivi al server (se presenti), creare gruppi e metterci i vari dispositivi in modo da raggrupparli (per esempio il gruppo Cucina può avere tutti i dispositivi che si trovano in cucina), gestire i permessi che gli utenti hanno su certi dispositivi o script automatici.

Oltre a questo, il pilastro portante del progetto è che il server in questione è in grado di riconoscere i dispositivi e di renderizzare automaticamente la grafica per il loro utilizzo (per esempio spegnere/accendere una luce) in base ad un protocollo che i dispositivi stessi devono implementare. Questo rende l'applicazione molto flessibile, dato che è in grado di gestire qualsiasi tipo di dispositivo a patto che utilizzi tale protocollo.

L'idea per l'elaborato di Project Management è quella di avere un'azienda software con già qualche anno alle spalle e che magari ha diretto accesso a dei dispositivi IoT che potrebbero programmare (o magari hanno già un loro protocollo che possono riutilizzare).

L'azienda che in questa simulazione si occuperà del progetto DomoticApp è la SDA Corporation (Smart Domotic Apps), che ha già creato dei dispositivi IoT in passato con relativa applicazione per gestirli, e vorrebbe riuscire ad estrarre un protocollo comune a tutti i dispositivi in modo da non doverli cambiare eccessivamente.

[Descrizione approccio utilizzato](./Descrizione_Approccio/DescrizioneApproccio.md)

[Documentazione di progetto](./Documentazione_Progetto/DocumentazioneProgetto.md)
