# Keyclick
History of Multitasking

---

La prima volta che ho sentito parlare di multitasking fu quando vidi la pubblicità di Apple alla fine degli anni 80, o inizio 90, ero piccolissimo, ma ricordo che c'era una persona che usava il PC e nel frattempo stampava... ora vi sembrerà normale ma non lo era! Quando stampavate qualcosa si fermava tutto, il PC si bloccava e restava così fino a quando non finivi, e con le vecchie stampanti poteva servire molto tempo. Poi anni dopo vidi in edicola una rivista, si chiamava "DEV" ed era della casa editrice "InfoMedia", quella fu la mia prima rivista di informatica seria, quando non c'erano blog, tutorial e non c'era neanche il Web e i tutorial erano i libri e le riviste in edicola, e sulla copertina c'era un titolo che mi avrebbe portato a scoprire un mondo intero, il titolo era "TSR - Terminant and stay resident" e parlava di Keyclick.

Ma il multitasking che stavo vedendo era in gran parte un'illusione, una bugia che i nostri computer ci raccontano ogni singolo microsecondo.


## L'Archeologia del Multitasking

Quando oggi penso al multitasking immagino i laptop contemporanei con le loro decine di schede browser aperte, i loro programmi in background che scaricano aggiornamenti, le notifiche che si accumulano come neve in una tempesta digitale. Ma il vero multitasking, quello che avrebbe dovuto cambiare tutto, non era destinato al pubblico consumer come me. Il multitasking nacque negli anni Sessanta e Settanta nei laboratori dei mainframe, in ambienti sterili e controllati dove decine, centinaia di utenti dovevano condividere una singola macchina gigantesca, e dove ogni microsecondo di inattività della CPU era denaro letteralmente bruciato.

Negli anni Ottanta, quando quello spot andava in onda sui televisori, il Macintosh (o il PC compatibile, dipendeva da quanto ricchi fossero i tuoi genitori) era già capace di fare qualcosa di straordinario dal punto di vista informatico, **il time-sharing**. Cioè, il processore alternava con una velocità tale da essere imperscrutabile ai sensi fra diversi compiti. Stampava un po', poi tornava a mostrare il prompt di sistema, poi tornava a stampare. Così velocemente che il mio cervello che opera a velocità biologiche dell'ordine dei millisecondi, non poteva nemmeno percepire l'alternanza.

**Quel multitasking era in realtà pseudoparallelismo, un'illusione di simultaneità generata dall'illusione della velocità**



## La Rivista DEV e l'Epifania dei TSR

Ecco che arriviamo a quella rivista che mi ha cambiato la vita intellettuale, **DEV**, della casa editrice InfoMedia. Un nome bellissimo nella sua semplicità, non "Computer Today" o "Digital Magazine", ma semplicemente "DEV", per sviluppatori, per me che pensavo al film War Games e immaginavo un giorno di avere un modem digitale e non uno a toni acustici. Questa rivista capiva che il vero pubblico interessato al multitasking non era il consumatore medio che voleva semplicemente stampare mentre lavorava, era il programmatore, il warlock del software, colui che voleva fare qualcosa di radicalmente nuovo e potenzialmente pericoloso con il computer. E quel titolo sulla copertina, "TSR: Terminant and Stay Resident", era, consapevolmente o per caso fortunato, la descrizione più poetica possibile di una delle più straordinarie violazioni degli accordi impliciti fra programmi che il mondo informatico abbia mai conosciuto.

**Un TSR era un programma che, una volta caricato in memoria, si installava nei meandri del sistema e rimaneva lì, in agguato, aspettando il momento giusto per svegliarsi e fare quello per cui era stato progettato.** Poteva essere una cosa utile o come Keyclick che che produceva un suono ogni volta che premevate sulla tastiera, una cosa ludica. Dal punto di vista del DOS, il Re indiscusso dell'informatica popolare di metà anni Ottanta, i TSR erano **parassiti che si mangiavano la memoria disponibile** e creavano quella che avrebbe dovuto essere l'illusione del multitasking vero. Ma i TSR non stavano creando il multitasking nel senso che il sistema operativo lo capisse o lo autorizzasse ufficialmente. Stavano creando il multitasking nonostante il sistema operativo, contro il sistema operativo, erano atti di resistenza creativa che si muovevano nello spazio grigio fra "cosa è tecnicamente possibile" e "cosa è lecito, cosa è etico" e rappresentavano il primo vero tentativo di multitasking volontario e sotto il controllo dell'utente nell'informatica consumer, ma lo facevano in modo estremamente primitivo, quasi barbarico, rispetto ai sistemi sofisticati di time-sharing che già esistevano nei laboratori universitari.

Un sistema di time-sharing moderno (e lo erano già negli anni Settanta, nei laboratori di MIT o Stanford) aveva un vero scheduler, cioè un componente intelligente del sistema operativo che decideva quale processo eseguire, per quanto tempo, e in quale ordine, tenendo conto di priorità, deadline, risorse disponibili, e complesse metriche di fairness. Un TSR, invece era più vicino a un **interrupt handler** che si inseriva nei circuiti elettrici del sistema operativo come un ospite inaspettato che bussasse alla porta, scavalcasse le convenzioni sociali, e si agganciasse ai vostri nervi. Funzionava catturando interrupt hardware, soprattutto quelli della tastiera, Il DOS, che era una creatura ingenua e non aveva scelta architettonica, lo permetteva. E poi il TSR si rimetteva in ombra, in uno stato vegetativo, aspettando il prossimo interrupt con la pazienza di un predatore.

**Non era multitasking nel senso accademico. Era un colpo di stato microscopico, ripetuto migliaia di volte al secondo, perpetrato ai danni della tranquillità del sistema operativo.**

E questo è il tipo di meraviglia e di genio borderline che una rivista come DEV cercava di raccontare ai suoi lettori, ti mostrava l'assembly e il C e ti spiegava come si poteva forzare il computer a fare cose che non era stato progettato per fare... era la definizione di Hacking vera e propria. **Un HAcker è qualcuno che ha capito una cosa meglio di chi l'ha inventata**, e DEV ti faceva fare tutto utilizzando gli strumenti primitivi di cui disponevamo e l'inesauribile creatività dei programmatori che capivano il sistema down to the metal, fino ai transistor.


## Il Disk Operating System

Per capire veramente la magia nera dei TSR, bisogna capire il nemico, o meglio, la vittima. Il DOS era, per definizione generosa, un sistema operativo estremamente lineare. Non era stato progettato per il multitasking ma era stato pensato per un utentee una applicazione alla volta. Ma DOS, per quanto ingenuo, aveva comunque una struttura minimale, con un interrupt handler, cioè routine di codice che rispondevano a certi eventi hardware come quando premevate un tasto, in quel momento l'hardware della tastiera generava un interrupt (interruzione forzata) che diceva al processore "Ehi, basta quello che stai facendo, devi gestire un altra cosa". Quando caricavate un TSR, quello che faceva era relativamente semplice:

1) Il TSR prendeva il vecchio indirizzo dell'interrupt handler della tastiera (il vettore di interrupt) e lo salvava da qualche parte nella memoria.

2) Riscriveva quel vettore di interrupt per fargli puntare al suo proprio codice.

3) Il TSR dichiarava se stesso come "resident", cioè, diceva al DOS di non cancellare la sua memoria quando ritornava il controllo al prompt dei comandi.

Da quel momento in poi, ogni pressione di un tasto passava prima attraverso il codice del TSR che poteva decidere di fare qualcosa, e poi passava il controllo al vero interrupt handler della tastiera, fingendo che nulla fosse accaduto.

## Il Primo TSR

Keyclick fù il primo TRS commerciale per quanto ne sappia, e catturava l'immaginazione di un ragazzo che leggeva DEV, non faceva niente se non generare un click dalla cassa del computer mentre si usava la tastiera, banale direte... non lo era all'epoca sopratutto se pensate che funzionava mentre un altro programma era in esecuzione e vi ricordo che il PC si bloccava addirittura mentre si stampava all'epoca.

Dal punto di vista della sicurezza informatica moderna, è ovvio che **Keyclick era prototipo un cavallo di Troia**. Un criminale poteva inserire il file `KEYCLICK.COM` nel vostro `AUTOEXEC.BAT` (il file che DOS eseguiva automaticamente al boot), e da quel momento in poi BOOM, ma nessuno era collegato a Internet e quindi nessuno lo faceva. Comunque negli anni Ottanta, la consapevolezza della sicurezza era ancora primitiva come DOS stesso. Keyclick era presentato come uno strumento di utilità legittima, era una dimostrazione di cosa fosse possibile fare quando capivate il sistema operativo così profondamente da poter scavalcare i suoi stessi meccanismi di controllo.

## La Rivoluzione Silenziosa (nel senso che non faceva click)

Anni dopo il multitasking è diventato standard e quel processo ha perso tutto il suo carisma borderline, quando Microsoft lanciò Windows 3.0 nel 1990 stava presentando il suo primo OS che prendeva il controllo dell'hardware, aggirava DOS, e implementava il suo scheduler, il suo proprio sistema di gestione della memoria, il suo proprio modello di multitasking. Ma c'era una differenza rispetto ai TSR., il multitasking di Windows era trasparente e, almeno in teoria, sicuro. I TSR non sparirono subito, molti utenti DOS continuavano a usarli anche durante l'era Windows. Ma era chiaro che il futuro apparteneva al multitasking ufficiale, al multitasking che il sistema operativo stesso gestiva e controllava. E poi, nel 1995, arrivò appunto Windows 95. E poi Windows NT. E poi Linux (che per me era solo Slackware). E in ognuno di questi sistemi, il multitasking era la fondazione stessa su cui veniva costruito il sistema operativo.



## Quello Che Abbiamo Perso

Seduto qui, nel 2026, con uno smartphone in tasca che esegue simultaneamente migliaia di processi, che comunica con satelliti, che mi localizza con precisione di pochi metri, che mi mostra in tempo reale video trasmessi da telecamere dall'altra parte del pianeta, seduto qui, non provo più quella meraviglia che provavo da bambino davanti a quello schermo. Ma ogni volta che leggo di architetture di scheduling come CFS (Completely Fair Scheduler) di Linux, o il Time Slice Replacement di macOS mi ricordo ancora di quella rivista, DEV*, e di quel ragazzino, e mi ricordo di quel titolo sulla copertina.

**Resident.** Rimanere. Stare. Persistere nel sistema. Continuare a esistere anche dopo che il programma principale era finito. Fare cose che nessuno ufficialmente ti aveva autorizzato a fare.

Forse, in qualche modo **il multitasking è sempre stato questo**, un atto di persistenza, un rifiuto di accettare i vincoli seriali del sistema, un'insistenza che una macchina potesse fare più di una cosa alla volta, nonostante tutto.


### Cache Misses e Thrashing

**Quando fate un context switch, non state solo salvando e ripristinando i registri ma state demolendo l'intero universo di caching del processore.**

I processori moderni hanno cache L1, L2, L3, gerarchie di memoria sempre più grandi ma sempre più lente, progettate per mantenere i dati più frequentemente usati il più vicino possibile ai circuiti di calcolo. Quando l'editor di testo stava eseguendo, la CPU aveva pazientemente caricato nella cache i dati che l'editor usava frequentemente. La cache era "calda", cioè, ottimizzata per quel specifico pattern di accesso alla memoria, le pipeline era precaricate, il brach target buffer stava sospirando in attesa di verificare se la sua intuizione fosse giusta ma...

Poi fate un context switch al browser.

Il browser ha un pattern di accesso alla memoria completamente diverso, accede a diverse pagine di memoria e la vostra cache L3, che era perfettamente organizzata per l'editor, è ora completamente inutile per il browser che deve ricominciare da capo, causando **cache misses** come se piovesse, cioè situazioni in cui il processore chiede dati che non sono in cache e deve aspettare che vengano caricati dalla memoria principale, un'operazione che può costare 100-200 cicli di clock.



## L'Arbitro Computazionale

Ma nel multitasking come decide uno scheduler quale processo eseguire, e per quanto tempo? Gli algoritmi di scheduling sono un campo profondo della scienza informatica teorica e nel corso dei decenni, i ricercatori hanno sviluppato dozzine di algoritmi, ognuno con le sue proprietà matematiche. Negli anni Ottanta, quando avevo quella rivista DEV in mano, la maggior parte dei sistemi usava **Round Robin (RR) scheduling** o varianti semplici. L'idea era che ogni processo ottiene un time slice fisso, diciamo, 100 millisecondi, e quando il suo tempo scade, viene aggiunto di nuovo in fondo alla coda, e il processo successivo nella coda prende il controllo della CPU. Ma la fairness matematica non è la stessa cosa che l'efficienza computazionale e un processo I/O-bound, cioè uno che passa la maggior parte del tempo ad aspettare input/output, come un editor di testo che aspetta che voi digitiate, avrebbe potuto fare il suo lavoro in 5 millisecondi, ma deve aspettare fino al termine del suo time slice di 100 millisecondi prima di poter tornare in coda. **Spreco.**mE un processo CPU-bound, uno che esegue calcoli intensivi, potrebbe preferire time slice più lunghi per ridurre l'overhead del context switching ma non poteva chiederlo a nessuno. Così gli algoritmi si sono evoluti... 

1) **Priority scheduling**: in cui si assegnano priorità diverse ai processi, quelli a alta priorità ottengono più tempo. Ma così un processo a bassa priorità potrebbe non eseguire mai se continua a essere eclissato da processi ad alta priorità.

2) **Multilevel Feedback Queues (MLFQ)**: mantentiene più code, con priorità diverse, e adatta dinamicamente la priorità di un processo basandosi sulla sua storia di esecuzione. Un processo che usa il suo intero time slice in calcoli viene demandato a una coda a priorità inferiore (è probabilmente CPU-bound). Un processo che rilascia il suo time slice presto viene promosso (è probabilmente I/O-bound e reattivo). E' quasi biologico, come se il sistema operativo imparasse il comportamento di ogni processo.

E poi, nel 2007, arrivò **CFS (Completely Fair Scheduler)** in Linux, sviluppato da Ingo Molnàr, un sistema che implementa il concetto di "fairness virturale" e invece di dividere il tempo in time slice fissi mantiene un tracking del tempo di CPU virtualeche ogni processo ha ricevuto, e esegue il processo che ha ricevuto meno tempo di CPU. Inoltre, CFS usa red-black trees per mantenere l'efficienza computazionale anche con migliaia di processi.




### Priority Inversion

Nel 1997, c'è stato un incidente famoso che ha evidenziato i limiti dei sistemi di scheduling, forse ne avete sentito parlare, il Mars Pathfinder Priority Inversion Incident. Il Mars Pathfinder era un rover in movimento verso Marte che aveva compiti critici. Lo scheduler del suo sistema operativo real-time (VxWorks) era impostato per eseguire compiti critici ad alta priorità e compiti non critici a bassa priorità. Ma il task ad alta priorità stava aspettando un mutex (una primitiva di sincronizzazione) che era tenuto da un task a bassa priorità. Il task ad alta priorità non poteva continuare finchè il task a bassa priorità non rilasciava il mutex. Ma il task a bassa priorità era costantemente interrotto da task a priorità media che non aspettavano nulla. Il risultato fù un deadlock e il task che doveva controllare i motori del rover, era bloccato aspettando un task che non poteva eseguire perché altri task stavano usando la CPU.

I rover su Marte non hanno un servizio clienti da chiamare e mandare un tecnico non era possibile, si doveva risolvere il problema dalla Terra inviando comandi con un ritardo di comunicazione di 20 minuti. Quando gli ingegneri del JPL finalmente capirono il problema, la soluzione era un semplice flag software, **priority inheritance**, quando un task ad alta priorità aspetta un mutex tenuto da un task a bassa priorità, il task a bassa priorità eredita temporaneamente la priorità del task ad alta priorità, così può completare il suo compito critico e rilasciare il mutex.

**Questo incidente dimostra che anche la teoria perfetta dello scheduling di fronte alla complessità della realtà può avere problemi, per questo strumenti formali, verifiche matematiche, e sistemi di tipo forti sono il nostro miglior alleato**

Ora torniamo un attimo indietro, quando ero bambino davanti il multitasking era un fatto interessante su un processore a singolo core, poi nel 2005, i processori hanno smesso di aumentare la frequenza e hanno iniziato a moltiplicare i core e improvvisamente, il multitasking  è diventato fisico. Su un processore dualcore, due thread possono realmente eseguire in parallelo vero su due diversi core. Su un processore a 32 core come gli EPYC di AMD, potete eseguire 32 thread contemporaneamente e non è context switching ma vero paralelismo. Ma non furono tutte rose e fiori, il multitasking diventò simultaneamente più semplice e infinitamente più complesso. Più semplice perché ora avete davvero del vero parallelismo, ma infinitamente più complesso perché ora si doveva affrontare il problema della sincronizzazione. Con un singolo processore che faceva context switching veloce, in un dato momento, solo un thread eseguiva il codice e questo permetteva di scrivere codice "thread-unsafe" senza problemi finchè lo scheduler era veloce abbastanza. Ma con i multicore due thread potrebbero davvero accedere alla stessa memoria nello stesso momento e se thread A sta leggendo una variabile mentre thread B la sta scrivendo, cosa succede? Succede che si manifestano potenzialmente Bug che non potete riprodurre e che appaiono casualmente e che cambiano comportamento a seconda di quanto è veloce il vostro processore. E questo problema ha generato interi campi di ricerca.

E se pensate che sia complicato allacciate le cinture perché il vostro smartphone oggi ha probabilmente 8 core e ognuno esegue istruzioni multiple per ciclo di clock grazie a una instruction-level parallelism e con lei avete probabilmente decine di processi in esecuzione e centinaia di thread. Il sistema operativo esegue un load balancing fra i core, cercando di distribuire il carico di lavoro in modo che nessun core sia sovraccarico mentre altri sono inattivi. Avete un thermal throttling, cioè se un core diventa troppo caldo, il sistema operativo riduce automaticamente la sua frequenza per evitare il surriscaldamento e avete un dynamic voltage and frequency scaling (DVFS), cioè il sistema operativo riduce la frequenza della CPU quando la domanda di computazione è bassa, per risparmiare batteria. E tutto questo gira su un heterogeneous computing, cioè il vostro smartphone ha alcuni core "grandi" per compiti pesanti e altri core "piccoli" per compiti leggeri, e il sistema operativo decide intelligentemente quale core usare per quale task. E' un'ottimizzazione che avrebbe fatto impazzire i progettisti di sistemi degli anni Ottanta. E il sistema operativo cerca anche di schedulare thread che accedono alla memoria in modo da ridurre la contesa sul bus di memoria (memory bandwidth management). E tutto questo accade senza che voi dobbiate fare nulla e accade milioni di volte al secondo, ogni secondo.

### Altri Mostri

MA il multitaskare ha altri problemi e forse il più famoso è il Deadlock, un concetto che è stato formalizzato da Edward Dijkstra negli anni Sessanta, e la teoria è matematicamente elegante, quattro condizioni devono essere soddisfatte simultaneamente perché si verifichi un deadlock:

1. **Mutual Exclusion**: una risorsa può essere tenuta da un solo processo alla volta.
2. **Hold and Wait**: un processo che tiene una risorsa può aspettare altre risorse.
3. **No Preemption**: nessun processo può essere forzato a rilasciare una risorsa.
4. **Circular Wait**: esiste una catena circolare di processi, ognuno aspettando una risorsa tenuta dal prossimo.

Se riuscite a eliminare anche una sola di queste condizioni, il deadlock non può verificarsi, quindi in teoria è semplice ma pratica è un incubo perché nel momento in cui pendaste di non permettere la mutual exclusion tutti possono accedere alla risorsa nello stesso tempo e vi trovate di fronte al problema della race condition per cui due thread accedono alla stessa memoria nello stesso istante, ognuno leggendo un valore e poi scrivono il loro risultato, che sovrascrive quello dell'altro trasformando un tipo di bug in un altro tipo di bug, e poi c'è la starvation e un sacco di altri problemi.

### Il Teorema CAP

Nel 2000, Eric Brewer ha formulato quello che è diventato conosciuto come il **Teorema CAP** ceh dice che in un sistema distribuito, potete garantire al massimo due delle seguenti tre proprietà:

- **Consistency (Coerenza)**: tutti i nodi vedono gli stessi dati nello stesso momento.
- **Availability (Disponibilità)**: il sistema risponde sempre alle richieste.
- **Partition Tolerance (Tolleranza alle Partizioni)**: il sistema continua a funzionare anche se la rete è partita in due.

Se la rete tra il vostro data center A e il vostro data center B si rompe (partition), dovete scegliere se mantenete la coerenza (alcuni server rifiutano richieste) o mantenete la disponibilità (i server continuano a servire richieste, ma i dati divergono). Non c'è una risposta "giusta" ma dipende da quello che il vostro sistema deve fare. Amazon sceglie Availability, se la rete tra i data center si rompe, i server continuano a servire i clienti e accettano che i dati potrebbero essere incoerenti per un po'. Quando la rete si ripara, riconciliano i dati. Un sistema bancario sceglie la Consistency e se la rete si rompe, rifiuta transazioni piuttosto che rischiare che due versioni del vostro conto bancario divergono. Quindi il multitasking è difficile su una singola macchina e diventa impossibilmente complesso quando diventa distribuito E il vostro smartphone moderno? Anche lui è un sistema distribuito, ha il suo processore locale, ma comunica costantemente con server nel cloud, ha una cache locale, ma i dati su quei server potrebbero cambiare. E la vostra email potrebbe essere sincronizzato con il server Google mentre il vostro cliente locale sta leggendo un'email vecchia.

### Determinismo v Non Determinismo

E sorpresa delle sorprese il vostro multitasking moderno è fondamentalmente non deterministico e se eseguite lo stesso programma multithreaded due volte, con gli stessi input, su una macchina multicore non è garantito che otterrete gli stessi risultati nello stesso ordine. Questo a causa dell'interleaving dei thread che è dipendente da mille fattori, quanto tempo impiega la CPU a eseguire quella istruzione particolare (che dipende da cache hits/misses), la temperatura del processore, altri processi in esecuzione nel sistema, la fase lunare (okay, non proprio, ma quasi).

Ma non è solo un male, infatti significa che il sistema operativo e l'hardware possono fare ottimizzazioni aggressive senza doversi preoccupare di una sequenza di esecuzione globale ma è anche straordinariamente pericoloso per la correttezza perché un bug potrebbe manifestarsi una volta ogni milione di esecuzioni, e voi non riuscirete mai a riprodurlo nel vostro debugger. E c'è un campo di ricerca chiamato **runtime verification** che cerca di affrontare questo problema e invece di cercare di provare che un programma multithreaded è corretto (il che potrebbe essere impossibile), monitora l'esecuzione e controlla se certe invarianti vengono violate. Ma questo richiede una comprensione matematica formale di quali siano gli invarianti, e nel multitasking in generale, definire questi invarianti è una forma d'arte pericolosa.


---

https://it.wikipedia.org/wiki/Gruppo_Editoriale_Infomedia
