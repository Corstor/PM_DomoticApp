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
  - [Launching Process Group](#launching-process-group)
    - [Reclutamento e bilanciamento del team](#reclutamento-e-bilanciamento-del-team)
    - [Kick-Off Meeting](#kick-off-meeting)
    - [Matrice RASCI](#matrice-rasci)
    - [Regole operative del team](#regole-operative-del-team)
      - [Problem Solving](#problem-solving)
      - [Decision Making](#decision-making)
      - [Conflict Resolution](#conflict-resolution)
      - [Consensus Building](#consensus-building)
      - [Brainstorming](#brainstorming)
      - [Team Meetings](#team-meetings)
    - [Gestione dei cambiamenti di scope](#gestione-dei-cambiamenti-di-scope)
    - [Gestione delle comunicazioni](#gestione-delle-comunicazioni)
    - [Work Packages](#work-packages)
    - [Finalizzazione della schedule](#finalizzazione-della-schedule)
  - [Monitoring e Controlling Process Group](#monitoring-e-controlling-process-group)
    - [Sistema di reporting](#sistema-di-reporting)
    - [Strumenti di reporting visuale](#strumenti-di-reporting-visuale)
    - [Gestione della Scope Bank](#gestione-della-scope-bank)
    - [Issues Log](#issues-log)
    - [Project Status Meetings](#project-status-meetings)
    - [Acquisizione dell'approvazione a chiudere](#acquisizione-dellapprovazione-a-chiudere)

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

| Orario        | Durata  | Argomento                                                                                          |
| ------------- | ------- | -------------------------------------------------------------------------------------------------- |
| 09:00 - 09:30 | 30 min  | Kick-off: riepilogo POS, presentazione team, introduzione alla pianificazione                      |
| 09:30 - 11:00 | 90 min  | Elaborazione PDS e validazione/prioritizzazione requisiti (MoSCoW)                                 |
| 11:00 - 11:15 | 15 min  | Pausa                                                                                              |
| 11:15 - 13:00 | 105 min | Generazione della WBS a partire dalla RBS                                                          |
| 13:00 - 14:00 | 60 min  | Pausa pranzo                                                                                       |
| 14:00 - 15:30 | 90 min  | Stime di effort, durata e risorse per ogni task della WBS                                          |
| 15:30 - 15:45 | 15 min  | Pausa                                                                                              |
| 15:45 - 17:00 | 75 min  | Costruzione del Project Network Diagram, identificazione del critical path e compressione schedule |
| 17:00 - 17:30 | 30 min  | Stima dei costi, cash flow e management reserve                                                    |
| 17:30 - 18:00 | 30 min  | Sintesi, consenso dei partecipanti e prossimi passi                                                |

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

- **Giudizio di esperti**: utilizzato per i task più semplici e ben compresi, dove il team aveva esperienza diretta da progetti precedenti (per esempio, il sottosistema Users Management e Notifications Management).
- **Tecnica Three-Point**: utilizzata per i task con maggiore incertezza, calcolando la durata attesa come E = (O + 4M + P) / 6, dove O è la stima ottimistica, M la più probabile e P la pessimistica. Questa tecnica è stata applicata in particolare per i sottosistemi con PMLC adattivo e iterativo.
- **Analisi di dati storici**: utilizzata dove possibile, confrontando con task simili svolti in progetti passati della SDA Corporation.

Si è tenuto conto che in media un individuo lavora al **75% di efficienza** a causa di interruzioni non pianificate, meeting e attività amministrative. Pertanto le stime di effort sono state calibrate di conseguenza.
****
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

## Launching Process Group

Il **Launching Process Group** rappresenta il passaggio dalla pianificazione all'esecuzione vera e propria del progetto. In questa fase si sono affrontate tutte le attività necessarie per mettere il team nella condizione di lavorare efficacemente: dal completamento del reclutamento, al kick-off meeting, alla definizione delle regole operative, fino alla predisposizione dei processi di gestione dei cambiamenti di scope, delle comunicazioni e dei work packages.

Essendo il progetto nato **internamente** alla SDA Corporation su iniziativa del CEO per rispondere ai feedback degli utenti, non esiste un committente esterno in senso tradizionale. Il ruolo che in un progetto commissionato sarebbe svolto dal cliente è qui ricoperto dal **CEO** stesso, che agisce come **sponsor interno** del progetto: è lui ad aver promosso l'iniziativa, a validare le decisioni di scope e ad approvare i deliverable alle milestone. Gli **investitori** rappresentano invece la parte finanziaria esterna.

### Reclutamento e bilanciamento del team

Il **core team** (PM, SD1, SD2) era già stato selezionato prima della fase di Planning e aveva partecipato alla JPPS. Per la fase di Launching si è completato il reclutamento del **developer team** (D1, D2, D3, D4), del **designer UX** e dello **specialista QA**, oltre alla formalizzazione del contratto part-time con lo **specialista IoT** come risorsa esterna (contracted team).

Per il bilanciamento del team si è fatto riferimento alla classificazione dei **learning styles di David Kolb**, cercando di avere una rappresentanza equilibrata dei quattro stili:

- **Assimilating**: QA e SD2, con la loro capacità di analisi strutturata e modellazione dei problemi
- **Diverging**: UX e lo specialista IoT, per la loro propensione a vedere alternative e prospettive non convenzionali
- **Accommodating**: D1, D2, D3 e D4, orientati all'azione e alla realizzazione concreta dei task
- **Converging**: SD1 e PM, capaci di individuare la soluzione migliore tra le alternative e guidare le scelte tecniche

Questo bilanciamento si è rivelato particolarmente utile per i sottosistemi con PMLC **adattivo** (Devices Protocol e Scripts Management), dove la capacità di esplorare alternative (Diverging) e convergere verso soluzioni concrete (Converging) è fondamentale nel ciclo iterativo.

### Kick-Off Meeting

Il **Project Kick-Off Meeting** è stato organizzato come evento formale per annunciare al team completo e agli stakeholder che il progetto è stato approvato e sta entrando nella fase esecutiva.

**Agenda del kick-off meeting:**

| Orario        | Durata | Argomento                                                      |
| ------------- | ------ | -------------------------------------------------------------- |
| 09:00 - 09:15 | 15 min | Introduzione e presentazione dello sponsor al team             |
| 09:15 - 09:30 | 15 min | Presentazione degli aspetti rilevanti del progetto (sponsor)   |
| 09:30 - 09:50 | 20 min | Presentazione del progetto e delle aspettative aziendali (CEO) |
| 09:50 - 10:20 | 30 min | Presentazione del progetto e del piano (Project Manager)       |
| 10:20 - 10:40 | 20 min | Presentazione dei membri del team e dei ruoli assegnati        |
| 10:40 - 10:50 | 10 min | Pausa                                                          |
| 10:50 - 11:20 | 30 min | Revisione del PDS con il team completo                         |
| 11:20 - 12:00 | 40 min | Definizione delle regole operative del team                    |
| 12:00 - 12:30 | 30 min | Integrazione nella schedule delle disponibilità dei membri     |
| 12:30 - 13:00 | 30 min | Identificazione e assegnazione dei work packages iniziali      |

Durante il meeting, il PM ha presentato il **PDS** all'intero team, dando a tutti la possibilità di approfondire e porre domande. Il PDS è servito come **punto di riferimento condiviso** per chiarire scope, obiettivi, vincoli e rischi del progetto, ed è stato particolarmente utile per i nuovi membri del developer team che non avevano partecipato alla JPPS.

### Matrice RASCI

Per l'assegnazione delle responsabilità si è adottata una **matrice RASCI** (Responsible, Accountable, Support, Consulted, Informed), che definisce chiaramente per ogni macro-attività della WBS chi ne è **responsabile**, chi ne **approva** il risultato, chi **supporta**, chi viene **consultato** e chi deve essere **informato**.

La scelta della matrice RASCI rispetto a una più semplice RACI è motivata dalla presenza di sottosistemi con PMLC differenti: nei sottosistemi adattivi, il ruolo di **Support** è particolarmente rilevante perché le risorse devono essere flessibili e pronte a intervenire su task che emergono durante le iterazioni. Per i sottosistemi lineari, la matrice risulta più statica e definita fin dall'inizio.

Il **PM** risulta **Accountable** per tutte le macro-attività, garantendo controllo e coerenza complessiva. I Senior Developer sono tipicamente **Consulted** anche sui sottosistemi di cui non sono direttamente responsabili, per assicurare coerenza architetturale.

### Regole operative del team

Durante il kick-off meeting sono state concordate le **regole operative** che il team seguirà durante l'esecuzione del progetto. Ogni aspetto è stato discusso e formalizzato per evitare ambiguità e garantire un processo decisionale efficiente.

#### Problem Solving

Per la risoluzione dei problemi si è adottato il modello dei **cinque passi di Daniel Couger**:

1. Definire il problema e identificarne il "proprietario" (owner)
2. Raccogliere i dati rilevanti e analizzare le cause
3. Generare delle idee (tramite brainstorming o analisi individuale)
4. Valutare e assegnare una priorità alle idee
5. Sviluppare un piano d'azione

Se la soluzione non si rivela soddisfacente, il processo viene ripetuto. Questa struttura è stata scelta perché fornisce un **framework chiaro e ripetibile**, adatto sia ai sottosistemi lineari (dove i problemi tendono ad essere più tecnici e circoscritti) sia a quelli adattivi (dove i problemi possono riguardare la definizione stessa della soluzione).

#### Decision Making

Per il decision making si è scelto un approccio **misto** in base al contesto:

- **Directive**: il PM prende le decisioni in autonomia per questioni di gestione progetto (scheduling, allocazione risorse, gestione della riserva) e per decisioni urgenti che non possono attendere una consultazione
- **Participative/Collaborative**: utilizzato durante le sessioni di planning delle iterazioni per i sottosistemi adattivi (Devices Protocol e Scripts Management), dove è fondamentale il contributo di tutti per convergere verso la soluzione migliore
- **Consultative**: utilizzato per le decisioni architetturali significative, dove il PM o il Senior Developer responsabile decidono dopo aver raccolto input dal team

Nella scelta degli stili si è fatto riferimento alle **sei fasi del processo decisionale di Wysocki**, che collegano ciascuna fase a uno stile di apprendimento di Kolb: dalla definizione della situazione (Assimilator), alla generazione di alternative (Diverger), alla valutazione e scelta (Converger), alla pianificazione dell'azione (Converger), alla valutazione del processo (Accommodator), fino alla valutazione dei risultati (Assimilator). Questo collegamento ha aiutato a capire quali membri del team coinvolgere in quale fase del processo decisionale.

#### Conflict Resolution

Per la gestione dei conflitti si è fatto riferimento al modello di **Thomas-Kilmann**, che identifica cinque approcci in base al grado di assertività e cooperatività. Il team ha concordato di privilegiare l'approccio **Collaborating** (integrativo) come prima scelta, cercando soluzioni win-win. In caso di disaccordo persistente su scelte tecniche, si ricorre al **Compromising** per trovare soluzioni accettabili per entrambe le parti. L'approccio **Competing** è riservato al PM solo per situazioni critiche dove è necessaria una decisione rapida per non bloccare il progetto.

Si è anche concordato che l'approccio **Avoiding** non è accettabile: i conflitti vanno affrontati tempestivamente per evitare che si accumulino e compromettano la collaborazione.

#### Consensus Building

Il team ha adottato la regola secondo cui il **consenso** è la modalità preferita per le decisioni importanti, ma con la consapevolezza — come avverte Wysocki — che un consenso che soddisfa ugualmente tutte le parti potrebbe non essere sempre la decisione migliore. Pertanto, quando il consenso non viene raggiunto in tempi ragionevoli, si passa all'approccio **consultativo** e il PM o il Senior Developer di riferimento prendono la decisione finale informata dal confronto avvenuto.

#### Brainstorming

Le sessioni di **brainstorming** sono state previste come strumento regolare, in particolare durante:

- Le sessioni di sprint planning per i sottosistemi adattivi
- La fase di generazione idee nel processo di problem solving
- Le situazioni in cui è necessario esplorare alternative architetturali o di design

Le regole concordate per il brainstorming prevedono: riunire chi ha conoscenza dell'ambito, raccogliere tutte le idee senza giudizio iniziale, continuare fino ad esaurimento idee, discutere tutte le idee con estrema apertura mentale, e solo infine convergere verso la soluzione.

#### Team Meetings

Per le riunioni di progetto sono state definite **tre tipologie** con regole precise:

**Daily Status Meeting** (15 minuti, in piedi):
- Si discutono solo i task aperti e non ancora completati
- Ogni responsabile riporta lo stato di avanzamento con una delle quattro formulazioni standard: "In schedule", "In ritardo di X, ma rientrerò entro Y", "In ritardo, ho bisogno di aiuto", "In anticipo, posso aiutare"
- I problemi non vengono risolti durante il daily ma vengono segnalati per essere affrontati in una riunione dedicata

**Problem Resolution Meeting** (durata variabile, su richiesta):
- Partecipa solo chi è coinvolto nel problema specifico
- Si identifica l'owner del problema, si definisce la soluzione e si stabiliscono i criteri per verificare che il problema sia effettivamente risolto
- Segue il modello dei cinque passi di Couger

**Project Review Meeting** (evento formale, a ogni milestone):
- Partecipano PM, senior management, committente, sponsor e stakeholder
- Si presenta lo stato del progetto alla milestone raggiunta con una revisione critica
- Si propongono eventuali azioni correttive

Per la gestione delle riunioni si è concordato di seguire le **linee guida before/during/after**: preparare sempre un'agenda e distribuirla in anticipo, rispettare rigorosamente i tempi, assegnare azioni specifiche con responsabili, e redigere un verbale con le decisioni prese e i punti ancora aperti.

### Gestione dei cambiamenti di scope

La gestione dei cambiamenti di scope è un aspetto critico considerando che il progetto include sottosistemi con PMLC **adattivo e iterativo**, dove i cambiamenti di scope sono attesi e fanno parte del processo.

**Processo adottato:**

Si è formalizzato un processo a 6 step:

1. **Sottomissione** della richiesta di cambiamento tramite un **Scope Change Request Form** (compilato dal richiedente)
2. **Revisione** iniziale della richiesta da parte del PM (accettata per valutazione, rigettata o rinviata al richiedente per rielaborazione)
3. **Studio di impatto** (Project Impact Statement) a cura del PM e del team, che analizza l'impatto su costi, schedule, qualità, risorse e rischio
4. **Revisione** dello studio di impatto con il CEO e il senior management
5. **Decisione** (approvazione, rinvio o rigetto)
6. **Ristrutturazione** del piano di progetto in caso di approvazione

**Differenziazione per PMLC model:**

Per i sottosistemi con PMLC **lineare** (Users Management, Notifications Management), i cambiamenti di scope sono gestiti con maggior rigore: ogni richiesta segue l'intero processo formale e i cambiamenti vengono approvati solo se assolutamente necessari.

Per i sottosistemi con PMLC **adattivo** (Devices Protocol, Scripts Management), i cambiamenti di scope sono parte integrante del ciclo: al termine di ogni iterazione si rivaluta lo scope alla luce di quanto appreso, e i cambiamenti vengono processati come parte naturale del ciclo plan-do-check. Per questi sottosistemi si è predisposta una **Scope Bank**, un registro dove "depositare" i requisiti non ancora integrati nella soluzione, con una priorità assegnata, da cui pescare nelle iterazioni successive.

**Management reserve per i cambiamenti di scope:**

Come già definito nel planning, le 3 settimane di management reserve (circa il 5.5% della durata del critical path) sono disponibili anche per assorbire l'impatto dei cambiamenti di scope approvati. La gestione della riserva è centralizzata nel PM.

### Gestione delle comunicazioni

La gestione delle comunicazioni è stata pianificata definendo **timing**, **contenuti** e **canali** per ogni tipo di comunicazione di progetto.

**Canali scelti:**

- **Comunicazioni one-to-one (two-way)**: riunioni in presenza e videochiamate per discussioni tecniche complesse, revisioni di design e risoluzione di problemi
- **Comunicazioni elettroniche (two-way)**: piattaforma di messaggistica aziendale per le comunicazioni rapide e quotidiane, repository Git con code review per le comunicazioni relative al codice, tool di project management per l'aggiornamento dello stato dei task
- **Comunicazioni scritte (one-way)**: report di avanzamento settimanali per gli stakeholder, email formali per le comunicazioni con il senior management e con gli investitori, documentazione tecnica su wiki condivisa

**Interfacce di comunicazione:**

Il PM è il **nodo centrale** delle comunicazioni, interfacciandosi con: il CEO (per le decisioni di scope e le approvazioni), gli investitori (per gli aspetti economici e le milestone), il senior management (per i report di stato), i team manager/Senior Developer (per il coordinamento tecnico), e i singoli membri del team (per il supporto operativo).

Per i sottosistemi adattivi, il CEO (o un suo delegato del reparto IT) partecipa attivamente alle **review di iterazione**, fornendo feedback diretto che alimenta la pianificazione dell'iterazione successiva. Per i sottosistemi lineari, la comunicazione con il CEO avviene principalmente alle milestone pianificate.

### Work Packages

I **work packages** sono stati scritti per fornire una descrizione dettagliata di come i task verranno completati, aumentando il controllo sul progetto e il rispetto della schedule.

**Criteri di selezione:**

I work packages sono stati redatti prioritariamente per:

- I task sul **critical path** (Devices Protocol, Devices Management, Presentation), dove un ritardo impatta direttamente sulla data di fine progetto
- I task ad **alto rischio** (in particolare quelli relativi ai sottosistemi adattivi)
- I task che richiedono risorse **scarse** (lo specialista IoT part-time)
- I task con **elevata varianza** nella stima della durata
- I task che consentono il raggiungimento di una **milestone** contrattuale
- I task che **condividono risorse** e dove il coordinamento è critico

Per ogni work package è stato compilato un **Work Package Assignment Sheet** (che assegna il responsabile e le risorse) e un **Work Package Description Form** (che descrive le attività, i deliverable attesi, i criteri di accettazione e le dipendenze).

### Finalizzazione della schedule

La schedule definita durante il planning è stata **integrata con le disponibilità effettive** dei membri del team. In particolare:

- Lo **specialista IoT** ha comunicato la sua disponibilità part-time (3 giorni/settimana), che era già stata considerata nelle stime
- Due developer (D3 e D4) hanno comunicato alcune settimane di indisponibilità per impegni su altri progetti, richiedendo un **ribilanciamento** di alcuni task non critici sfruttando gli slack disponibili

Per le risorse in **over-allocation** si è intervenuti con le seguenti strategie, in ordine di preferenza:

1. **Utilizzo degli slack**: spostare i task non critici all'interno del loro margine di float
2. **Decomposizione ulteriore dei task**: suddividere task grandi in parti più piccole assegnabili a risorse diverse
3. **Sostituzione di risorse**: assegnare risorse alternative con competenze comparabili
4. **Allungamento della durata**: estendere la durata di un task riducendo l'impegno settimanale della risorsa (senza modificare l'effort totale)

Non è stato necessario ricorrere allo straordinario né far slittare la data di fine progetto, grazie agli ampi margini di slack presenti nei percorsi non critici della schedule.

## Monitoring e Controlling Process Group

Il **Monitoring e Controlling Process Group** ha lo scopo di mantenere il progetto allineato al piano approvato, raccogliendo informazioni sullo stato di avanzamento, intercettando tempestivamente gli scostamenti e attivando le azioni correttive necessarie.

### Sistema di reporting

Per effettuare in modo efficiente il reporting sull'avanzamento del progetto ci si è dotati di un **Progress Reporting System** con le seguenti caratteristiche (come indicato da Wysocki):

- Fornisce informazioni sullo stato di avanzamento **tempestive, complete e accurate**
- Non richiede un overhead eccessivo per il suo utilizzo, così da non essere controproducente
- Il reporting è **intuitivo e facilmente accettabile** da parte del team e del senior management
- Il sistema è un efficace strumento di **early warning** per intercettare tempestivamente eventuali problemi

Si sono adottati quattro tipi di report: **Current Period Reports**, **Cumulative Reports**, **Exception Reports** e **Variance Reports**.

La scelta di questi quattro tipi nasce dalla necessità di rivolgersi a **destinatari diversi**: il team necessita di report operativi e dettagliati (Current Period, Variance), mentre il CEO e gli investitori necessitano di report sintetici e ad alto livello (Exception). I Cumulative Reports servono ad entrambi per comprendere il trend complessivo del progetto.

**Aggiornamento delle informazioni:**

Si è stabilito di aggiornare le informazioni con **cadenza settimanale**, in un giorno e orario fissi. Per ogni periodo vengono riportati: il lavoro effettivamente svolto, i dati storici sull'eseguito, le stime aggiornate sulle attività rimanenti, le date di inizio e fine di ciascuna attività iniziata o terminata, i giorni già impegnati e quelli previsti per il completamento, le risorse consumate e quelle rimanenti, e la **percentuale di completamento** di ogni task attivo.

### Strumenti di reporting visuale

**Gantt Chart Project Status Report:**

Il Gantt chart aggiornato con lo stato di avanzamento è il principale strumento visuale per confrontare il pianificato con l'eseguito. Mostra per ogni task la barra pianificata e il progresso effettivo, rendendo immediatamente visibili i task in ritardo o in anticipo.

**Milestone Trend Charts:**

I **Milestone Trend Chart** (cumulative report) sono stati scelti per tracciare l'andamento delle milestone nel tempo. Ad ogni periodo di reporting si riporta la data prevista per ciascuna milestone: se la curva tende verso l'alto, la milestone sta slittando; se è stabile o tende verso il basso, il progetto è sotto controllo. Questo strumento è particolarmente utile per le comunicazioni con il CEO e gli investitori poiché offre una visione sintetica e immediata della salute del progetto.

**Earned Value Analysis (EVA):**

L'Earned Value Analysis è stata applicata per misurare le performance del progetto in termini economici. Si basa su tre grandezze fondamentali:

- **PV** (Planned Value): il valore del lavoro pianificato alla data di rilevazione
- **EV** (Earned Value): il valore del lavoro effettivamente completato
- **AC** (Actual Cost): il costo effettivamente sostenuto

Da queste si derivano due indici fondamentali:

- **SPI** (Schedule Performance Index) = EV / PV — fornisce una misura di come il progetto sta performando rispetto a quanto pianificato. Un valore < 1 indica ritardo, > 1 indica anticipo
- **CPI** (Cost Performance Index) = EV / AC — fornisce una misura di come i costi del lavoro svolto evolvono rispetto ai costi stimati. Un valore < 1 indica superamento del budget, > 1 indica risparmio

### Gestione della Scope Bank

La **Scope Bank**, già predisposta durante il Launching, viene gestita attivamente durante il monitoring e funziona come un vero e proprio "deposito" di tempo:

- Il tempo necessario per processare e integrare una richiesta di modifica dello scope è **attinto dalla Scope Bank**
- Per aggiungere tempo alla Scope Bank è necessario **rimuovere delle funzionalità/feature** e depositare il tempo che sarebbe stato richiesto per il loro sviluppo
- Se si **risparmia del tempo** nell'esecuzione di qualche attività, lo si può aggiungere alla Scope Bank
- Il CEO (nel ruolo di sponsor interno) **ridefinisce continuamente le priorità** del contenuto della Scope Bank

Questo meccanismo è coerente con i sottosistemi adattivi (Devices Protocol e Scripts Management), dove lo scope viene rivalutato ad ogni iterazione e la Scope Bank funge da contenitore dei requisiti non ancora integrati, prioritizzati dallo sponsor.

### Issues Log

L'**Issues Log** è un documento dinamico che contiene tutti i problemi emersi durante il progetto, in particolare quelli non ancora risolti. La sua risoluzione è fondamentale per la continuazione e il successo del progetto.

Per ogni issue vengono registrate le seguenti informazioni: **ID Number**, **data di apertura**, descrizione del **problema**, descrizione dell'**impatto** sul progetto se non viene risolto, **proprietario** del problema (problem owner), **azione da intraprendere**, **stato** e **esito**. L'Issues Log è anche una preziosa fonte di **dati storici** per progetti futuri.

L'Issues Log viene aggiornato durante i **daily status meeting** e nei **Problem Management Meeting**, garantendo che nessun problema venga dimenticato o trascurato.

### Project Status Meetings

Per il monitoraggio si sono utilizzati due tipi di meeting, già definiti nel Launching:

**15-Minute Daily Status Meeting:**

Partecipa l'intero team (o solo i task manager responsabili dei task in lavorazione). Sono riunioni **in piedi** e un facilitatore guida la discussione. Per ciascun task attivo viene riportato sinteticamente lo stato: "in schedula", "in anticipo rispetto alla schedula" (specificando di quanto), oppure "in ritardo rispetto alla schedula" (specificando di quanto e se c'è bisogno di aiuto). Al termine si aggiornano la **Scope Bank** e l'**Issues Log**.

**Problem Management Meeting:**

Partecipano solo i **membri del team coinvolti** nel problema. Si concorda la definizione del problema, si identifica il **proprietario**, si effettua un **brainstorming** per la soluzione, si assegna una priorità alle soluzioni individuate, e si aggiorna l'Issues Log. Se necessario, si pianifica un meeting successivo.

### Acquisizione dell'approvazione a chiudere

Quando tutti i **criteri di accettazione** previsti per la soluzione sono stati soddisfatti, il PM acquisisce l'approvazione formale dal CEO per chiudere il progetto e passare alla **fase di chiusura** (Closing Process Group).

