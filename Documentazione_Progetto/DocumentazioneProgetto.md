# Indice

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
- Procedura di installazione di un dispositivo per hostare l'applicativo in locale se richiesto.
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

| Da     | Voglio poter                                                                                                                        | così che                                                                                                                                   |
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
