# Indice

- [Indice](#indice)
- [Documentazione di progetto](#documentazione-di-progetto)
  - [Analisi dello stato](#analisi-dello-stato)
    - [AS IS](#as-is)
    - [TO BE](#to-be)
    - [NICE TO HAVE](#nice-to-have)
  - [Condictions of Satisfaction (COS)](#condictions-of-satisfaction-cos)
  - [Project Overview Statement (POS)](#project-overview-statement-pos)
    - [Analisi dei Rischi](#analisi-dei-rischi)
      - [Rischi tecnici](#rischi-tecnici)
      - [Rischi di gestione progetto](#rischi-di-gestione-progetto)
      - [Rischi di organizzazione](#rischi-di-organizzazione)
      - [Piani di contingenza](#piani-di-contingenza)
  - [Requirements Breakdown Structure (RBS)](#requirements-breakdown-structure-rbs)
  - [User Stories](#user-stories)
    - [Definition of Done](#definition-of-done)
  - [Modello PMLC](#modello-pmlc)
    - [Users Management Subsystem](#users-management-subsystem)
    - [Devices Management Subsystem](#devices-management-subsystem)
    - [Devices Protocol](#devices-protocol)
    - [Devices Registration Subsystem](#devices-registration-subsystem)
    - [Scripts Management Subsystem](#scripts-management-subsystem)
    - [Permissions Management Subsystem](#permissions-management-subsystem)
    - [Notifications Management Subsystem](#notifications-management-subsystem)
    - [Presentation Subsystem](#presentation-subsystem)
  - [Project Definition Statement (PDS)](#project-definition-statement-pds)
  - [Work Breakdown Structure (WBS)](#work-breakdown-structure-wbs)
  - [Stime di Effort e Durata](#stime-di-effort-e-durata)
  - [Assegnamento delle Risorse](#assegnamento-delle-risorse)
  - [Project Network Diagram](#project-network-diagram)
  - [Critical Path e Schedule](#critical-path-e-schedule)
  - [Stime dei Costi](#stime-dei-costi)
  - [Cash Flow](#cash-flow)
  - [Project Proposal](#project-proposal)
    - [Executive Summary](#executive-summary)
    - [Background](#background)
    - [Objective](#objective)
    - [Overview of Approach](#overview-of-approach)
    - [Time and Cost Summary](#time-and-cost-summary)
  - [Matrice RASCI](#matrice-rasci)
  - [Regole operative del team](#regole-operative-del-team)
    - [Problem Solving](#problem-solving)
    - [Decision Making](#decision-making)
    - [Conflict Resolution](#conflict-resolution)
    - [Consensus Building](#consensus-building)
    - [Brainstorming](#brainstorming)
    - [Team Meetings](#team-meetings)
  - [Gestione dei cambiamenti di scope](#gestione-dei-cambiamenti-di-scope)
    - [Processo di gestione](#processo-di-gestione)
    - [Scope Change Request Form](#scope-change-request-form)
    - [Project Impact Statement](#project-impact-statement)
    - [Scope Bank](#scope-bank)
  - [Piano delle comunicazioni](#piano-delle-comunicazioni)
  - [Work Packages](#work-packages)
    - [Work Package: Progettazione struttura protocollo (1.2.2)](#work-package-progettazione-struttura-protocollo-122)
    - [Work Package: Implementazione parser protocollo (1.2.3)](#work-package-implementazione-parser-protocollo-123)
    - [Work Package: Implementazione visualizzazione dispositivi (1.4.2)](#work-package-implementazione-visualizzazione-dispositivi-142)
    - [Work Package: Collegamento frontend-backend (1.9.4)](#work-package-collegamento-frontend-backend-194)
    - [Work Package: Test di integrazione (1.10.1)](#work-package-test-di-integrazione-1101)
  - [Monitoring e Controlling](#monitoring-e-controlling)
    - [Tipi di report](#tipi-di-report)
    - [Earned Value Analysis](#earned-value-analysis)
    - [Scope Bank](#scope-bank-1)
    - [Issues Log](#issues-log)

# Documentazione di progetto

## Analisi dello stato

### AS IS

- Molteplici dispositivi IoT fabbricati con una propria applicazione che ne permette la gestione.
- Ogni applicativo ha una UI e una UX specializzata per quel singolo tipo di dispositivo.
- Per la stessa tipologia di dispositivo possono esistere più versioni dello stesso applicativo se necessario (per esempio una lampada senza colori e una lampada con i colori).
- Nessuna applicazione per gestire tutti i dispositivi insieme.
- La cooperazione/competizione tra i dispositivi è pressochè inesistente.
- Possibilità di avere molteplici dispositivi con diverse applicazioni diverse con però gli stessi passaggi ripetitivi.

### TO BE

- Singolo applicativo che coesiste con gli altri, ma che permette la gestione di tutti i dispositivi insieme.
- UI e UX dell'applicativo semplici ed intuitive, uguali per ogni dispositivo.
- Fornire la possibilità di gestire i dispositivi in modo cooperativo/competitivo attraverso script automatici.
- Tutti i passaggi ripetitivi presenti sotto un'unica applicazione, in modo da effettuarli una singola volta e non per ogni dispositivo.
- Gestione di utenti e dei loro permessi, in modo da raggruppare utenti (per esempio una famiglia) che usano gli stessi dispositivi.
- Possibilità di raggruppare vari dispositivi in gruppi logici.
- Protocollo per la registrazione di dispositivi eterogenei.

### NICE TO HAVE

- Notifiche quando un dispositivo va offline o online.
- Notifiche quando uno script da errore.
- Fornitura di un server online (cloud) come secondo entry point dell'applicativo, in modo da permettere l'utilizzo del suddetto anche da remoto.

## Condictions of Satisfaction (COS)

| Condizione                                 | Obiettivo                                                                                                                       |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| Protocollo univoco per tutti i dispositivi | Tutti i dispositivi devono poter essere registrati sull'applicativo, senza perdere le proprie funzionalità                      |
| Restare nel budget                         | €2 M                                                                                                                            |
| Feedback dagli utenti                      | Positivi o suggerimenti per nuove aggiunte                                                                                      |
| UX e UI                                    | Interfaccia grafica accessibile per chiunque, semplice ed intuitiva                                                             |
| Modularità                                 | Il sistema deve poter essere espandibile facilmente per possibili aggiunte di nuove funzionalità                                |
| Vecchi applicativi non scompaiono          | L'applicativo non deve essere un sostituto per i vecchi applicativi quanto più un supporto                                      |
| Alte performance                           | L'applicativo deve poter rispondere velocemente agli utenti, se installato sul dispositivo aziendale tempo di risposta < 100 ms |
| Comunicazione di guasti                    | Se si presenta un errore, non lo si deve mascherare ma si deve avvisare l'utente                                                |
| Aggiornamento applicativo autonomo         | L'applicativo deve poter essere aggiornato dall'utente senza un nuovo intervento dell'azienda                                   |
| Gestione dei permessi efficace             | Gli utenti devono essere soddisfatti della gestione dei permessi dell'applicativo                                               |

## Project Overview Statement (POS)

<table>
  <tbody>
    <tr>
      <th>Problema / Opportunità</th>
      <td> Molteplici applicativi diversi per la gestione di molteplici dispositivi diversi e completa assenza di cooperazione/competizione tra i vari dispositivi </td>
    </tr>
    <tr>
      <th>Goal</th>
      <td> Creare un applicativo che riesca a gestire l'insieme di dispositivi eterogenei in modo facile ed intuibile, portando anche cooperazione e/o competizione tra di loro </td>
    </tr>
    <tr>
      <th>Obbiettivi</th>
      <td> 
        <ul>
          <li> Creazione di un protocollo che permetta la descrizione formale di dispositivi IoT eterogenei. </li>
          <li> Implementazione di un linguaggio di scripting a blocchi per la programmazione di script che permettono la cooperazione e competizione dei dispositivi presenti nel sistema. </li>
          <li> Implementazione di un sistema software che permetta la gestione di molteplici dispositivi IoT eterogenei, degli utenti, dei loro permessi e degli script. </li>
          <li> Sviluppo di un'interfaccia utente semplice ed intuitiva, che sia simile in ogni pagina così che gli utenti possano imparare rapidamente ad usare l'applicativo. </li>
          <li> Fornire la possibilità di essere notificati di un dispositivo che va offline/online o quando uno script da errore. </li>
        </ul>
      </td>
    </tr>
    <tr>
      <th>Criteri di successo</th>
      <td> 
        <ul> 
          <li> Tutti i dispositivi aziendali devono poter essere utilizzati attraverso l'applicativo e senza perdita di funzionalità. </li> 
          <li> Gli utenti imparano ad utilizzare l'applicativo in circa 3/4 giorni, massimo 7. </li>
          <li> Almeno il 70% degli utenti che possiedono 4 o più dispositivi IoT utilizzano l'applicativo insieme ai vecchi applicativi. </li>
          <li> Soddisfazione pari o superiore all'80% nelle recensioni. </li>
          <li> Aumento del guadagno annuale di almeno 15% entro 2 anni dalla fine del progetto. </li>
        </ul>
      </td>
    </tr>
    <tr>
      <th>Assunzioni</th>
      <td>
        <ul>
          <li> Gli utenti admin del sistema sono mediamente esperti di tecnologia: sanno usare uno smartphone e navigare su internet. </li>
        </ul>
      </td>
    </tr>
    <tr>
      <th>Ostacoli</th>
      <td>
        <ul> 
          <li> Gli utenti potrebbero volere funzionalità avanzate o specifiche per certi dispositivi che vanno oltre lo scopo del progetto. </li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Analisi dei Rischi

#### Rischi tecnici

| ID   | Rischio                                              | Triangolo dello scope | Impatto | Probabilità | Mitigazione          |
| ---- | ---------------------------------------------------- | --------------------- | ------- | ----------- | -------------------- |
| #001 | Basse performance                                    | Qualità               | Alto    | Bassa       | Mitigare             |
| #002 | Tempo per creare il protocollo troppo lungo          | Tempo                 | Medio   | Media       | Piano di contingenza |
| #003 | Difficoltà nell'integrazione dei vari sottosistemi   | Scope                 | Alto    | Bassa       | Mitigare             |
| #004 | Difficoltà nel creare un linguaggio di script adatto | Scope                 | Alto    | Media       | Piano di contingenza |
| #005 | Gestione dei permessi utenti complessa               | Scope                 | Basso   | Bassa       | Accettare            |
| #006 | Uso di librerie su cui non si è formati              | Scope                 | Medio   | Bassa       | Mitigare             |
| #007 | UX e UI non efficaci                                 | Qualità               | Alto    | Media       | Piano di contingenza |
| #008 | Sistema non modulare                                 | Scope                 | Medio   | Alta        | Evitare              |

#### Rischi di gestione progetto

| ID   | Rischio                                    | Triangolo dello scope | Impatto | Probabilità | Mitigazione |
| ---- | ------------------------------------------ | --------------------- | ------- | ----------- | ----------- |
| #009 | Scarsa cura nell'allocazione delle risorse | Risorse               | Alto    | Media       | Evitare     |

#### Rischi di organizzazione

| ID   | Rischio                                                 | Triangolo dello scope | Impatto | Probabilità | Mitigazione |
| ---- | ------------------------------------------------------- | --------------------- | ------- | ----------- | ----------- |
| #010 | Non disponibilità di dispositivi da testare             | Risorse               | Alto    | Bassa       | Evitare     |
| #011 | Budget non sufficiente                                  | Costo                 | Alto    | Media       | Evitare     |
| #012 | Errata assegnazione delle priorità ai vari sottosistemi | Risorse               | Alto    | Media       | Evitare     |

#### Piani di contingenza

| ID Rischio | Piano di contingenza                                                                                                                                                                                   |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| #002       | Si può lavorare al protocollo mentre altri lavorano ad altre parti, perciò si può nel caso aumentare il tempo a disposizione per lavorare al protocollo finchè gli altri lavorano al resto del sistema |
| #004       | Si può discutere del linguaggio insieme ad altri sviluppatori o architetti per cercare di trovare una soluzione, ispirandosi anche ad altri linguaggi a blocchi conosciuti                             |
| #007       | Utilizzo di prototipi intermedi da far valutare agli utenti in modo da ricevere feedback e tornare sulla giusta strada                                                                                 |

## Requirements Breakdown Structure (RBS)

[Goal](#project-overview-statement-pos) -> **R1: Devices Protocol**
[Goal](#project-overview-statement-pos) -> **R2: Scripts management subsystem**
[Goal](#project-overview-statement-pos) -> **R3: Presentation subsystem**
[Goal](#project-overview-statement-pos) -> **R4: Devices management subsystem**
[Goal](#project-overview-statement-pos) -> **R5: Devices registration subsystem**
[Goal](#project-overview-statement-pos) -> **R6: Users management subsystem**
[Goal](#project-overview-statement-pos) -> **R7: Permissions management subsystem**
[Goal](#project-overview-statement-pos) -> **R8: Notifications management susbystem**

- **R1**
  - **R1.F1**: scelta linguaggio del protocollo
  - **R1.F2**: dichiarazione informazioni base sul dispositivo IoT
  - **R1.F3**: dichiarazione proprietà del dispositivo IoT
  - **R1.F4**: dichiarazione azioni del dispositivo IoT
  - **R1.F5**: dichiarazione eventi del dispositivo IoT
- **R2**
  - **R2.F1**: creazione script vuoto con nome
  - **R2.F2**: aggiunta istruzioni allo script
  - **R2.F3**: esecuzione script
    - **_SF1_**: avvio manuale della task
    - **_SF2_**: avvio automatico della automazione
  - **R2.F4**: visualizzazione script
  - **R2.F5**: modifica script già esistente
  - **R2.F6**: eliminazione script già esistente
  - **R2.F7**: visualizzazione di tutti gli script
- **R3**
  - **R3.F1**: scelta design system
  - **R3.F2**: creazione template per uniformare le pagine
  - **R3.F3**: creazione pagine per tutti gli utenti
    - **_SF1_**: pagina per la gestione dei dispositivi
    - **_SF2_**: pagina per la gestione delle task
    - **_SF3_**: pagina per la gestione delle automazioni
    - **_SF4_**: pagina per la gestione delle notifiche
  - **R3.F4**: creazione pagine per l'admin
    - **_SF1_**: pagina per la gestione degli utenti
    - **_SF2_**: pagina per la registrazione dei dispositivi
    - **_SF3_**: pagina per la gestione dei gruppi di dispositivi
    - **_SF4_**: pagina per la gestione dei permessi utente-dispositivo
    - **_SF5_**: pagina per la gestione dei permessi utente-script
  - **R3.F5**: collegamento frontend-backend
- **R4**
  - **R4.F1**: creazione gruppo di dispositivi
  - **R4.F2**: aggiunta dispositivo esistente ad un gruppo
  - **R4.F3**: visualizzazione dispositivi in un gruppo
  - **R4.F4**: rimozione dispositivo da un gruppo
  - **R4.F5**: cambio nome gruppo
  - **R4.F6**: eliminazione gruppo
  - **R4.F7**: visualizzazione gruppi
  - **R4.F8**: visualizzazione dispositivi
  - **R4.F9**: visualizzazione proprietà ed azioni del singolo dispositivo
  - **R4.F10**: eseguire azioni di un dispositivo
- **R5**
  - **R5.F1**: Individuazione dispositivi
  - **R5.F2**: Invio richiesta di registrazione ad un dispositivo
  - **R5.F3**: Ricezione della registrazione del dispositivo
    - **_SF1_**: Dispositivo accettato se conforme al protocollo
    - **_SF2_**: Dispositivo non accettato altrimenti
- **R6**
  - **R6.F1**: Registrazione utente
    - **_SF1_**: Automaticamente admin se è il primo utente
    - **_SF2_**: Invio richiesta registrazione all'admin altrimenti
  - **R6.F2**: Visualizzazione richieste di registrazione
  - **R6.F3**: Accettazione richiesta di registrazione
  - **R6.F4**: Rifiuto richiesta di registrazione
  - **R6.F5**: Eliminazione utente dal server
  - **R6.F6**: Login utente registrato nel server
- **R7**
  - **R7.F1**: Visualizzazione permessi utente-dispositivo
  - **R7.F2**: Modifica permessi utente-dispositivo
  - **R7.F3**: Visualizzazione permessi utente-scripts
  - **R7.F4**: Modifica permessi utente-scripts
- **R8**
  - **R8.F1**: Utente sceglie di ricevere notifiche sullo status offline/online di un certo dispositivo
  - **R8.F2**: Invio notifica ad un utente specifico

## User Stories

| Da     | Voglio poter                                                                                                                        | Così che                                                                                                                                   |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Utente | Creare una task con istruzioni di tutti i tipi anche se non ho i permessi su certi dispositivi                                      | Qualcuno diverso da me potrà eseguirla oppure darmi i permessi per farlo io stesso                                                         |
| Utente | Creare un'automazione senza le istruzioni che eseguono le azioni sui dispositivi su cui non ho i permessi                           | Non possa eseguire azioni sui dispositivi che l'admin non vuole farmi usare                                                                |
| Admin  | Gestire i permessi utente-dispositivo                                                                                               | Gli utenti possano eseguire azioni solamente sui dispositivi che voglio                                                                    |
| Admin  | Gestire una whitelist ed una blacklist per ogni task                                                                                | A prescindere dai permessi utente-dispositivo un utente possa eseguire o non eseguire la task                                              |
| Admin  | Gestire una editlist per una task o una automazione                                                                                 | Possa decidere quali utenti possono modificare tale task o automazione (per un'automazione controllo anche chi può attivarla/disattivarla) |
| Admin  | Eliminare un gruppo di dispositivi senza eliminare i dispositivi dal server                                                         | Possa continuare ad usarli ma senza quel gruppo specifico                                                                                  |
| Utente | Aggiungere un'istruzione ad uno script che invii una notifica con un messaggio personalizzato a qualcuno nello specifico            | Possa decidere a chi inviare un messaggio personalizzato in modo automatico                                                                |
| Utente | Aggiungere un'istruzione ad uno script che blocchi lo script per una quantità di tempo specificata                                  | Possa interrompere il flusso di controllo dello script per un tot di tempo                                                                 |
| Utente | Aggiungere un'istruzione ad uno script che faccia partire un'altra task                                                             | Il mio script attuale si fermi fino alla fine dell'esecuzione della task avviata                                                           |
| Utente | Aggiungere un'istruzione ad uno script che crea una costante tipizzata con un valore specifico                                      | Possa utilizzare tale valore in seguito dentro lo stesso script                                                                            |
| Utente | Aggiungere un'istruzione ad uno script che quando eseguito legga il valore di una proprietà specifica di un particolare dispositivo | Tale valore venga messo dentro una costante da utilizzare in seguito dentro lo stesso script                                               |
| Utente | Aggiungere un'istruzione ad uno script che esegue un'azione su un certo dispositivo                                                 | Possa eseguire azioni in modo pre-programmato e/o automatico                                                                               |
| Utente | Aggiungere un'istruzione di If che confronta due valori dello stesso tipo tra di loro                                               | Possa eseguire delle istruzioni solo nel caso in cui la condizione torni vero                                                              |
| Utente | Aggiungere un'istruzione di If-Else che confronta due valori dello stesso tipo tra di loro                                          | Possa eseguire certe istruzioni nel caso in cui la condizione sia vera e altre istruzioni altrimenti                                       |
| Utente | Decidere se un'automazione parte in base al ricevimento di un evento di un dispositivo o secondo un certo periodo di tempo          | Possa automatizzare l'esecuzione delle automazioni secondo i miei bisogni, possibilmente creando cooperazione tra i dispositivi            |
| Utente | Cambiare il mio username e la mia password                                                                                          | Possa tener aggiornati i miei dati                                                                                                         |

### Definition of Done

Sarà fondamentale seguire la metodologia del TDD (Test Driven Development) per lo sviluppo software dove possibile.
Questo permette di definire una user story così come una funzione/sottofunzione della RBS completata al 100% quando:

- Tutti gli unit test passano
- Il codice compila senza errori
- Il codice è stato revisionato da un altro sviluppatore e tutti i possibili problemi risolti
- Il nuovo codice non genera conflitti con quello vecchio
- La documentazione è stata aggiornata
- La funzionalità implementata è validata

Ovviamente il primo punto non può valere per il presentation subsystem in quanto non è possibile testare l'interfaccia grafica. In questo caso, il punto sarà scambiato con:

- L'interfaccia grafica è stata provata da persone che non ci hanno lavorato ed è stato approvato con successo

## Modello PMLC

### Users Management Subsystem

**Metodologia**: Lineare

**Motivazione**: Lo scope è ben definito e non cambierà, la soluzione è chiara ed è possibile usare una COTS per accelerare i lavori.

### Devices Management Subsystem

**Metodologia**: Incrementale

**Motivazione**: Non si è completamente sicuri di come visualizzare le proprietà ed eseguire le azioni di un dispositivo, per questo bisognerà procedere di volta in volta testando se le funzionalità sviluppate rispettano i requisiti che sono chiari e ben definiti.

### Devices Protocol

**Metodologia**: Adattivo

**Motivazione**: Il protocollo comune tra i dispositivi dovrà essere creato durante il progetto ed essendo qualcosa di completamente nuovo per l'azienda potrebbe richiedere vari cambi di requisiti e di idee per la soluzione finale.

### Devices Registration Subsystem

**Metodologia**: Incrementale

**Motivazione**: I requisiti sono chiari e ben definiti, ma ci sono tante soluzioni possibili e bisogna sceglierne una che potrebbe cambiare per vari motivi, come performance o semplicità di utilizzo/messa in pratica.

### Scripts Management Subsystem

**Metodologia**: Adattivo

**Motivazione**: La gestione degli script è complicata ed è previsto che ci saranno molti cambiamenti anche dei requisiti nel corso del progetto.

### Permissions Management Subsystem

**Metodologia**: Iterativo

**Motivazione**: La gestione dei permessi è qualcosa di complesso e si ha bisogno del feedback di utenti per poter capire se i requisiti sono corretti e completi.

### Notifications Management Subsystem

**Metodologia**: Lineare

**Motivazione**: Requisiti ben definiti e soluzione già ben utilizzata in più progetti, non sarà necessario modificare questo sottosistema una volta progettato.

### Presentation Subsystem

**Metodologia**: Incrementale

**Motivazione**: I requisiti sono piuttosto stabili e ben definiti, ma la soluzione è da perfezionare attraverso dei prototipi intermedi da far provare ad altri sviluppatori ed esperti del settore. Arrivati ad un certo punto di completezza del prototipo possono essere rilasciate versioni beta da far provare direttamente agli utenti e perfezionare l'applicativo attraverso il feedback ricevuto.

## Project Definition Statement (PDS)

<table>
  <tbody>
    <tr>
      <th>Problema / Opportunità</th>
      <td> Gli utenti con molti dispositivi IoT devono gestire ciascuno tramite la propria applicazione dedicata, con passaggi ripetitivi e senza la possibilità di creare cooperazione e/o competizione tra di essi. </td>
    </tr>
    <tr>
      <th>Goal</th>
      <td> Creare un applicativo che riesca a gestire l'insieme di dispositivi eterogenei in modo facile ed intuibile, portando anche cooperazione e/o competizione tra di loro, senza sostituire le applicazioni esistenti ma affiancandole come strumento di gestione unificata. </td>
    </tr>
    <tr>
      <th>Obbiettivi</th>
      <td> 
        <ul>
          <li> <b>O1</b>: Creazione di un protocollo formale (Devices Protocol) che permetta la descrizione di dispositivi IoT eterogenei attraverso proprietà, azioni ed eventi, mantenendo tutte le funzionalità originali. Sottosistemi coinvolti: R1 (Devices Protocol), R5 (Devices Registration). </li>
          <li> <b>O2</b>: Implementazione di un linguaggio di scripting a blocchi per la programmazione di task ed automazioni che permettano la cooperazione e competizione dei dispositivi presenti nel sistema. Sottosistemi coinvolti: R2 (Scripts Management). Dipende da: O1. </li>
          <li> <b>O3</b>: Implementazione del sistema software di gestione dei dispositivi, comprensivo di gruppi logici e comunicazione con i dispositivi. Sottosistemi coinvolti: R4 (Devices Management), R5 (Devices Registration). Dipende da: O1. </li>
          <li> <b>O4</b>: Implementazione del sistema di gestione utenti con ruoli (user/admin) e del sistema di gestione dei permessi sugli utenti. Sottosistemi coinvolti: R6 (Users Management), R7 (Permissions Management). </li>
          <li> <b>O5</b>: Sviluppo di un'interfaccia utente semplice ed intuitiva, uniforme in ogni pagina, permettendo agli utenti di imparare rapidamente. Sottosistemi coinvolti: R3 (Presentation). Dipende da: O1, O2, O3, O4. </li>
          <li> <b>O6</b>: Fornire la possibilità di essere notificati dello stato online/offline dei dispositivi e degli errori negli script. Sottosistemi coinvolti: R8 (Notifications Management). Dipende da: O2, O3, O4. </li>
        </ul>
      </td>
    </tr>
    <tr>
      <th>Criteri di successo</th>
      <td> 
        <ul> 
          <li> Tutti i dispositivi aziendali attualmente in produzione devono poter essere utilizzati attraverso l'applicativo e senza perdita di funzionalità. Verificabile al completamento dell'obiettivo O1. </li> 
          <li> Gli utenti imparano ad utilizzare l'applicativo in circa 3/4 giorni, massimo 7. Verificabile tramite test di usabilità durante la fase di beta testing. </li>
          <li> Almeno il 70% degli utenti che possiedono 4 o più dispositivi IoT utilizzano l'applicativo insieme ai vecchi applicativi. Verificabile entro 6 mesi dal rilascio. </li>
          <li> Soddisfazione pari o superiore all'80% nelle recensioni. Verificabile entro 6 mesi dal rilascio. </li>
          <li> Aumento del guadagno annuale di almeno 15% entro 2 anni dalla fine del progetto. </li>
          <li> Costo totale del progetto inferiore a €2M (vincolo COS). </li>
          <li> Durata totale del progetto non superiore a 15 mesi. </li>
        </ul>
      </td>
    </tr>
    <tr>
      <th>Assunzioni</th>
      <td>
        <ul>
          <li> Gli utenti admin del sistema sono mediamente esperti di tecnologia: sanno usare uno smartphone e navigare su internet. </li>
          <li> I dispositivi IoT aziendali attualmente in produzione sono disponibili per il testing durante l'intero progetto. </li>
          <li> Le competenze necessarie per lo sviluppo del protocollo e del linguaggio a blocchi sono presenti nel team o acquisibili tramite formazione. </li>
          <li> L'infrastruttura tecnologica aziendale (server di sviluppo, ambienti di test) è disponibile e adeguata. </li>
          <li> Gli utenti finali sono disponibili per sessioni di feedback durante la fase di beta testing. </li>
        </ul>
      </td>
    </tr>
    <tr>
      <th>Rischi e Ostacoli</th>
      <td>
        <ul> 
          <li> Gli utenti potrebbero volere funzionalità avanzate o specifiche per certi dispositivi che vanno oltre lo scopo del progetto. Piano: comunicazione chiara dello scope tramite le COS. </li>
          <li> Il protocollo potrebbe non riuscire a coprire tutti i dispositivi esistenti senza perdita di funzionalità (Rischio #002). Piano di contingenza: aumento del tempo a disposizione o rilascio iniziale privo di tali funzionalità, da aggiungere in una nuova versione del software. </li>
          <li> Il linguaggio a blocchi potrebbe risultare troppo complesso o limitato per gli utenti (Rischio #004). Piano di contingenza: ispirazione a linguaggi a blocchi esistenti e sessioni di confronto. </li>
          <li> La UX/UI potrebbe non soddisfare gli utenti (Rischio #007). Piano di contingenza: prototipi intermedi con feedback utenti. </li>
          <li> Il sistema potrebbe non essere sufficientemente modulare per futuri ampliamenti (Rischio #008). Piano: architettura a microservizi/moduli fin dalla progettazione. </li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

## Work Breakdown Structure (WBS)

**1. DomoticApp**

- **1.1 Project Management**
  - 1.1.1 Pianificazione del progetto
  - 1.1.2 Monitoraggio e controllo (attività continuativa)
  - 1.1.3 Chiusura del progetto
- **1.2 Devices Protocol** *(PMLC: Adattivo)*
  - 1.2.1 Analisi dei dispositivi IoT esistenti
  - 1.2.2 Progettazione della struttura del protocollo
  - 1.2.3 Implementazione del parser del protocollo
  - 1.2.4 Test del protocollo sui dispositivi
  - 1.2.5 Revisione e raffinamento del protocollo
- **1.3 Users Management Subsystem** *(PMLC: Lineare)*
  - 1.3.1 Selezione e configurazione COTS per autenticazione
  - 1.3.2 Implementazione registrazione e login
  - 1.3.3 Implementazione gestione ruoli (user/admin)
  - 1.3.4 Test del sottosistema utenti
- **1.4 Devices Management Subsystem** *(PMLC: Incrementale)*
  - 1.4.1 Implementazione CRUD gruppi di dispositivi
  - 1.4.2 Implementazione visualizzazione dispositivi e proprietà
  - 1.4.3 Implementazione esecuzione azioni su dispositivi
  - 1.4.4 Test del sottosistema dispositivi
- **1.5 Devices Registration Subsystem** *(PMLC: Incrementale)*
  - 1.5.1 Implementazione individuazione dispositivi nella rete
  - 1.5.2 Implementazione flusso di registrazione del dispositivo
  - 1.5.3 Implementazione validazione conformità al protocollo
  - 1.5.4 Test del sottosistema registrazione
- **1.6 Scripts Management Subsystem** *(PMLC: Adattivo)*
  - 1.6.1 Progettazione del linguaggio a blocchi
  - 1.6.2 Implementazione editor visuale per script
  - 1.6.3 Implementazione motore di esecuzione script
  - 1.6.4 Implementazione gestione task e automazioni
  - 1.6.5 Test del sottosistema script
- **1.7 Permissions Management Subsystem** *(PMLC: Iterativo)*
  - 1.7.1 Progettazione del modello dei permessi
  - 1.7.2 Implementazione permessi utente-dispositivo
  - 1.7.3 Implementazione permessi utente-script (whitelist/blacklist/editlist)
  - 1.7.4 Validazione dei permessi con utenti e raffinamento
- **1.8 Notifications Management Subsystem** *(PMLC: Lineare)*
  - 1.8.1 Implementazione sistema di notifiche base
  - 1.8.2 Implementazione notifiche stato dispositivo (online/offline)
  - 1.8.3 Implementazione notifiche errori script
  - 1.8.4 Test del sottosistema notifiche
- **1.9 Presentation Subsystem** *(PMLC: Incrementale)*
  - 1.9.1 Selezione design system e creazione template base
  - 1.9.2 Implementazione pagine utente
  - 1.9.3 Implementazione pagine admin
  - 1.9.4 Collegamento frontend-backend
  - 1.9.5 Test UX e prototipi intermedi
- **1.10 Testing e Integrazione**
  - 1.10.1 Test di integrazione dei sottosistemi
  - 1.10.2 Test end-to-end
  - 1.10.3 Beta testing con utenti
  - 1.10.4 Correzione bug e ottimizzazione

**Mapping WBS → RBS:**

| WBS | RBS | Copertura                                                                                           |
| --- | --- | --------------------------------------------------------------------------------------------------- |
| 1.2 | R1  | R1.F1-R1.F5 (scelta linguaggio, dichiarazione info base, proprietà, azioni, eventi)                 |
| 1.3 | R6  | R6.F1-R6.F6 (registrazione, visualizzazione richieste, accettazione/rifiuto, eliminazione, login)   |
| 1.4 | R4  | R4.F1-R4.F10 (CRUD gruppi, visualizzazione dispositivi/gruppi/proprietà, esecuzione azioni)         |
| 1.5 | R5  | R5.F1-R5.F3 (individuazione, invio richiesta, ricezione registrazione)                              |
| 1.6 | R2  | R2.F1-R2.F7 (creazione/aggiunta istruzioni/esecuzione/visualizzazione/modifica/eliminazione script) |
| 1.7 | R7  | R7.F1-R7.F4 (visualizzazione/modifica permessi utente-dispositivo e utente-script)                  |
| 1.8 | R8  | R8.F1-R8.F2 (scelta notifiche, invio notifiche)                                                     |
| 1.9 | R3  | R3.F1-R3.F5 (design system, template, pagine utente, pagine admin, collegamento FE-BE)              |

## Stime di Effort e Durata

Le stime sono espresse in settimane. La tecnica di stima utilizzata è indicata per ogni task.

| ID     | Task                                        | Durata (settimane) | Tecnica di stima    |
| ------ | ------------------------------------------- | ------------------ | ------------------- |
| 1.1.1  | Pianificazione del progetto                 | 3                  | Giudizio di esperti |
| 1.2.1  | Analisi dei dispositivi IoT esistenti       | 3                  | Giudizio di esperti |
| 1.2.2  | Progettazione struttura protocollo          | 3                  | Three-Point         |
| 1.2.3  | Implementazione parser protocollo           | 4                  | Three-Point         |
| 1.2.4  | Test protocollo sui dispositivi             | 3                  | Three-Point         |
| 1.2.5  | Revisione e raffinamento protocollo         | 2                  | Three-Point         |
| 1.3.1  | Selezione e configurazione COTS             | 2                  | Dati storici        |
| 1.3.2  | Implementazione registrazione e login       | 3                  | Dati storici        |
| 1.3.3  | Implementazione gestione ruoli              | 2                  | Giudizio di esperti |
| 1.3.4  | Test sottosistema utenti                    | 2                  | Giudizio di esperti |
| 1.4.1  | Implementazione CRUD gruppi                 | 3                  | Giudizio di esperti |
| 1.4.2  | Implementazione visualizzazione dispositivi | 3                  | Three-Point         |
| 1.4.3  | Implementazione azioni su dispositivi       | 3                  | Three-Point         |
| 1.4.4  | Test sottosistema dispositivi               | 2                  | Giudizio di esperti |
| 1.5.1  | Implementazione individuazione dispositivi  | 3                  | Three-Point         |
| 1.5.2  | Implementazione flusso di registrazione     | 3                  | Three-Point         |
| 1.5.3  | Implementazione validazione protocollo      | 2                  | Giudizio di esperti |
| 1.5.4  | Test sottosistema registrazione             | 2                  | Giudizio di esperti |
| 1.6.1  | Progettazione linguaggio a blocchi          | 4                  | Three-Point         |
| 1.6.2  | Implementazione editor visuale              | 4                  | Three-Point         |
| 1.6.3  | Implementazione motore di esecuzione        | 4                  | Three-Point         |
| 1.6.4  | Implementazione gestione task e automazioni | 3                  | Three-Point         |
| 1.6.5  | Test sottosistema script                    | 3                  | Giudizio di esperti |
| 1.7.1  | Progettazione modello permessi              | 3                  | Three-Point         |
| 1.7.2  | Implementazione permessi utente-dispositivo | 3                  | Three-Point         |
| 1.7.3  | Implementazione permessi utente-script      | 3                  | Three-Point         |
| 1.7.4  | Validazione permessi con utenti             | 3                  | Giudizio di esperti |
| 1.8.1  | Implementazione sistema notifiche base      | 2                  | Dati storici        |
| 1.8.2  | Implementazione notifiche stato dispositivo | 2                  | Giudizio di esperti |
| 1.8.3  | Implementazione notifiche errori script     | 2                  | Giudizio di esperti |
| 1.8.4  | Test sottosistema notifiche                 | 2                  | Giudizio di esperti |
| 1.9.1  | Selezione design system e template          | 2                  | Dati storici        |
| 1.9.2  | Implementazione pagine utente               | 4                  | Three-Point         |
| 1.9.3  | Implementazione pagine admin                | 3                  | Three-Point         |
| 1.9.4  | Collegamento frontend-backend               | 4                  | Three-Point         |
| 1.9.5  | Test UX e prototipi intermedi               | 3                  | Giudizio di esperti |
| 1.10.1 | Test di integrazione dei sottosistemi       | 3                  | Giudizio di esperti |
| 1.10.2 | Test end-to-end                             | 3                  | Giudizio di esperti |
| 1.10.3 | Beta testing con utenti                     | 3                  | Giudizio di esperti |
| 1.10.4 | Correzione bug e ottimizzazione             | 3                  | Three-Point         |
| 1.1.3  | Chiusura del progetto                       | 2                  | Giudizio di esperti |

**Nota**: il task 1.1.2 (Monitoraggio e controllo) è un'attività continuativa del Project Manager per tutta la durata del progetto (~30% del suo tempo) e non è incluso come task discreto nel network diagram.

## Assegnamento delle Risorse

**Composizione del team di progetto:**

| ID  | Ruolo              | Competenze principali                             | Costo settimanale (lordo) |
| --- | ------------------ | ------------------------------------------------- | ------------------------- |
| PM  | Project Manager    | Gestione progetto, comunicazione, dominio IoT     | €1.600                    |
| SD1 | Senior Developer 1 | Backend, IoT, protocolli di comunicazione         | €1.400                    |
| SD2 | Senior Developer 2 | Backend, architettura software, linguaggi formali | €1.400                    |
| D1  | Developer 1        | Backend, database, API REST                       | €1.100                    |
| D2  | Developer 2        | Backend, sicurezza, autenticazione                | €1.100                    |
| D3  | Developer 3        | Frontend, linguaggi visuali, UX                   | €1.100                    |
| D4  | Developer 4        | Full-stack, testing, automazione                  | €1.100                    |
| UX  | UX/UI Designer     | Design system, prototipazione, accessibilità      | €1.100                    |
| QA  | QA Tester          | Testing, quality assurance, automazione test      | €1.000                    |
| IoT | IoT Specialist     | Dispositivi IoT, elettronica, protocolli hardware | €1.200 (part-time)        |

**Assegnamento risorse per task:**

| ID     | Task                                        | Risorse assegnate    | Costo task   |
| ------ | ------------------------------------------- | -------------------- | ------------ |
| 1.1.1  | Pianificazione del progetto                 | PM, SD1, SD2         | €13.200      |
| 1.2.1  | Analisi dispositivi IoT esistenti           | SD1, IoT             | €7.800       |
| 1.2.2  | Progettazione struttura protocollo          | SD1, IoT             | €7.800       |
| 1.2.3  | Implementazione parser protocollo           | SD1, D1              | €10.000      |
| 1.2.4  | Test protocollo sui dispositivi             | QA, IoT              | €6.600       |
| 1.2.5  | Revisione e raffinamento protocollo         | SD1, IoT             | €5.200       |
| 1.3.1  | Selezione e configurazione COTS             | D2                   | €2.200       |
| 1.3.2  | Implementazione registrazione e login       | SD2, D2              | €7.500       |
| 1.3.3  | Implementazione gestione ruoli              | D2                   | €2.200       |
| 1.3.4  | Test sottosistema utenti                    | QA                   | €2.000       |
| 1.4.1  | Implementazione CRUD gruppi                 | D1, D2               | €6.600       |
| 1.4.2  | Implementazione visualizzazione dispositivi | D1                   | €3.300       |
| 1.4.3  | Implementazione azioni su dispositivi       | D1, D2               | €6.600       |
| 1.4.4  | Test sottosistema dispositivi               | QA                   | €2.000       |
| 1.5.1  | Implementazione individuazione dispositivi  | SD1, IoT             | €7.800       |
| 1.5.2  | Implementazione flusso di registrazione     | SD1                  | €4.200       |
| 1.5.3  | Implementazione validazione protocollo      | SD1, D1              | €5.000       |
| 1.5.4  | Test sottosistema registrazione             | QA                   | €2.000       |
| 1.6.1  | Progettazione linguaggio a blocchi          | SD2, D3              | €10.000      |
| 1.6.2  | Implementazione editor visuale              | D3, UX               | €8.800       |
| 1.6.3  | Implementazione motore di esecuzione        | SD2, D4              | €10.000      |
| 1.6.4  | Implementazione gestione task e automazioni | SD2, D3, D4          | €10.800      |
| 1.6.5  | Test sottosistema script                    | QA, D4               | €6.300       |
| 1.7.1  | Progettazione modello permessi              | PM                   | €4.800       |
| 1.7.2  | Implementazione permessi utente-dispositivo | D2                   | €3.300       |
| 1.7.3  | Implementazione permessi utente-script      | D2, D4               | €6.600       |
| 1.7.4  | Validazione permessi con utenti             | QA, PM               | €7.800       |
| 1.8.1  | Implementazione sistema notifiche base      | D4                   | €2.200       |
| 1.8.2  | Implementazione notifiche stato dispositivo | D4                   | €2.200       |
| 1.8.3  | Implementazione notifiche errori script     | D4                   | €2.200       |
| 1.8.4  | Test sottosistema notifiche                 | QA                   | €2.000       |
| 1.9.1  | Selezione design system e template          | UX                   | €2.200       |
| 1.9.2  | Implementazione pagine utente               | UX, D3               | €8.800       |
| 1.9.3  | Implementazione pagine admin                | UX, D3               | €6.600       |
| 1.9.4  | Collegamento frontend-backend               | D1, D2               | €8.800       |
| 1.9.5  | Test UX e prototipi intermedi               | UX, QA               | €6.300       |
| 1.10.1 | Test di integrazione                        | QA, SD1, SD2         | €11.400      |
| 1.10.2 | Test end-to-end                             | QA, D1               | €6.300       |
| 1.10.3 | Beta testing con utenti                     | QA, PM, UX           | €11.100      |
| 1.10.4 | Correzione bug e ottimizzazione             | SD1, SD2, D1, D2     | €15.000      |
| 1.1.2  | Monitoraggio e controllo (continuativo)     | PM (~30%)            | €25.920      |
| 1.1.3  | Chiusura del progetto                       | PM                   | €3.200       |
|        |                                             | **Totale personale** | **€284.620** |

## Project Network Diagram

**Tabella delle dipendenze** (tutte le dipendenze sono di tipo Finish-to-Start):

| ID     | Task                                        | Predecessori        | Durata |
| ------ | ------------------------------------------- | ------------------- | ------ |
| 1.1.1  | Pianificazione del progetto                 | -                   | 3      |
| 1.2.1  | Analisi dispositivi IoT esistenti           | 1.1.1               | 3      |
| 1.2.2  | Progettazione struttura protocollo          | 1.2.1               | 3      |
| 1.2.3  | Implementazione parser protocollo           | 1.2.2               | 4      |
| 1.2.4  | Test protocollo sui dispositivi             | 1.2.3               | 3      |
| 1.2.5  | Revisione e raffinamento protocollo         | 1.2.4               | 2      |
| 1.3.1  | Selezione e configurazione COTS             | 1.1.1               | 2      |
| 1.3.2  | Implementazione registrazione e login       | 1.3.1               | 3      |
| 1.3.3  | Implementazione gestione ruoli              | 1.3.2               | 2      |
| 1.3.4  | Test sottosistema utenti                    | 1.3.3               | 2      |
| 1.4.1  | Implementazione CRUD gruppi                 | 1.2.5, 1.3.4        | 3      |
| 1.4.2  | Implementazione visualizzazione dispositivi | 1.4.1               | 3      |
| 1.4.3  | Implementazione azioni su dispositivi       | 1.4.2               | 3      |
| 1.4.4  | Test sottosistema dispositivi               | 1.4.3               | 2      |
| 1.5.1  | Implementazione individuazione dispositivi  | 1.2.5               | 3      |
| 1.5.2  | Implementazione flusso di registrazione     | 1.5.1               | 3      |
| 1.5.3  | Implementazione validazione protocollo      | 1.5.2               | 2      |
| 1.5.4  | Test sottosistema registrazione             | 1.5.3               | 2      |
| 1.6.1  | Progettazione linguaggio a blocchi          | 1.1.1               | 4      |
| 1.6.2  | Implementazione editor visuale              | 1.6.1               | 4      |
| 1.6.3  | Implementazione motore di esecuzione        | 1.6.1               | 4      |
| 1.6.4  | Implementazione gestione task e automazioni | 1.6.2, 1.6.3, 1.2.5 | 3      |
| 1.6.5  | Test sottosistema script                    | 1.6.4               | 3      |
| 1.7.1  | Progettazione modello permessi              | 1.1.1               | 3      |
| 1.7.2  | Implementazione permessi utente-dispositivo | 1.7.1, 1.3.4        | 3      |
| 1.7.3  | Implementazione permessi utente-script      | 1.7.2, 1.6.5        | 3      |
| 1.7.4  | Validazione permessi con utenti             | 1.7.3               | 3      |
| 1.8.1  | Implementazione sistema notifiche base      | 1.3.4               | 2      |
| 1.8.2  | Implementazione notifiche stato dispositivo | 1.8.1, 1.4.4        | 2      |
| 1.8.3  | Implementazione notifiche errori script     | 1.8.2, 1.6.5        | 2      |
| 1.8.4  | Test sottosistema notifiche                 | 1.8.3               | 2      |
| 1.9.1  | Selezione design system e template          | 1.1.1               | 2      |
| 1.9.2  | Implementazione pagine utente               | 1.9.1, 1.4.4        | 4      |
| 1.9.3  | Implementazione pagine admin                | 1.9.2               | 3      |
| 1.9.4  | Collegamento frontend-backend               | 1.9.3, 1.7.4, 1.8.4 | 4      |
| 1.9.5  | Test UX e prototipi intermedi               | 1.9.4               | 3      |
| 1.10.1 | Test di integrazione                        | 1.9.4, 1.5.4        | 3      |
| 1.10.2 | Test end-to-end                             | 1.10.1              | 3      |
| 1.10.3 | Beta testing con utenti                     | 1.10.2, 1.9.5       | 3      |
| 1.10.4 | Correzione bug e ottimizzazione             | 1.10.3              | 3      |
| 1.1.3  | Chiusura del progetto                       | 1.10.4              | 2      |

## Critical Path e Schedule

**Forward Pass e Backward Pass:**

La seguente tabella riporta i risultati del forward pass (ES, EF) e del backward pass (LS, LF) per ogni task, con il calcolo della slack time. I task con slack = 0 fanno parte del **critical path** (contrassegnati con \*).

| ID     | ES  | EF  | LS  | LF  | Slack   |
| ------ | --- | --- | --- | --- | ------- |
| 1.1.1  | 1   | 3   | 1   | 3   | **0\*** |
| 1.2.1  | 4   | 6   | 4   | 6   | **0\*** |
| 1.2.2  | 7   | 9   | 7   | 9   | **0\*** |
| 1.2.3  | 10  | 13  | 10  | 13  | **0\*** |
| 1.2.4  | 14  | 16  | 14  | 16  | **0\*** |
| 1.2.5  | 17  | 18  | 17  | 18  | **0\*** |
| 1.3.1  | 4   | 5   | 10  | 11  | 6       |
| 1.3.2  | 6   | 8   | 12  | 14  | 6       |
| 1.3.3  | 9   | 10  | 15  | 16  | 6       |
| 1.3.4  | 11  | 12  | 17  | 18  | 6       |
| 1.4.1  | 19  | 21  | 19  | 21  | **0\*** |
| 1.4.2  | 22  | 24  | 22  | 24  | **0\*** |
| 1.4.3  | 25  | 27  | 25  | 27  | **0\*** |
| 1.4.4  | 28  | 29  | 28  | 29  | **0\*** |
| 1.5.1  | 19  | 21  | 31  | 33  | 12      |
| 1.5.2  | 22  | 24  | 34  | 36  | 12      |
| 1.5.3  | 25  | 26  | 37  | 38  | 12      |
| 1.5.4  | 27  | 28  | 39  | 40  | 12      |
| 1.6.1  | 4   | 7   | 17  | 20  | 13      |
| 1.6.2  | 8   | 11  | 21  | 24  | 13      |
| 1.6.3  | 8   | 11  | 21  | 24  | 13      |
| 1.6.4  | 19  | 21  | 25  | 27  | 6       |
| 1.6.5  | 22  | 24  | 28  | 30  | 6       |
| 1.7.1  | 4   | 6   | 25  | 27  | 21      |
| 1.7.2  | 13  | 15  | 28  | 30  | 15      |
| 1.7.3  | 25  | 27  | 31  | 33  | 6       |
| 1.7.4  | 28  | 30  | 34  | 36  | 6       |
| 1.8.1  | 13  | 14  | 29  | 30  | 16      |
| 1.8.2  | 30  | 31  | 31  | 32  | 1       |
| 1.8.3  | 32  | 33  | 33  | 34  | 1       |
| 1.8.4  | 34  | 35  | 35  | 36  | 1       |
| 1.9.1  | 4   | 5   | 28  | 29  | 24      |
| 1.9.2  | 30  | 33  | 30  | 33  | **0\*** |
| 1.9.3  | 34  | 36  | 34  | 36  | **0\*** |
| 1.9.4  | 37  | 40  | 37  | 40  | **0\*** |
| 1.9.5  | 41  | 43  | 44  | 46  | 3       |
| 1.10.1 | 41  | 43  | 41  | 43  | **0\*** |
| 1.10.2 | 44  | 46  | 44  | 46  | **0\*** |
| 1.10.3 | 47  | 49  | 47  | 49  | **0\*** |
| 1.10.4 | 50  | 52  | 50  | 52  | **0\*** |
| 1.1.3  | 53  | 54  | 53  | 54  | **0\*** |

**Critical Path:**

> 1.1.1 → 1.2.1 → 1.2.2 → 1.2.3 → 1.2.4 → 1.2.5 → 1.4.1 → 1.4.2 → 1.4.3 → 1.4.4 → 1.9.2 → 1.9.3 → 1.9.4 → 1.10.1 → 1.10.2 → 1.10.3 → 1.10.4 → 1.1.3

*Pianificazione → Devices Protocol → Devices Management → Presentation → Testing e Integrazione → Chiusura*

**Durata del critical path**: 54 settimane

**Durata totale con management reserve** (3 settimane, ~5,5%): **57 settimane** (~13 mesi)

**Schedule (Gantt sintetico):**

| Fase                     | Settimane                        | Periodo indicativo |
| ------------------------ | -------------------------------- | ------------------ |
| Pianificazione           | 1-3                              | Mese 1             |
| Devices Protocol         | 4-18                             | Mesi 1-4           |
| Users Management         | 4-12                             | Mesi 1-3           |
| Scripts Management       | 4-24                             | Mesi 1-6           |
| Permissions Management   | 4-30                             | Mesi 1-7           |
| Devices Management       | 19-29                            | Mesi 5-7           |
| Devices Registration     | 19-28                            | Mesi 5-7           |
| Notifications Management | 13-35                            | Mesi 3-8           |
| Presentation             | 4-43                             | Mesi 1-10          |
| Testing e Integrazione   | 41-52                            | Mesi 10-12         |
| Management Reserve       | 53-55                            | Mese 13            |
| Chiusura                 | 53-54 (o 56-57 se usata reserve) | Mese 13            |

## Stime dei Costi

**Riepilogo costi per sottosistema:**

| Sottosistema                                                    | Costo personale |
| --------------------------------------------------------------- | --------------- |
| 1.1 Project Management (pianificazione + monitoring + chiusura) | €42.320         |
| 1.2 Devices Protocol                                            | €37.400         |
| 1.3 Users Management                                            | €13.900         |
| 1.4 Devices Management                                          | €18.500         |
| 1.5 Devices Registration                                        | €19.000         |
| 1.6 Scripts Management                                          | €45.900         |
| 1.7 Permissions Management                                      | €22.500         |
| 1.8 Notifications Management                                    | €8.600          |
| 1.9 Presentation                                                | €32.700         |
| 1.10 Testing e Integrazione                                     | €43.800         |
| **Totale costi di personale**                                   | **€284.620**    |

**Costi aggiuntivi:**

| Voce                                                            | Costo        |
| --------------------------------------------------------------- | ------------ |
| Infrastruttura (server di sviluppo, ambienti di test, cloud)    | €15.000      |
| Licenze software (MS Project, IDE, strumenti di testing)        | €10.000      |
| Dispositivi IoT per testing (campioni da reparto elettronica)   | €20.000      |
| Formazione specifica (protocolli IoT, linguaggi a blocchi)      | €5.000       |
| Overhead aziendale (pro-rata: ufficio, utenze, amministrazione) | €80.000      |
| **Totale costi aggiuntivi**                                     | **€130.000** |

**Management reserve** (~10% del totale): **€41.500**

|                                         |                |
| --------------------------------------- | -------------- |
| **Costo totale stimato del progetto**   | **€456.120**   |
| **Costo totale con management reserve** | **~€460.000**  |
| **Budget disponibile (vincolo COS)**    | **€2.000.000** |

## Cash Flow

**Piano di incasso (inflow):**

Si è previsto un piano di incasso misto con anticipo, pagamenti a milestone e saldo:

| Evento                                                     | Periodo       | Importo      | % del totale |
| ---------------------------------------------------------- | ------------- | ------------ | ------------ |
| Anticipo alla firma del contratto                          | Settimana 1   | €69.000      | 15%          |
| Milestone 1: Protocol + Users Management completati        | ~Settimana 18 | €100.000     | 21,7%        |
| Milestone 2: Primo prototipo funzionante (FE-BE collegato) | ~Settimana 40 | €120.000     | 26,1%        |
| Milestone 3: Beta release                                  | ~Settimana 49 | €100.000     | 21,7%        |
| Saldo: accettazione finale                                 | ~Settimana 57 | €71.000      | 15,5%        |
| **Totale**                                                 |               | **€460.000** | **100%**     |

**Piano di spesa (outflow) e cash flow netto su base trimestrale:**

| Trimestre  | Settimane | Outflow (uscite) | Inflow (entrate) | Cash Flow netto | Cash Flow cumulato |
| ---------- | --------- | ---------------- | ---------------- | --------------- | ------------------ |
| Q1         | 1-13      | €120.000         | €69.000          | -€51.000        | -€51.000           |
| Q2         | 14-26     | €105.000         | €100.000         | -€5.000         | -€56.000           |
| Q3         | 27-39     | €92.000          | €0               | -€92.000        | -€148.000          |
| Q4         | 40-52     | €100.000         | €220.000         | +€120.000       | -€28.000           |
| Q5         | 53-57     | €43.000          | €71.000          | +€28.000        | €0                 |
| **Totale** |           | **€460.000**     | **€460.000**     | **€0**          |                    |

**Nota**: il cash flow cumulato negativo raggiunge il picco nel Q3 (-€148.000). Questa è la massima esposizione finanziaria del progetto, che l'azienda deve essere in grado di coprire con la propria liquidità.

## Project Proposal

### Executive Summary

La SDA Corporation propone lo sviluppo di **DomoticApp**, una web application per la gestione unificata di dispositivi IoT eterogenei. Il progetto ha una durata stimata di 57 settimane (inclusa management reserve) e un costo stimato di €460.000, ben al di sotto del vincolo di budget di €2M.

### Background

L'azienda produce dispositivi IoT, ciascuno con la propria applicazione dedicata. Gli utenti con molti dispositivi devono utilizzare applicazioni diverse per ciascuno, senza possibilità di automazione o cooperazione tra dispositivi. L'analisi delle recensioni degli utenti ha evidenziato questa problematica come fonte di insoddisfazione.

### Objective

Realizzare un applicativo che permetta la gestione di tutti i dispositivi aziendali da un'unica interfaccia, inclusa la possibilità di creare automazioni trasversali tramite un linguaggio di scripting a blocchi. Il tutto basato su un protocollo comune che renda il sistema espandibile a qualsiasi futuro dispositivo.

### Overview of Approach

Il progetto è suddiviso in 8 sottosistemi, ciascuno gestito con il PMLC model più adatto:

| Sottosistema             | PMLC Model   | Motivazione sintetica                                    |
| ------------------------ | ------------ | -------------------------------------------------------- |
| Devices Protocol         | Adattivo     | Requisiti incerti, soluzione completamente nuova         |
| Scripts Management       | Adattivo     | Alta complessità e requisiti soggetti a cambiamenti      |
| Devices Management       | Incrementale | Requisiti chiari, soluzione da perfezionare              |
| Devices Registration     | Incrementale | Requisiti chiari, più soluzioni tecniche possibili       |
| Presentation             | Incrementale | Requisiti stabili, prototipazione iterativa con feedback |
| Users Management         | Lineare      | Scope ben definito, COTS disponibili                     |
| Notifications Management | Lineare      | Requisiti semplici e ben compresi                        |
| Permissions Management   | Iterativo    | Complessità, necessità di feedback utenti                |

### Time and Cost Summary

|                                 |                                                                                    |
| ------------------------------- | ---------------------------------------------------------------------------------- |
| Durata stimata                  | 54 settimane (critical path) + 3 settimane (management reserve) = **57 settimane** |
| Team                            | 10 persone (9 full-time + 1 part-time)                                             |
| Costo totale stimato            | **~€460.000** (inclusa management reserve)                                         |
| Budget disponibile              | €2.000.000                                                                         |
| Massima esposizione finanziaria | €148.000 (al termine del Q3)                                                       |
| Critical path                   | Pianificazione → Protocol → Devices Mgmt → Presentation → Testing → Chiusura       |

## Matrice RASCI

Matrice di assegnazione responsabilità per le macro-attività della WBS. Leggenda: **R** = Responsible, **A** = Accountable, **S** = Support, **C** = Consulted, **I** = Informed.

<table>
  <tr>
    <th>Macro-attività</th><th>PM</th><th>SD1</th><th>SD2</th><th>D1</th><th>D2</th><th>D3</th><th>D4</th><th>UX</th><th>QA</th><th>IoT</th>
  </tr>
  <tr>
    <td>1.1 Project Management</td><td>R/A</td><td>C</td><td>C</td><td>I</td><td>I</td><td>I</td><td>I</td><td>I</td><td>I</td><td>I</td>
  </tr>
  <tr>
    <td>1.2 Devices Protocol</td><td>A</td><td>R</td><td>C</td><td>S</td><td></td><td></td><td></td><td></td><td>S</td><td>R</td>
  </tr>
  <tr>
  <td>1.3 Users Management</td><td>A</td><td>C</td><td>S</td><td></td><td>R</td><td></td><td></td><td></td><td>S</td><td></td>
  </tr>
  <tr>
  <td>1.4 Devices Management</td><td>A</td><td>C</td><td>C</td><td>R</td><td>S</td><td></td><td></td><td></td><td>S</td><td></td>
  </tr>
  <tr>
  <td>1.5 Devices Registration</td><td>A</td><td>R</td><td>C</td><td>S</td><td></td><td></td><td></td><td></td><td>S</td><td>C</td>
  </tr>
  <tr>
  <td>1.6 Scripts Management</td><td>A</td><td>C</td><td>R</td><td></td><td></td><td>S</td><td>S</td><td>S</td><td>S</td><td></td>
  </tr>
  <tr>
  <td>1.7 Permissions Management</td><td>A/S</td><td>C</td><td>C</td><td></td><td>R</td><td></td><td>S</td><td></td><td>S</td><td></td>
  </tr>
  <tr>
  <td>1.8 Notifications Management</td><td>A</td><td>C</td><td></td><td></td><td></td><td></td><td>R</td><td></td><td>S</td><td></td>
  </tr>
  <tr>
  <td>1.9 Presentation</td><td>A</td><td>C</td><td>C</td><td>S</td><td>S</td><td>R</td><td></td><td>R</td><td>S</td><td></td>
  </tr>
  <tr>
  <td>1.10 Testing e Integrazione</td><td>A</td><td>S</td><td>S</td><td>S</td><td>S</td><td></td><td></td><td>S</td><td>R</td><td></td>
  </tr>
</table>

## Regole operative del team

### Problem Solving

| Step | Attività                                           | Output                                     |
| ---- | -------------------------------------------------- | ------------------------------------------ |
| 1    | Definire il problema e identificare l'owner        | Problem statement con owner assegnato      |
| 2    | Raccogliere i dati rilevanti e analizzare le cause | Root cause analysis                        |
| 3    | Generare delle idee (brainstorming/analisi)        | Lista di possibili soluzioni               |
| 4    | Valutare e assegnare una priorità alle idee        | Ranking delle soluzioni                    |
| 5    | Sviluppare un piano d'azione                       | Action plan con responsabili e tempistiche |

Se la soluzione non è soddisfacente, il processo viene ripetuto dal punto 1 o 2.

### Decision Making

| Contesto                                         | Stile                              | Esempio                                                                                       |
| ------------------------------------------------ | ---------------------------------- | --------------------------------------------------------------------------------------------- |
| Gestione progetto (scheduling, risorse, riserva) | Directive (PM)                     | Il PM decide di spostare un task non critico per risolvere una over-allocation                |
| Sprint planning sottosistemi adattivi            | Participative/Collaborative        | Tutto il sub-team del Protocol decide quali funzionalità affrontare nella prossima iterazione |
| Scelte architetturali significative              | Consultative                       | SD1 decide l'architettura del protocollo dopo aver raccolto input dal team                    |
| Decisioni urgenti bloccanti                      | Directive (PM o SD di riferimento) | Il PM assegna una risorsa di supporto per sbloccare un task critico                           |

### Conflict Resolution

Approccio basato sul modello Thomas-Kilmann, con la seguente scala di preferenza:

| Priorità | Approccio                   | Quando utilizzarlo                                                |
| -------- | --------------------------- | ----------------------------------------------------------------- |
| 1        | Collaborating (Integration) | Prima scelta: cercare soluzioni win-win                           |
| 2        | Compromising (Sharing)      | Disaccordo persistente su scelte tecniche                         |
| 3        | Competing (Domination)      | Solo per decisioni urgenti critiche (riservato al PM)             |
| -        | Avoiding (Neglect)          | **Non accettabile**: i conflitti vanno affrontati tempestivamente |

### Consensus Building

Il consenso è la modalità preferita per le decisioni importanti del team. Se non raggiunto in tempi ragionevoli, si passa all'approccio consultativo con decisione finale del PM o del Senior Developer di riferimento.

### Brainstorming

Regole concordate:

1. Riunire chi ha conoscenza dell'ambito
2. Raccogliere tutte le idee senza giudizio iniziale
3. Continuare finché le idee non si esauriscono
4. Discutere tutte le idee con apertura mentale
5. Convergere verso la soluzione

Contesti di utilizzo previsti: sprint planning (sottosistemi adattivi), fase di generazione idee nel problem solving, esplorazione di alternative architetturali o di design.

### Team Meetings

**Daily Status Meeting** — Durata: 15 min, frequenza: giornaliera, formato: in piedi

Partecipano tutti i membri attivi. Si discutono solo i task aperti. Ogni responsabile riporta lo stato con una delle seguenti formulazioni:

- "Sono in schedule"
- "Sono in ritardo di X ore, ma prevedo di rientrare entro Y giorni"
- "Sono in ritardo di X ore e ho bisogno di aiuto per recuperare"
- "Sono in anticipo di X ore e posso aiutare chi ha bisogno"

I problemi vengono solo segnalati, non risolti durante il daily.

**Problem Resolution Meeting** — Durata: variabile, frequenza: su richiesta

| Aspetto      | Dettaglio                                                                    |
| ------------ | ---------------------------------------------------------------------------- |
| Partecipanti | Solo chi è coinvolto nel problema                                            |
| Obiettivi    | Identificare l'owner, definire la soluzione, stabilire i criteri di verifica |
| Processo     | 5 step di Couger (vedi Problem Solving)                                      |

**Project Review Meeting** — Durata: 1-2 ore, frequenza: a ogni milestone

| Aspetto      | Dettaglio                                                                       |
| ------------ | ------------------------------------------------------------------------------- |
| Partecipanti | PM, senior management, CEO, investitori, stakeholder, tecnici esperti           |
| Obiettivi    | Presentare lo stato del progetto, revisione critica, proporre azioni correttive |

## Gestione dei cambiamenti di scope

### Processo di gestione

```
Richiesta di cambiamento (Scope Change Request Form)
    │
    ▼
Revisione iniziale (PM)
    │
    ├─── Rigetto ───► Fine
    ├─── Rinvio per rielaborazione ───► Ritorno al richiedente
    │
    ▼
Studio di impatto (Project Impact Statement)
    │
    ▼
Revisione con CEO e senior management
    │
    ├─── Rigetto ───► Fine
    ├─── Rinvio per rielaborazione ───► Ritorno allo studio di impatto
    │
    ▼
Approvazione ───► Ristrutturazione del piano di progetto
```

### Scope Change Request Form

| Campo                       | Descrizione                                          |
| --------------------------- | ---------------------------------------------------- |
| Nome progetto               | DomoticApp                                           |
| Richiesto da                | *(nome del richiedente)*                             |
| Data richiesta              | *(data)*                                             |
| Descrizione del cambiamento | *(descrizione dettagliata della modifica richiesta)* |
| Giustificazione di business | *(motivazione e beneficio atteso)*                   |
| Azione proposta             | *(azione raccomandata)*                              |
| Approvato da                | *(nome e ruolo)*                                     |
| Data approvazione           | *(data)*                                             |

### Project Impact Statement

Per ogni richiesta accettata per la valutazione, il PM con la collaborazione del team prepara un Project Impact Statement che risponde alle seguenti domande:

| Domanda                                                                                  | Risposta         |
| ---------------------------------------------------------------------------------------- | ---------------- |
| Qual è il beneficio atteso dal cambiamento?                                              | *(da compilare)* |
| Come impatterà il cambiamento sui costi?                                                 | *(da compilare)* |
| Come impatterà il cambiamento sulla schedule del progetto?                               | *(da compilare)* |
| Come impatterà il cambiamento sulla qualità della soluzione?                             | *(da compilare)* |
| Come impatterà il cambiamento sull'allocazione delle risorse?                            | *(da compilare)* |
| Il cambiamento può essere rimandato a un successivo stadio o prossima versione?          | *(da compilare)* |
| Il progetto è in uno stato in cui il cambiamento rischia di destabilizzare la soluzione? | *(da compilare)* |

**Possibili esiti della valutazione:**

1. Il cambiamento può essere applicato entro le risorse e i tempi previsti
2. Il cambiamento può essere applicato, ma richiede un'estensione della schedule
3. Il cambiamento può essere applicato entro la schedule, ma sono richieste ulteriori risorse
4. Il cambiamento richiede ulteriori risorse e un'estensione della schedule
5. Il cambiamento può essere applicato con strategia "multiple release" (prioritizzazione dei deliverable)
6. Il cambiamento non può essere applicato senza modifiche sostanziali del progetto

### Scope Bank

Per i sottosistemi con PMLC adattivo (Devices Protocol, Scripts Management) e iterativo (Permissions Management), è stato predisposto un registro (Scope Bank) per depositare i requisiti non ancora integrati nella soluzione:

| ID  | Requisito                             | Sottosistema | Priorità         | Sprint di origine | Stato                            |
| --- | ------------------------------------- | ------------ | ---------------- | ----------------- | -------------------------------- |
|     | *(da compilare durante l'esecuzione)* |              | Alta/Media/Bassa |                   | In attesa / Integrato / Scartato |

La Scope Bank viene rivalutata al termine di ogni iterazione per decidere quali requisiti includere nel prossimo ciclo.

## Piano delle comunicazioni

| Tipo di comunicazione                 | Canale                        | Frequenza                    | Partecipanti                            | Formato                |
| ------------------------------------- | ----------------------------- | ---------------------------- | --------------------------------------- | ---------------------- |
| Daily status                          | Riunione in piedi / Videocall | Giornaliera                  | Team completo                           | Orale, 15 min          |
| Aggiornamento stato task              | Tool di project management    | Continuo                     | Team completo                           | Aggiornamento digitale |
| Comunicazione rapida                  | Piattaforma messaggistica     | Continuo                     | Team completo                           | Chat                   |
| Code review                           | Repository Git (Pull Request) | Ad ogni commit significativo | Sviluppatori                            | Review scritta         |
| Problem resolution                    | Riunione dedicata             | Su richiesta                 | Solo coinvolti                          | Orale + verbale        |
| Sprint review (sottosistemi adattivi) | Riunione formale              | Fine iterazione              | Sub-team + CEO (o delegato)             | Presentazione + demo   |
| Report di avanzamento                 | Email / Documento             | Settimanale                  | PM → Stakeholder                        | Report scritto         |
| Project review (milestone)            | Riunione formale              | A ogni milestone             | PM, senior management, CEO, investitori | Presentazione formale  |
| Comunicazioni con investitori         | Email formale                 | Mensile / A milestone        | PM → Investitori                        | Report formale         |
| Documentazione tecnica                | Wiki condivisa                | Continuo                     | Team sviluppo                           | Documento tecnico      |

**Interfacce di comunicazione del PM:**

| Interfaccia            | Contenuti principali                                        | Frequenza                       |
| ---------------------- | ----------------------------------------------------------- | ------------------------------- |
| PM ↔ CEO               | Decisioni di scope, approvazioni, review iterazioni         | Settimanale + a ogni iterazione |
| PM ↔ Investitori       | Aspetti economici, milestone, avanzamento                   | A milestone                     |
| PM ↔ Senior Management | Report di stato, escalation, richieste di risorse           | Settimanale                     |
| PM ↔ SD1, SD2          | Coordinamento tecnico, decisioni architetturali             | Giornaliera                     |
| PM ↔ Team              | Supporto operativo, assegnazione task, risoluzione problemi | Giornaliera                     |

## Work Packages

I work packages sono stati redatti prioritariamente per i task sul critical path, ad alto rischio e che richiedono risorse scarse.

### Work Package: Progettazione struttura protocollo (1.2.2)

| Campo                       | Valore                                                                                                                                                                                                             |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **WBS ID**                  | 1.2.2                                                                                                                                                                                                              |
| **Nome**                    | Progettazione struttura protocollo                                                                                                                                                                                 |
| **Responsabile**            | SD1                                                                                                                                                                                                                |
| **Risorse assegnate**       | SD1, IoT Specialist                                                                                                                                                                                                |
| **Durata stimata**          | 3 settimane                                                                                                                                                                                                        |
| **Predecessori**            | 1.2.1 (Analisi dispositivi IoT esistenti)                                                                                                                                                                          |
| **Successori**              | 1.2.3 (Implementazione parser protocollo)                                                                                                                                                                          |
| **Descrizione**             | Progettare la struttura del protocollo comune basandosi sull'analisi dei dispositivi esistenti. Definire il formato per proprietà, azioni ed eventi dei dispositivi. Produrre la specifica formale del protocollo. |
| **Deliverable**             | Specifica formale del protocollo (documento)                                                                                                                                                                       |
| **Criteri di accettazione** | Il protocollo deve supportare almeno l'80% dei dispositivi analizzati. La specifica deve essere validata dallo specialista IoT.                                                                                    |
| **Rischi**                  | Incompatibilità tra dispositivi eterogenei; complessità eccessiva del protocollo                                                                                                                                   |
| **Note**                    | Task sul critical path. Lo specialista IoT è disponibile part-time (3 gg/settimana). Previste sessioni di brainstorming per esplorare alternative.                                                                 |

### Work Package: Implementazione parser protocollo (1.2.3)

| Campo                       | Valore                                                                                                                                                                             |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **WBS ID**                  | 1.2.3                                                                                                                                                                              |
| **Nome**                    | Implementazione parser protocollo                                                                                                                                                  |
| **Responsabile**            | SD1                                                                                                                                                                                |
| **Risorse assegnate**       | SD1, D1                                                                                                                                                                            |
| **Durata stimata**          | 4 settimane                                                                                                                                                                        |
| **Predecessori**            | 1.2.2 (Progettazione struttura protocollo)                                                                                                                                         |
| **Successori**              | 1.2.4 (Test protocollo sui dispositivi)                                                                                                                                            |
| **Descrizione**             | Implementare il parser del protocollo secondo la specifica prodotta nel task precedente. Implementare la serializzazione/deserializzazione dei messaggi e la validazione dei dati. |
| **Deliverable**             | Parser protocollo funzionante con unit test                                                                                                                                        |
| **Criteri di accettazione** | Tutti gli unit test passano. Test coverage > 80%. Compatibilità verificata con i formati definiti nella specifica.                                                                 |
| **Rischi**                  | Prestazioni insufficienti del parsing; ambiguità nella specifica del protocollo                                                                                                    |
| **Note**                    | Task sul critical path con la durata più lunga nel sottosistema Protocol. Richiede coordinamento stretto tra SD1 e D1.                                                             |

### Work Package: Implementazione visualizzazione dispositivi (1.4.2)

| Campo                       | Valore                                                                                                                                                         |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **WBS ID**                  | 1.4.2                                                                                                                                                          |
| **Nome**                    | Implementazione visualizzazione dispositivi                                                                                                                    |
| **Responsabile**            | D1                                                                                                                                                             |
| **Risorse assegnate**       | D1                                                                                                                                                             |
| **Durata stimata**          | 3 settimane                                                                                                                                                    |
| **Predecessori**            | 1.4.1 (Implementazione CRUD gruppi)                                                                                                                            |
| **Successori**              | 1.4.3 (Implementazione azioni su dispositivi)                                                                                                                  |
| **Descrizione**             | Implementare le API e la logica per la visualizzazione dei dispositivi registrati, dei gruppi e delle proprietà in tempo reale tramite il protocollo definito. |
| **Deliverable**             | API di visualizzazione dispositivi funzionanti con test                                                                                                        |
| **Criteri di accettazione** | Le API restituiscono correttamente stato e proprietà di tutti i dispositivi registrati. Tempi di risposta < 500ms.                                             |
| **Rischi**                  | Problemi di performance con molti dispositivi connessi simultaneamente                                                                                         |
| **Note**                    | Task sul critical path. D1 lavora da solo su questo task: assicurarsi che non sia bloccato da dipendenze esterne.                                              |

### Work Package: Collegamento frontend-backend (1.9.4)

| Campo                       | Valore                                                                                                                                                                             |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **WBS ID**                  | 1.9.4                                                                                                                                                                              |
| **Nome**                    | Collegamento frontend-backend                                                                                                                                                      |
| **Responsabile**            | D1                                                                                                                                                                                 |
| **Risorse assegnate**       | D1, D2                                                                                                                                                                             |
| **Durata stimata**          | 4 settimane                                                                                                                                                                        |
| **Predecessori**            | 1.9.3 (Implementazione pagine admin)                                                                                                                                               |
| **Successori**              | 1.9.5 (Test UX e prototipi), 1.10.1 (Test di integrazione)                                                                                                                         |
| **Descrizione**             | Integrare le pagine frontend con le API backend completate. Implementare la comunicazione real-time per l'aggiornamento dello stato dei dispositivi e la gestione delle notifiche. |
| **Deliverable**             | Applicazione web funzionante end-to-end                                                                                                                                            |
| **Criteri di accettazione** | Tutte le pagine utente e admin sono correttamente collegate alle API. Lo stato dei dispositivi si aggiorna in tempo reale.                                                         |
| **Rischi**                  | Incompatibilità tra interfacce frontend e backend; problemi di latenza nella comunicazione real-time                                                                               |
| **Note**                    | Task sul critical path. Richiede che le API di tutti i sottosistemi siano completate e stabili.                                                                                    |

### Work Package: Test di integrazione (1.10.1)

| Campo                       | Valore                                                                                                                                                                              |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **WBS ID**                  | 1.10.1                                                                                                                                                                              |
| **Nome**                    | Test di integrazione dei sottosistemi                                                                                                                                               |
| **Responsabile**            | QA                                                                                                                                                                                  |
| **Risorse assegnate**       | QA, SD1, SD2                                                                                                                                                                        |
| **Durata stimata**          | 3 settimane                                                                                                                                                                         |
| **Predecessori**            | 1.9.4 (Collegamento frontend-backend), completamento test dei singoli sottosistemi                                                                                                  |
| **Successori**              | 1.10.2 (Test end-to-end)                                                                                                                                                            |
| **Descrizione**             | Verificare il corretto funzionamento dell'integrazione tra tutti i sottosistemi: protocollo ↔ registrazione ↔ gestione dispositivi ↔ script ↔ permessi ↔ notifiche ↔ presentazione. |
| **Deliverable**             | Report di integrazione con lista bug e stato                                                                                                                                        |
| **Criteri di accettazione** | Tutti i flussi principali (registrazione dispositivo → visualizzazione → azione → notifica) funzionano end-to-end. Zero bug bloccanti.                                              |
| **Rischi**                  | Bug di integrazione non previsti tra sottosistemi sviluppati indipendentemente                                                                                                      |
| **Note**                    | Task sul critical path. SD1 e SD2 supportano QA per la risoluzione rapida dei bug di integrazione.                                                                                  |

## Monitoring e Controlling

### Tipi di report

| Tipo di report            | Destinatari            | Contenuto                                                                    | Frequenza    |
| ------------------------- | ---------------------- | ---------------------------------------------------------------------------- | ------------ |
| **Current Period Report** | Team, PM               | Attività completate, variazioni rispetto al piano, cause e misure correttive | Settimanale  |
| **Cumulative Report**     | PM, senior management  | Trend completo del progetto, evoluzione scostamenti nel tempo                | A milestone  |
| **Exception Report**      | Senior management, CEO | Solo scostamenti rispetto al piano, cause e misure correttive (sintetico)    | Su necessità |
| **Variance Report**       | PM, team               | Confronto pianificato vs. effettivo per ogni attività e periodo              | Settimanale  |

### Earned Value Analysis

| Grandezza                            | Formula            | Descrizione                                 |
| ------------------------------------ | ------------------ | ------------------------------------------- |
| **PV** (Planned Value)               | Da baseline        | Valore del lavoro pianificato alla data     |
| **EV** (Earned Value)                | Da % completamento | Valore del lavoro effettivamente completato |
| **AC** (Actual Cost)                 | Consuntivo         | Costo effettivamente sostenuto              |
| **SPI** (Schedule Performance Index) | EV / PV            | < 1: in ritardo; > 1: in anticipo           |
| **CPI** (Cost Performance Index)     | EV / AC            | < 1: oltre il budget; > 1: sotto il budget  |

**Tabella di tracking EVA (da compilare settimanalmente):**

| Settimana                             | PV (€) | EV (€) | AC (€) | SPI | CPI | Note |
| ------------------------------------- | ------ | ------ | ------ | --- | --- | ---- |
| *(da compilare durante l'esecuzione)* |        |        |        |     |     |      |

### Scope Bank

| Data                                  | Operazione          | Descrizione                                 | Tempo depositato | Tempo prelevato | Saldo | Autorizzato da |
| ------------------------------------- | ------------------- | ------------------------------------------- | ---------------- | --------------- | ----- | -------------- |
| Inizio progetto                       | Deposito iniziale   | Riserva iniziale (~5-10% tempo complessivo) |                  |                 |       | PM             |
| *(da compilare durante l'esecuzione)* | Deposito / Prelievo |                                             |                  |                 |       | CEO / PM       |

### Issues Log

| ID                                    | Data | Descrizione problema | Impatto se non risolto | Problem owner | Azione da intraprendere | Stato                  | Esito |
| ------------------------------------- | ---- | -------------------- | ---------------------- | ------------- | ----------------------- | ---------------------- | ----- |
| *(da compilare durante l'esecuzione)* |      |                      |                        |               |                         | Aperto/In corso/Chiuso |       |
