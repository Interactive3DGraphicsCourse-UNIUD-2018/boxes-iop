# Report di progetto - Turus Davide, Iop Alessandro
## Parte 1: idee
La prima idea era stata di realizzare un'ambientazione ricollegabile al Signore Degli Anelli, in particolare le fortezze di Minas Tirith o di Barad-Dur, con particolare cura nei dettagli architettonici. L'animazione sarebbe stata il movimento delle mura che crollano nel primo caso e il movimento dell'occhio di Sauron assieme all'apertura dei cancelli neri nel secondo. Tuttavia, per motivi di tempo e originalità della stessa, l'idea è stata subito scartata.
La scelta è stata quindi di optare per la costruzione di un ambiente rappresentante la base di lancio di uno space shuttle. Per l'animazione si è optato di rappresentare il lancio dello stesso, con effetti di fiamme e fumo alla base, nonché la rotazione dei bracci meccanici della torre per simulare la ripresa di un lancio spaziale.

|![Scene graph](media/scenegraph.png)|
|:--:|
|*Scenegraph generale degli oggetti contenuti in scene.*|

## Parte 2: modellazione dello space shuttle
Al fine di rendere il lavoro di realizzazione più semplice e veloce possibile, lo shuttle è stato modellato a partire da un parallelepipedo centrale con funzione di "scheletro", sulla superficie del quale sono stati poi apposti dei box più piccoli, di dimensioni variabili, per definire i dettagli e le componenti del veicolo più piccole. Sono state realizzate, tra le altre cose, le ali, i propulsori, la punta, il serbatoio e i razzi. Tutte le componenti sono modulari e dipendono da tre variabili numeriche indicanti approssimativamente le dimensioni del suddetto "scheletro", in forma di sottrazione o di divisione di tali parametri; le proporzioni del velivolo sono quindi impostate "ad occhio".
In una seconda fase, sono state progettate le prime animazioni da applicare successivamente, cioè il movimento dello shuttle in alto preceduto dalla rotazione/ritrazione dei bracci della torre di lancio. E' seguito lo sviluppo delle fiamme e la colonna di fumo che si sprigionano dai propulsori dello shuttle. Questi elementi sono generati e gestiti come entità separate, create e animate in funzioni separate all'interno del codice, "attaccate" alla base del veicolo che funge da pivot.

|![Inspiration model](media/Shuttle_proiezioni.jpg)|
|:--:|
|*Modello d'ispirazione alle forme e ai colori dello space shuttle, trovato in [questo sito](https://ideas.lego.com/projects/50a447cc-0acb-4fff-b3c9-41739fed157c).*|

## Parte 3: animazioni
Inizialmente l'idea per le animazioni era quella di permettere all'utente di controllare quando far partire lo space shuttle, e far "scorrere" lo sfondo attorno ad esso in modo da produrre una transizione da un cielo atmosferico a uno spaziale. Tuttavia, per motivi di semplicità e per un desiderio di sviluppare il meglio possibile le animazioni legati al solo movimento dello shuttle, la maggior parte della concentrazione è stata posta nella realizzazione del riposizionamento del veicolo una volta finita l'animazione e nella cura degli effetti di fumo e fuoco, oltre al movimento delle braccia della torre di lancio. Quello che succede durante il suddetto riposizionamento è una modifica della visibilità del fumo e delle fiamme, in modo che i propulsori sembrino spenti, e un successivo riposizionamento una volta che lo shuttle è tornato alla posizione di partenza. Al posto del controllo dell'utente, l'intera animazione è stata fatta proseguire in loop all'infinito: non venendosi a creare nuovi oggetti durante i suddetti effetti legati al movimento, il frame rate non ne soffre.

## Parte 4: generazione del terreno e sfondo
Per evitare una riduzione degli fps ulteriore, considerando che già le animazioni risultano piuttosto impegnative da questo punto di vista, lo sviluppo del terreno a partire da una heightmap è stato volutamente progettato in maniera essenziale e "minimalista". In virtù di questo, la mappatura dei livelli di grigio in tipologie di terreno distinte è implementata per "fasce": ai valori di grigio inferiori a una certa soglia corrisponde un colore simile a quello dell'acqua, a quelli superiori a un'altra soglia corrispondono dei colori che emulano la terra, a quelli compresi tra esse dei colori che ricordano la sabbia. La mappatura dei livelli di grigio avviene anche, ovviamente, sull'altezza dei box che compongono il terreno, uno per ogni pixel logico della heightmap. La scelta di non applicare una texture a ognuno di essi, bensì un colore "piatto", è dovuta a una questione di uniformità a uno stile volutamente cartoon, dalle forme squadrate e colori vivaci.
Per quanto riguarda lo sfondo della scena, per non accontentarsi di un banale colore azzurro cielo si è optato per la generazione di una sfera contenitiva dello space shuttle e del terreno su cui poggia. L'obiettivo è chiaramente quello di applicarvi una texture sulla faccia interna, che risulta essere l'unica visibile, raffigurante un ambiente "spaziale".

|![Star background](textures/2k_stars.jpg)|
|:--:|
|*Sfondo utilizzato nella faccia interna della sfera, trovato in [questo sito](https://www.solarsystemscope.com/textures/).*|

## Parte 5: integrazione del codice
Come è possibile attestare, l'intero codice è contenuto in un unico file complessivo, che non ricorre quindi a chiamate esterne se non alla libreria di three.js. La decisione è dovuta principalmente alla necessità di avere sempre il codice sotto mano per tutte le componenti (strutturali e di animazione), oltre a facilitare la gestione delle variabili globali e il passaggio di parametri tra le funzioni. Durante lo sviluppo del progetto si è adottato, in generale, un approccio "incrementale": si procedeva per piccole introduzioni, che venivano testate isolatamente, per poi venire integrate a gruppi o singolarmente; ad ogni step si verificava che il codice funzionasse come desiderato prima di procedere allo step successivo. Particolare cura è stata posta nella regolazione dei parametri di animazione, in ottica di un risparmio di fps e in vista della generazione finale del terreno (vedi parte 3). Una volta introdotte tutte le componenti nel codice, ci si è preoccupati di aggiustare i dettagli di presentazione.

## Parte 6: risultati
Vengono presentati di seguito alcuni screenshot del lavoro in fase di sviluppo e a lavoro finito, accompagnato da alcune gif integrative.

|![Shuttle still](media/screen6.png)|
|:--:|
|*Space shuttle fermo sulla base di lancio, con sfondo stellato e terreno "lunare".*|

|![Shuttle animation](media/screen7.png)|
|:--:|
|*Space shuttle in fase di partenza, con effetti di fiamme e fumo che si sprigionano dai propulsori.*|

|![Star background](media/shuttle4.gif)|
|:--:|
|*Fase di lancio dello space shuttle, una volta aperte del tutto le braccia della torre, con movimento panoramico della camera.*|

|![Star background](media/shuttle3.gif)|
|:--:|
|*Fase di riposizionamento dello space shuttle sulla base di lancio, una volta terminata l'animazione*|