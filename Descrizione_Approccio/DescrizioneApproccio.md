# Indice

- [Indice](#indice)
- [Descrizione dell'approccio utilizzato](#descrizione-dellapproccio-utilizzato)
  - [Riassunto del problema](#riassunto-del-problema)
    - [Soluzione proposta](#soluzione-proposta)
  - [Project Scoping Meeting](#project-scoping-meeting)
  - [Stakeholders Analysis](#stakeholders-analysis)
    - [Utenti](#utenti)
    - [Sviluppatori](#sviluppatori)
    - [SDA Corporation](#sda-corporation)
    - [Investitori e finanziatori](#investitori-e-finanziatori)
  - [Desideri e Bisogni](#desideri-e-bisogni)
    - [Desideri](#desideri)
    - [Bisogni](#bisogni)
  - [Altri Project Scoping Meeting](#altri-project-scoping-meeting)
    - [Project Scoping Meeting 2](#project-scoping-meeting-2)
    - [Project Scoping Meeting 3](#project-scoping-meeting-3)
    - [Project Scoping Meeting 4](#project-scoping-meeting-4)
  - [Planning Process Group](#planning-process-group)
    - [Joint Project Planning Session (JPPS)](#joint-project-planning-session-jpps)
    - [Project Definition Statement (PDS)](#project-definition-statement-pds)
    - [Work Breakdown Structure (WBS)](#work-breakdown-structure-wbs)
    - [Stime di Effort e Durata](#stime-di-effort-e-durata)
    - [Assegnamento delle Risorse](#assegnamento-delle-risorse)
    - [Project Network Diagram e Critical Path](#project-network-diagram-e-critical-path)
    - [Compressione della Schedule](#compressione-della-schedule)
    - [Management Reserve](#management-reserve)
    - [Stime dei Costi e Cash Flow](#stime-dei-costi-e-cash-flow)
    - [Project Proposal](#project-proposal)

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

Inoltre la discussione ha fatto luce su certe **Conditions Of Satisfactions (COS)** che guideranno la definizione del **POS** e il monitoring del progetto ed un'analisi degli **stakeholder** per comprendere appieno il target del progetto.

Infine, sono stati decisi i prossimi passi, incluso un secondo incontro per la **gestione dei rischi** e un'analisi dettagliata dei **requisiti**.

Nonostante inizialmente erano presenti degli sviluppatori un po' scettici riguardo il protocollo comune tra i dispositivi, la comunicazione tra le varie parti e qualche idea abbozzata ha calmato gli spiriti e tutti sperano nella riuscita del progetto.

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

## Desideri e Bisogni

Grazie alla stakeholder analysis e all'analisi dello stato attuale e lo stato desiderato, è stato possibile definire quali sono i desideri e i bisogni dell'azienda.

### Desideri

- Fornire delle notifiche agli utenti quando un dispositivo cambia status da online ad offline o viceversa;
- Fornire delle notifiche agli utenti quando uno script da errore;
- Non sostituire i vecchi applicativi con quello nuovo, ma evidenziarne l'utilità;
- Raggruppare i dispositivi in gruppi logici per facilitare l'utilizzo dell'applicativo da parte degli utenti.

### Bisogni

- Applicativo che gestisca molti dispositivi anche eterogenei in modo uniforme;
- Applicativo che permetta di eseguire automazioni e/o sequenze di azioni pre-programmate su vari dispositivi anche eterogenei;
- Riduzione dei passaggi ripetitivi da parte degli utenti per aumentarne la soddisfazione;

## Altri Project Scoping Meeting

In seguito al primo Project Scoping Meeting ne sono succeduti altri tre, in cui hanno fatto parte anche altri stakeholder chiave, come gli investitori e, indirettamente, gli utenti (attraverso il loro feedback delle recensioni lasciate sul sito dell'azienda).

### Project Scoping Meeting 2

Nel secondo incontro ci si è concentrati sulla definizione dei requisiti e della analisi degli stakeholder, oltre che alla scelta dei PMLC model, come preannunciato alla fine del primo.

Si è redatto una **Requirements Breakdown Structure** (RBS) per la maggior parte delle funzionalità, pur incorporandola con delle **user stories** per poter definire ancor meglio i ruoli degli utenti (user/admin) e certi requisiti complessi che non riuscivano ad essere definiti in modo chiaro e completo attraverso la RBS.

In seguito alla **analisi degli stakeholder**, si è deciso di tenere in considerazione anche il feedback degli utenti sia per i requisiti sia per le prossime fasi del progetto, così come l'invito alla partecipazione nei prossimi incontri dei possibili investitori del progetto.

Infine, per poter sfruttare al meglio il progetto, si è scelti di seguire dei **PMLC model** differenti per ogni macro-requisito. Infatti in questo modo sarà possibile lavorare, per esempio, seguendo un modello **lineare** per implementare dei sistemi già noti, mentre altri sviluppatori lavoreranno seguendo un modello **incrementale**, **iterativo** o addirittura **adattivo** per altri sistemi meno noti o meno semplici.

### Project Scoping Meeting 3

Nel terzo incontro, sia in seguito ad ulteriori feedback da parte di utenti che alle richieste degli investitori, si è deciso di aggiornare la RBS e soprattutto certe user stories, in particolar modo la parte riguardante i **permessi**. Questo incontro infatti ha dato la possibilità di evidenziare quanto sia complesso e pericoloso il mondo dei permessi sui dispositivi IoT per un applicativo che ne gestisce molti.

In tal proposito, si è anche deciso di utilizzare un modello iterativo per il sistema dei permessi piuttosto che uno incrementale, in modo da essere più flessibili sui requisiti se mai dovessero cambiare di nuovo.

### Project Scoping Meeting 4

Nell'ultimo incontro è stato formalizzato il **Project Overview Statement** (POS), in modo da sintetizzare le informazioni più importanti del progetto. Questo incontro ha permesso quindi di stabilire una solida base per l'avanzamento del progetto nelle prossime fasi.

## Planning Process Group

### Joint Project Planning Session (JPPS)

La fase di planning è iniziata con una **Joint Project Planning Session (JPPS)**, una sessione di pianificazione congiunta che ha svolto un ruolo cruciale nella definizione della pianificazione del progetto. L'obiettivo della JPPS era quello di produrre tutti i deliverable necessari per l'avvio del progetto: PDS, WBS, stime di effort/durata/risorse, Project Network Diagram, schedulazione delle attività e stime dei costi.

**Partecipanti:**

- **Facilitator**: responsabile di moderare la sessione e mantenere il focus sugli obiettivi
- **Project Manager**: responsabile della conduzione e del successo del progetto
- **Technographer**: responsabile della registrazione digitale delle decisioni tramite software di PM (MS Project)
- **Core project team**: composto da 2 Senior Developer, 4 Developer, 1 UX/UI Designer e 1 QA Tester
- **IoT Specialist**: esperto del reparto elettronica, con conoscenza approfondita dei dispositivi aziendali
- **Rappresentante del committente (CEO)**: per validare i requisiti e le decisioni di pianificazione
- **Resource Manager**: per fornire visibilità sulle risorse disponibili e sui loro impegni

**Struttura della sessione:**

La sessione è stata articolata in una giornata intera, organizzata come segue:

| Orario        | Durata  | Argomento                                                                                       |
| ------------- | ------- | ----------------------------------------------------------------------------------------------- |
| 09:00 - 09:30 | 30 min  | Kick-off: riepilogo POS, presentazione team, introduzione alla pianificazione                   |
| 09:30 - 11:00 | 90 min  | Elaborazione PDS e validazione/prioritizzazione requisiti (MoSCoW)                              |
| 11:00 - 11:15 | 15 min  | Pausa                                                                                           |
| 11:15 - 13:00 | 105 min | Generazione della WBS a partire dalla RBS                                                       |
| 13:00 - 14:00 | 60 min  | Pausa pranzo                                                                                    |
| 14:00 - 15:30 | 90 min  | Stime di effort, durata e risorse per ogni task della WBS                                       |
| 15:30 - 15:45 | 15 min  | Pausa                                                                                           |
| 15:45 - 17:00 | 75 min  | Costruzione del Project Network Diagram, identificazione del critical path e compressione schedule |
| 17:00 - 17:30 | 30 min  | Stima dei costi, cash flow e management reserve                                                 |
| 17:30 - 18:00 | 30 min  | Sintesi, consenso dei partecipanti e prossimi passi                                             |

**Facility e attrezzature:**

La sessione si è svolta in una sala conferenze ampia e lontana da interruzioni, dotata di:

- Lavagna bianca per la costruzione della WBS tramite sticky notes
- Proiettore per la visualizzazione dei documenti in tempo reale
- Software di project management (MS Project) utilizzato dal Technographer per la registrazione
- Pennarelli colorati per evidenziare le relazioni di dipendenza e il critical path sulla lavagna

**Prioritizzazione MoSCoW:**

Durante la prima parte della sessione il rappresentante del committente ha partecipato alla **prioritizzazione MoSCoW** dei requisiti, classificandoli in:

- **Must have**: R1 (Devices Protocol), R4 (Devices Management), R5 (Devices Registration), R6 (Users Management), R2 (Scripts Management), R3 (Presentation)
- **Should have**: R7 (Permissions Management), R8 (Notifications Management)
- **Could have**: Server cloud come secondo entry point dell'applicativo

Questa prioritizzazione ha guidato l'allocazione delle risorse e la definizione delle dipendenze nella WBS.

**Esito della JPPS:**

Al termine della sessione, tutti i partecipanti hanno raggiunto il **consenso** sulla pianificazione proposta. I deliverable prodotti dalla JPPS includono: il PDS, la WBS completa, le stime di effort e durata, l'assegnamento delle risorse, il Project Network Diagram con il critical path identificato, la schedulazione delle attività e le stime dei costi con il relativo cash flow.

### Project Definition Statement (PDS)

Il **Project Definition Statement (PDS)** è stato elaborato come versione estesa del POS, con lo scopo di assicurare che tutto il team di progetto abbia una **visione comune e dettagliata** degli obiettivi, dei criteri di successo e dei rischi.

Il PDS è stato redatto nella prima parte della JPPS, partendo dal POS già approvato durante lo Scoping e arricchendolo con dettagli emersi durante le discussioni del planning team. Rispetto al POS, il PDS approfondisce in particolar modo:

- Gli **obiettivi**, esplicitando per ciascuno i sottosistemi coinvolti e le relative dipendenze
- I **criteri di successo**, aggiungendo metriche misurabili e tempistiche per la loro verifica
- Le **assunzioni**, estese per includere aspetti tecnici e organizzativi identificati dal core team
- I **rischi e ostacoli**, associando a ciascuno il piano di mitigazione o contingenza già definito nell'analisi dei rischi

### Work Breakdown Structure (WBS)

La **WBS** è stata costruita durante la JPPS utilizzando un approccio **top-down**, partendo direttamente dalla **RBS** precedentemente definita. Per ogni requisito di livello più basso della RBS, si è proceduto a decomporre il lavoro in attività (task) stimabili.

**Approccio scelto:**

Si è utilizzato un approccio ibrido tra **verb-type** (design-build-test) e **organizational** (per sottosistema), dato che il progetto è composto da sottosistemi relativamente indipendenti con PMLC model differenti. Ogni sottosistema è stato decomposto nelle sue attività principali seguendo il ciclo analisi -> progettazione -> implementazione -> test, adattandolo al modello PMLC scelto.

**Criteri di completamento:**

La decomposizione si è fermata quando ogni task soddisfaceva i **6 criteri di completamento** della WBS:

1. Lo stato e il completamento del task sono misurabili (utilizzando la Definition of Done già definita)
2. Il task ha un inizio e una fine ben definiti
3. Il task ha un deliverable associato
4. Tempi e costi sono facilmente stimabili
5. La durata del task è entro un limite accettabile (massimo 4 settimane)
6. Il task è indipendente e può essere svolto senza interruzioni significative

Inoltre, per i sottosistemi con PMLC **adattivo** (Devices Protocol e Scripts Management), si è utilizzato anche il **7° criterio** suggerito da Wysocki: essendo previsti cambiamenti di scope, la WBS per questi sottosistemi è stata definita a un livello di dettaglio leggermente inferiore, accettando che verrà raffinata nelle iterazioni successive. Questo è coerente con la scelta del modello adattivo, in cui la pianificazione è iterativa nel tempo.

**Approccio di costruzione:**

Il team è stato suddiviso in **sub-team** secondo le competenze specifiche (**Subteam Approach**). Ogni sub-team ha lavorato alla decomposizione del proprio sottosistema di competenza (per esempio, lo specialista IoT e il Senior Developer 1 hanno lavorato sul Devices Protocol), per poi ri-unirsi e consolidare la WBS complessiva aggiungendo le attività di integrazione e testing trasversali (nodo 1.10 della WBS).

Oltre ai sottosistemi derivati dalla RBS, è stato aggiunto un nodo per il **Project Management** (1.1) che comprende le attività di pianificazione, monitoraggio e chiusura, e un nodo per il **Testing e Integrazione** (1.10) che comprende le attività di test trasversali a tutti i sottosistemi.

### Stime di Effort e Durata

Le stime di effort e durata sono state effettuate a livello di singolo task della WBS durante la JPPS. Si sono utilizzate diverse **tecniche di stima** in base alla natura del task:

- **Giudizio di esperti**: utilizzato per i task più semplici e ben compresi, dove il team aveva esperienza diretta da progetti precedenti (per esempio, il sottosistema Users Management e Notifications Management)
- **Tecnica Three-Point**: utilizzata per i task con maggiore incertezza, calcolando la durata attesa come $E = \frac{O + 4M + P}{6}$ dove $O$ è la stima ottimistica, $M$ la più probabile e $P$ la pessimistica. Questa tecnica è stata applicata in particolare per i sottosistemi con PMLC adattivo e iterativo
- **Analisi di dati storici**: utilizzata dove possibile, confrontando con task simili svolti in progetti passati della SDA Corporation

Si è tenuto conto che in media un individuo lavora al **75% di efficienza** a causa di interruzioni non pianificate, meeting e attività amministrative. Pertanto le stime di effort sono state calibrate di conseguenza.

Le stime sono espresse in **settimane** come unità temporale, scelta che risulta adeguata per un progetto di queste dimensioni (circa 12 mesi). Per ogni task si è stimata sia la **durata** (elapsed time, necessaria per la schedulazione) sia l'**effort** (labor, necessario per il calcolo dei costi e l'assegnamento delle risorse), tenendo presente che la relazione tra le due non è lineare.

### Assegnamento delle Risorse

L'assegnamento delle risorse è stato effettuato utilizzando una **matrice competenze-necessità** (skill-need matrix), incrociando le competenze richieste da ogni task della WBS con le competenze disponibili nel team.

Si è scelto un team di 10 persone, di cui 9 a tempo pieno e 1 part-time (IoT Specialist dal reparto elettronica). Il team è stato organizzato secondo una **struttura a matrice**, in cui le risorse sono condivise tra i vari sottosistemi in base alle necessità, mantenendo il Project Manager come punto di riferimento centrale.

Dopo l'assegnamento iniziale si è proceduto al **resource leveling** per risolvere eventuali conflitti di allocazione, utilizzando MS Project. In alcuni casi è stato accettato un leggero allungamento di task non critici (con slack positivo) per evitare il sovraccarico di risorse.

### Project Network Diagram e Critical Path

Il **Project Network Diagram** è stato costruito utilizzando il formato **Task on the Node**, partendo dalla WBS e definendo le **relazioni di dipendenza** tra i task.

**Tipologie di dipendenze utilizzate:**

Per la prima pianificazione si sono utilizzate esclusivamente dipendenze di tipo **Finish-to-Start (FS)**, come suggerito dalle best practice, in quanto più semplici da gestire e da comprendere. In fase di compressione della schedule, alcune dipendenze FS sono state convertite in **Start-to-Start (SS)** dove possibile per consentire la parallelizzazione.

**Vincoli di dipendenza identificati:**

- **Vincoli tecnici**: il protocollo (R1) deve essere completato prima dell'implementazione della comunicazione con i dispositivi; il sottosistema utenti (R6) deve essere completato prima dell'implementazione dei permessi (R7); il motore di esecuzione script deve essere completato prima dell'implementazione delle notifiche sugli errori script
- **Vincoli discrezionali**: si è scelto di completare il testing di ogni sottosistema prima di procedere all'integrazione
- **Vincoli di best practice**: la progettazione del linguaggio a blocchi prima della sua implementazione; la selezione del design system prima dell'implementazione delle pagine

**Critical Path:**

Attraverso il **forward pass** e il **backward pass** sul network diagram, è stato identificato il **critical path** del progetto, che attraversa i seguenti sottosistemi:

**Pianificazione → Devices Protocol (completo) → Devices Management (completo) → Presentation (pagine utente e admin) → Collegamento Frontend-Backend → Test di Integrazione → Test End-to-End → Beta Testing → Correzione Bug → Chiusura**

Questo percorso critico evidenzia come il **Devices Protocol** sia il primo collo di bottiglia del progetto, coerentemente con quanto definito nel POS e nel terzo Project Scoping Meeting come "pilastro portante del progetto". Il secondo punto critico è il **Presentation Subsystem**, che dipende dal completamento di più sottosistemi (Devices Management, Permissions, Notifications).

È stata inoltre calcolata la **slack time** (float) per ogni task non critico, evidenziando che:

- I sottosistemi con maggiore slack sono il **Permissions Management** (fino a 21 settimane per la fase di progettazione) e il **Devices Registration** (12 settimane), il che offre flessibilità nella loro schedulazione
- Il sottosistema **Notifications** ha uno slack molto basso (1 settimana per le fasi finali), il che suggerisce di monitorarlo con attenzione
- Il sottosistema **Scripts Management** parte con uno slack elevato ma lo perde man mano che si avvicina all'integrazione con il protocollo

La durata totale del progetto risultante dal critical path è di **54 settimane** (circa 12,5 mesi).

### Compressione della Schedule

In fase di analisi della schedule si è valutata la possibilità di **comprimere** la durata del progetto. Sono state adottate le seguenti strategie:

- **Parallelizzazione**: ovvero la sostituzione di dipendenze FS con dipendenze SS dove tecnicamente possibile. Per esempio, l'editor visuale (1.6.2) e il motore di esecuzione (1.6.3) del sottosistema Scripts sono stati parallelizzati in quanto indipendenti tra loro
- **Assegnazione di membri più esperti ai task critici**: il Senior Developer 1 è stato assegnato ai task del critical path relativi al protocollo e il QA Tester è stato dedicato alla fase di testing
- **Possibilità di spostamento risorse**: risorse da task non critici (con slack elevato) possono essere spostate verso task nel critical path in caso di ritardi durante l'esecuzione

Non si è proceduto ad una compressione aggressiva, seguendo il principio che "la compressione non è mai gratis": ridurre i tempi non riduce il lavoro, e può aumentare costi, rischi e complessità di coordinamento.

### Management Reserve

È stata inserita una **management reserve** pari a **3 settimane** (~5,5% della durata complessiva), aggiunta come buffer prima della chiusura del progetto. Questa riserva è stata dimensionata tenendo conto:

- Della presenza di sottosistemi con PMLC adattivo, che hanno una probabilità intrinsecamente più alta di ritardi e cambiamenti di scope
- Dell'esperienza di progetti precedenti della SDA Corporation
- Del livello medio-basso dei rischi identificati nell'analisi dei rischi

La riserva verrà gestita come una "**scope bank**": eventuali ritardi sui task saranno assorbiti dalla riserva senza impattare la data di consegna prevista, finché questa non si esaurisce. Il consumo della riserva sarà monitorato attentamente durante la fase di Monitoring & Controlling.

La durata totale del progetto **inclusa la management reserve** è pertanto di **57 settimane** (~13 mesi).

### Stime dei Costi e Cash Flow

I **costi del progetto** sono stati stimati partendo dall'assegnamento delle risorse ai task della WBS, moltiplicando il costo settimanale lordo di ogni risorsa per le settimane di impegno previste. A questi costi di personale sono stati aggiunti i costi per infrastruttura, licenze software, dispositivi IoT per il testing e le spese generali aziendali.

**Tipologia di stima**: si è utilizzata una **budget estimate**, considerata adeguata per questa fase di pianificazione. Stime più definitive verranno prodotte all'avvio di ogni fase del progetto, come richiesto dai modelli incrementali e adattivi.

**Cash flow**: è stato elaborato un piano di cash flow che confronta le **entrate (inflow)** e le **uscite (outflow)** del progetto su base trimestrale. Le entrate sono state pianificate secondo il contratto con gli investitori, che prevede:

- **Anticipo** alla firma del contratto (15% del budget totale)
- **Pagamenti a milestone** al completamento di determinate fasi (Protocol completato, primo prototipo funzionante, beta release)
- **Saldo** all'accettazione finale del progetto

Si è optato per un **contratto a corpo (fixed-price)** per le parti con PMLC lineare e incrementale, dove le stime sono più affidabili, e un **contratto a consuntivo (time & materials)** con tetto massimo per le parti con PMLC adattivo, dove le stime sono meno attendibili e il rischio di sforamento è più alto.

Il costo totale stimato del progetto è di circa **€460.000**, ben al di sotto del vincolo di budget di €2M definito nelle COS, lasciando un margine significativo per eventuali imprevisti.

### Project Proposal

Al termine della JPPS, è stata redatta una **Project Proposal** che sintetizza l'intera pianificazione del progetto per ottenere l'**approvazione formale** da parte del senior management e degli investitori. La proposta è strutturata come segue:

- **Executive Summary**: sintesi del progetto, dei costi e dei tempi
- **Background**: contesto aziendale e motivazioni del progetto (riferimento allo stato AS IS/TO BE)
- **Objective**: obiettivi del progetto (riferimento al POS/PDS)
- **Overview of Approach**: panoramica dell'approccio di gestione, inclusi i PMLC model scelti e la motivazione per ciascuno
- **Detailed Statement of Work**: WBS completa con stime e schedulazione
- **Time and Cost Summary**: durata totale (57 settimane inclusa management reserve), costo totale (~€460.000), cash flow previsto
- **Appendici**: analisi dei rischi, diagrammi di rete, tabelle di assegnamento risorse

La proposta è stata **approvata** dal senior management dopo una presentazione e una breve sessione di Q&A, con la raccomandazione di monitorare con particolare attenzione i sottosistemi con PMLC adattivo (Devices Protocol e Scripts Management) e di utilizzare la management reserve con parsimonia.

