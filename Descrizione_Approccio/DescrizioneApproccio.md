# Descrizione dell'approccio utilizzato

## Riassunto del problema

Il progetto consiste nel creare una web app per la gestione di una casa domotica, con tanto di gestione dei permessi degli utenti, login/registrazione, script, raggruppamento logico di dispositivi e protocollo per la gestione di dispositivi eterogenei.

### Soluzione proposta

**_Users management subsystem_**: Il sottosistema che si occupa della gestione degli utenti nel server, ovvero login/registrazione, più il loro ruolo. Il ruolo potrà essere user o admin, dove l'admin ha permessi avanzati. Essendo pensato per un sistema che girerà in locale nelle case di persone, il primo utente a registrarsi diventerà automaticamente admin, gli altri dovranno essere approvati dall'admin per entrare come utenti normali (per evitare che uno sconosciuto si registri nel server di casa). Software COTS potrebbero costituire una parte significativa per la soluzione finale di tale sottosistema.

**_Devices management subsystem_**: Il sottosistema che si occupa della gestione dei dispositivi nel server, come la creazione e modifica dei gruppi logici, o la visualizzazione dei dispositivi attualmente presenti nel sistema, così come la comunicazione con essi (per esempio un utente può visualizzare una lampada accesa ma può anche spegnerla).
Solo un admin può creare e gestire i gruppi per non creare troppa confusione all'interno dell'app.

**_Devices Protocol_**: Protocollo per permettere a quanti più tipi diversi di dispositivi di registrarsi nel server, cercando di togliere meno funzionalità possibili ai dispositivi. Per esempio, se una lampadina si può accendere/spegnere, cambiare illuminazione e/o colore, tali funzionalità devono persistere quanto più possibile nel server. Va bene sacrificare la complessità grafica (come immagina/icone specifiche per ogni dispositivo) a favore di tale protocollo generico, in quanto gli utenti possiederebbero già un'applicazione specifica per ogni dispositivo, infatti lo scopo è creare un'app per gestirli tutti nel caso di tanti dispositivi diversi e di poterli anche automatizzare attraverso degli script.
Un'idea di base può essere dividere "l'essenza" di un dispositivo in tre punti: proprietà, azioni ed eventi.
Le proprietà sarebbero lo stato effettivo del dispositivo (luce rossa accesa al 50% di luminosità), le azioni sarebbero ciò che l'utente può effettuare per modificare le proprietà (accendi luce, cambia colore, cambia luminosità) e gli eventi sono inviati dal dispositivi quando una certa proprietà cambia in qualche modo (la luce è stata spenta, la luce è stata accesa, la luce ha cambiato colore, la luce ha cambiato luminosità).
In quanto sono già stati creati vari dispositivi eterogenei dalla SDA, un possibile approccio potrebbe essere quello di controllare i loro dispositivi e creare un protocollo che riesca a farli funzionare tutti correttamente, fornendo loro anche una buona dose di test per tale protocollo.

**_Devices registration subsystem_**: Il sottosistema che si occupa di registrare i dispositivi nel server a patto che rispettano il protocollo scelto. Tale sottosistema individua quali dispositivi sono presenti (per esempio attraverso bluetooth o wi-fi) e a quel punto un admin può decidere quali dei vari dispositivi presenti registrare nel server.

**_Scripts management subsystem_**: Il sottosistema che si occupa della gestione degli script nel server. Per poterli creare ci sarà bisogno di creare un linguaggio a blocchi (per migliorare la UX e renderlo accessibile a quante più persone possibili) che permetta l'esecuzione di azioni su vari dispositivi o di lettura di proprietà per creare flussi di controllo più complessi (per esempio: se la luce è spenta accendila, altrimenti spegnila). Sarà inoltre necessario dividere gli script in due tipi: task e automazioni.
Le task sono eseguibili manualmente da un utente che ne ha il permesso, mentre le automazioni sono eseguite automaticamente in base ad un evento di un dispositivo o ad una cadenza periodica e possono essere attivate e disattivate se l'utente in questione possiede i permessi per farlo.

**_Permissions management subsystem_**: Il sottosistema che si occupa della gestione dei permessi degli utenti nel server. Tale sottosistema deve dare la possibilità all'admin di vietare o permettere ad un utente di utilizzare le azioni di un certo dispositivo, di azionare una task, di creare/attivare/disattivare un' automazione.

**_Notifications management susbystem_**: Questo sottosistema si occupa della gestione delle notifiche, che possono essere inviate dagli script oppure da un dispositivo che va offline. Per evitare troppe notifiche, gli utenti possono decidere di quali dispositivi essere aggiornati dello stato online/offline.

**_Presentation subsystem_**: Questo sottosistema si occupa della resa grafica del sistema per aiutare gli utenti nella gestione della propria casa domotica. In quanto non si cerca di creare un sito web quanto più bello possibile ma uno molto funzionale ed intuitivo, non è necessario spendere troppo tempo nella UI quanto nella UX. A tale scopo si può rimanere molto legati a qualche design system completo già presente per accelerare il lavoro.
