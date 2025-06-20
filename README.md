
# Dashboard 4 ristoranti

Sono da sempre un grande appassionato del programma "4 Ristoranti" di Sky e ultimamente una delle mie ipotesi era che l'ultimo ristoratore fosse penalizzato solamente per il fatto di essere ultimo. Ho voluto creare una dashboard sia per verificare che questa mia ipotesi fosse corretta (spoiler: no ) sia per vedere nel dettaglio le città e le regioni che avevano partecipato più volte al programma. Inoltre ho fatto un focus sulla categoria "Special" introdotta a partire dalla quarta stagione.


## Step

**Step 1: Data entry**. Ho iniziato in questo caso dal passaggio più lento e piu macchinoso di tutto il progetto, quello di raccogliere informazioni sulla puntata: Data, Stagione, Puntata, Località, Special (se presente) e punteggio di ogni singolo ristorante. Non avendo trovato una pagina dettagliata con le informazioni che cercavo ho dovuto guardare ogni puntata singolarmente e raccogliere i dati che mi servivano.

**Step 2: Creazione del DB**. Oltre alle informazioni sopra ho creato una colonna per la Zona della puntata (Nord,Sud,Centro,Estero), diverse colonne per alcuni flag (Special, Piato vegetariano, Portata special), il ristorante vincitore, il numero di categoria della puntata e il punteggio utilizzato (0-5, 0-10)

**Step 3: Connessione a PowerBI e creazione delle misure**. Una volta connesso al file Excel ho creato le diverse misure per le diverse visualizzazioni del report:

-**N Località** = 
DISTINCTCOUNT('DB Puntate'[Località])

-**N Ristoranti** = 
[Numero Puntate]*4

-**N Special** = 
DISTINCTCOUNT('DB Puntate'[Special])

-**Numero Puntate** = 
DISTINCTCOUNT('DB Puntate'[ID Ordine])

-**Punteggio più alto** = 
MAX('DB Puntate'[Punteggio Vincitore])

-**Punteggio più basso** = 
MIN('DB Puntate'[Punteggio più basso])


**Step 4: Progettazione della Dashboard**. La dashboard è divisa in 4 sezioni:

-**Navigation Page**: Pagina iniziale in cui c'è uno strumento di navigazione interattivo con collegamenti che portano alle altre sezioni della Dashboard

-**Sezione Location**: In questa sezione c'è la visualizzazione delle puntate per geografia. In alto ci sono 4 schede KPI che indicano il numero di puntate, il numero di ristoranti, il numero di località e il numero degli special. Il Grafico a mostra la % di puntate per Zona e il grafico a barre il numero di puntate per regione. Infine c'è una tabella in cui sono indicate tutte le città. Al lato di ogni pagina c'è una sezione dedicata ai filtri per selezionare una specifica stagione, puntata o la presenza della categoria special.

-**Sezione Special**: In questa sezione sono analizzate nel dettaglio le puntate che hanno la categoria special. In alto ci sono gli stessi KPI della prima pagina. Come grafici invece troviamo un grafico a barre che indica il numero di puntate per ogni portata dello special e un grafico ad albero che indica il numero di puntate per tipologia di special. Come nella prima pagina, è presente una tabella con lo special.

-**Sezione Recap**: Nella pagina finale sono presenti 3 schede kpi con la media del punteggio del vincitore, il punteggio massimo e il punteggio minimo di puntata. Nella parte principale c'è una tabella in cui in ogni riga c'è la descrizione e il risultato di ogni puntata. Tramite la formattazione condizionale in verde sono indicati i punteggi piu alti della puntata corrispondente e in rosso quelli piu bassi.

**Step 5: Navigazione e Formattazione**. Per rendere il report navigabile ho usato lo strumento di navigazione orizzontale nella navigation page e ho usato lo stesso strumento per le altre pagine ma in modo verticale e con altri colori. Per formattare le celle dell'ultima tabella ho usato le seguenti formule:

-**Formattazione Primo** = 
IF (
    SELECTEDVALUE ( 'DB Puntate'[Primo Ristorante] )
        = SELECTEDVALUE ( 'DB Puntate'[Punteggio Vincitore] ),
    "Verde",
    IF (
        SELECTEDVALUE ( 'DB Puntate'[Primo Ristorante] )
            = SELECTEDVALUE ( 'DB Puntate'[Punteggio più basso] ),
        "Rosso",
        "No"
    )
)


-**Formattazione Secondo** = 
IF (
    SELECTEDVALUE ( 'DB Puntate'[Secondo Ristorante] )
        = SELECTEDVALUE ( 'DB Puntate'[Punteggio Vincitore] ),
    "Verde",
    IF (
        SELECTEDVALUE ( 'DB Puntate'[Secondo Ristorante] )
            = SELECTEDVALUE ( 'DB Puntate'[Punteggio più basso] ),
        "Rosso",
        "No"
    )
)

-**Formattazione Terzo** = 
IF (
    SELECTEDVALUE ( 'DB Puntate'[Terzo Ristorante] )
        = SELECTEDVALUE ( 'DB Puntate'[Punteggio Vincitore] ),
    "Verde",
    IF (
        SELECTEDVALUE ( 'DB Puntate'[Terzo Ristorante] )
            = SELECTEDVALUE ( 'DB Puntate'[Punteggio più basso] ),
        "Rosso",
        "No"
    )
)

**Formattazione Quarto** = 
IF (
    SELECTEDVALUE ( 'DB Puntate'[Quarto Ristorante] )
        = SELECTEDVALUE ( 'DB Puntate'[Punteggio Vincitore] ),
    "Verde",
    IF (
        SELECTEDVALUE ( 'DB Puntate'[Quarto Ristorante] )
            = SELECTEDVALUE ( 'DB Puntate'[Punteggio più basso] ),
        "Rosso",
        "No"
    )
)
