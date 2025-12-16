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
| Restare nel budget                         | €5 M                                                                                                                            |
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
      <th>Scopo</th>
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
          <li> Almeno il 70% degli utenti che possiedono 4 o più dispositivi di tipologia diversa utilizzano l'applicativo insieme ai vecchi applicativi. </li>
          <li> Soddisfazione pari o superiore all'80% nelle recensioni. </li>
          <li> Aumento del guadagno annuale di almeno 15% entro 2 anni dalla fine del progetto. </li>
        </ul>
      </td>
    </tr>
    <tr>
      <th>Assunzioni</th>
      <td>
        <ul>
          <li> Gli utenti admin del sistema sono mediamente esperti di tecnologia. </li>
          <li>  </li>
        </ul>
      </td>
    </tr>
    <tr>
      <th>Rischi</th>
      <td></td>
    </tr>
    <tr>
      <th>Ostacoli</th>
      <td></td>
    </tr>
  </tbody>
</table>
