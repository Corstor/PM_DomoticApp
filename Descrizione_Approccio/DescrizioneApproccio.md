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

## Project Scoping Meeting

Partecipanti: Project Manager, Responsabile Reparto Elettronica, Responsabile Reparto IT, Sviluppatori, CEO, Facilitator.

Ordine del giorno:

| Orario        | Durata | Argomento                                                                   |
| ------------- | ------ | --------------------------------------------------------------------------- |
| 09:30 - 09:45 | 15 min | Introduzione al progetto e obiettivi del meeting                            |
| 09:45 - 10:15 | 30 min | Stato Attuale (AS IS)                                                       |
| 10:15 - 11:00 | 45 min | Stato Desiderato (TO BE), identificazione priorità e criticità del progetto |
| 11:00 - 11:20 | 20 min | Condictions Of Satisfaction (COS)                                           |
| 11:20 - 11:30 | 10 min | Analisi degli stakeholders                                                  |
| 11:30 - 11:40 | 10 min | Pianificazione degli incontri successivi e delle attività operative         |
| 11:40 - 12:00 | 20 min | Chiusura con osservazioni e sintesi del meeting, raccolta di feedback       |

Durante il primo **Project Scoping Meeting** i partecipanti hanno comunicato e condiviso la necessità per l'azienda di dover fornire ai propri utenti un sistema software che permetta l'utilizzo di molteplici dispositivi in maniera rapida ed efficace, senza dover pensare troppo ad un interfaccia grafica ad-hoc per dispositivo, in quanto forniscono già quelle applicazioni.

Questo è stato possibile poichè è stata condotta un'analisi dell'attuale utilizzo degli utenti dei propri dispositivi IoT (**AS IS**) (tale analisi è stata possibile grazie alle recensioni lasciate dagli utenti), discutendo quindi di come poter risolvere il problema attraverso un sistema software (**TO BE**), definendone le principali caratteristiche, come il linguaggio a blocchi per gli script, un protocollo comune tra tutti i dispositivi e la gestione dei permessi degli utenti da parte di un admin.

Il **linguaggio a blocchi** è stato pensato per poter dare agli utenti la possibilità di far eseguire azioni pre-programmate o automatiche a certi dispositivi in base all'ambiente che li circonda (per esempio chiudere la finestra se fa freddo, utilizzando un sensore per la temperatura e un attuatore per la finestra che prima non potevano comunicare).
Il **protocollo** è il pilastro portante del progetto in quanto è necessario per poter gestire molteplici dispositivi eterogenei con la stessa applicazione senza dover fare grafiche diverse per ogni dispositivo.
La **gestione dei permessi** è saltata fuori nel momento in cui un bambino dovesse creare script "pericolosi" senza il permesso dei genitori, è richiesto dunque una adeguata gestione in tal senso.

Inoltre la discussione ha fatto luce su certe **Conditions Of Satisfactions (COS)** che guideranno il monitoring del progetto ed un'analisi degli **stakeholder** per comprendere appieno il target del progetto.

Infine, sono stati decisi i prossimi passi, incluso un secondo incontro per la **gestione dei rischi** e un'analisi dettagliata dei **requisiti**. Nonostante inizialmente erano presenti degli sviluppatori un po' scettici riguardo il protocollo comune tra i dispositivi, la comunicazione tra le varie parti e qualche idea abbozzata ha calmato gli spiriti e tutti sperano nella riuscita del progetto.

## Stakeholders Analysis

L'analisi degli stakeholders effettuata nel project scoping meeting è stato piuttosto veloce, dato che molti stakeholders dei vecchi progetti sono gli stessi di questo progetto, anche se con qualche eccezione.

### Utenti

Gli utenti rappresentano il target principale del progetto, e possono essere suddivisi a loro volta in due categorie principali: utenti con **almeno 4 dispositivi IoT** e utenti con **meno di 4 dispositivi IoT**.

I primi sono il vero target del progetto, in quanto l'applicativo serve proprio per aiutare nella gestione di tanti dispositivi IoT attraverso l'utilizzo di una singola app.

I secondi, per quanto non siano il target principale, sono comunque considerati per più motivi:
- potrebbero decidere di comprare altri dispositivi IoT dall'azienda se ne vedono un particolare guadagno con l'utilizzo dell'applicativo;
- potrebbero decidere comunque di usare l'applicativo perchè comodo (per esempio potrebbero avere solamente un sensore della luce e una o due lampadine IoT, permettendo di automatizzare accensione/spegnimento delle luci in base alla luce percepita dal sensore);
- E' importante controllare e far sì che questi utenti non preferiscano il nuovo applicativo al vecchio in tutte le situazioni, perchè questo progetto non si pone l'obbiettivo di togliere le vecchie applicazioni specifiche per dispositivo.

Ovviamente per l'azienda rendere "inutili" i vecchi applicativi vorrebbe dire non doverle più aggiornare e produrre ma piuttosto tenere aggiornato solo quello nuovo, però questa decisione avrebbe bisogno di un appoggio concreto fornito da tanti feedback da parte degli utenti, in modo da capire se il nuovo applicativo è davvero in grado di sostituire tutti i vecchi, per cui si pensa che si possa mettere da parte questa soluzione per il momento.

### Sviluppatori

Gli sviluppatori sono un altro importante stakeholder. Infatti questo progetto andrà ad impattare per sempre il loro modo di lavorare, dato che per ogni nuovo dispositivo dovranno poi andare a fornirne il protocollo deciso in questo progetto. Un altro motivo è che se dovesse essere creato un dispositivo che non è gestibile attraverso questo applicativo, sarà comunque compito loro dover aggiornare il protocollo per renderlo funzionante anche nel nuovo caso.

### SDA Corporation

Supporta il progetto per i benefici strategici che ne possono ricavare, come il miglioramento della soddisfazione dei clienti e il rafforzamento della loro reputazione nel complesso mondo dell'IoT.

### Investitori e finanziatori

Supporta il progetto per i benefici economici che ne possono ricavare, puntando ad un guadagno misurabile ottenuto principalmente dalla maggiore soddisfazione dei clienti.
