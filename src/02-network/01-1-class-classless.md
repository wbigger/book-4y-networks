# Classful e classless
Prima di andare avanti, è necessario fare un approfondimento storico, per capire meglio il presente.

Il metodo che abbiamo visto di calcolare la maschera di sottorete utilizzando il numero esatto di bit, è attualmente lo standard e viene chiamato CIDR (Classless Inter-Domain Routing). Fate attenzione alla parola _classless_, che in italiano si può tradurre con "senza classi": per capire a cosa si riferisce, bisogna addentrarsi un po' nella storia.

## Classi di indirizzi IP
Quando è nato Internet, negli anni '70, la maschera di sottorete era unica e fissa per tutti gli indirizzi IP, ed era di 8 bit. C'erano quindi solo 254 reti, ognuna con circa 16 milioni di dispositivi.

Quando negli anni '80 la tecnologia di Internet prese piede a livello mondiale, ci fu la necessità di mettere a disposizione un maggior numero di reti. Si decise quindi di cambiare un po' strategia e di assegnare delle maschere di rete in automatico in base ai primi bit dell'indirizzo IP.

Decisero di divedere gli indirizi IP in tre _classi_:
- **classe A**: il primo bit dell'indirizzo è 0, mantiene la maschera a 8 bit
- **classe B**: il primo bit dell'indirizzo è 1 e il secondo 0, viene assegnata una maschera a 16 bit
- **classe C**: i primi due bit dell'indirizzo sono entrambi 1 ed il terzo a 0, viene assegnata una maschera a 24 bit

In questo modo, il numero di reti assegnabili aumentò notevolmente e per un po' si andò avanti così.

> Per completezza, esistono altre due classi, la D e la E, in base al valore del terzo e quarto bit. Noi non le tratteremo.

### Una scelta infelice
Nel passare alle classi, ci fu la necessità di rappresentare in qualche modo la maschera di sottorete. Decisero di rappresentare le maschere con la stessa notazione in 4 ottetti degli indirizzi IP, in cui venivano valorizzati ad 1 il numero di bit della maschera di sottorete. Si ottenne il risultato seguente:

- per la classe A: 255.0.0.0
- per la classe B: 255.255.0.0
- per la classe C: 255.255.255.0

Questa scelta fu un po' infelice, perché ha una serie di problemi:
1. la rappresentazione è uguale a quella degli indirizzi IP, nonostante sia un concetto completamente diverso, portando quindi ad una certa confusione
1. la rappresentazione è molto prolissa, quando viene scritta usa molti più caratteri di quanto potrebbero essere necessari
1. ci sono potenzialmente molte maschere di sottorete non valide. Ad esempio le maschere 255.255.235.0, 255.255.0.255 non hanno senso e sono invalide. Questo, insieme al punto precedente, porta ad un maggior rischio di errori
1. se il numero di bit della maschera non è moltiplo di 8 questa notazione diventa di difficile interpretazione. Ad esempio una maschera di 20 bit viene rappresentata come 255.255.240.0, ed una maschera di 14 bit come 255.252.0.0, e la conversione richiede un po' di calcoli e di pratica

Ad ogni modo, per diversi anni si è usata questa notazione e si trova molto spesso ancora in giro, quindi è di fondamentale importanza comprendere il significato di queste maschere e saper passare dalla notazione ad ottetti alla notazione slash e viceversa.

## Indirizzi IP senza classi
Il problema dell'assegnazione degli indirizzi si ripresentò verso la fine degli anni '80, in particolare per gli indirizzi di classe C: la nuova Internet Economy vedeva fiorire molte piccole aziende che avevano bisogno di pochi indirizzi IP, ma si trovavano costrette A pagare alte somme per avere un indirizzo di classe C, che per la maggior parte non utilizzavano.

Per cui, agli inizi degli anni '90 si cambiò di nuovo sistema, abbandonando il concetto di classe: ogni indirizzo IP, indipendentemente dal suo valore numerico, poteva avere una qualsiasi maschera di sottorete. Si passò contestualmente anche alla notazione slash, più compatta e chiara, che è ancora lo standard attuale.

> Alcuni enti ed aziende hanno mantenuto la proprietà di interi blocchi di classe A anche dopo il passaggio a CIDR. Per un elenco completo, guardate [questa pagina](https://en.wikipedia.org/wiki/List_of_assigned_/8_IPv4_address_blocks). La lista è molto interessante perché fa capire ancora oggi quali sono le influenze ed i rapporti di potere nel mondo di Internet!


## Passaggio da notazione ad ottetti a notazione slash
È importante saper passare da una notazione all'altra, perché nella pratica le troverete tutte e due.

### Da ottetti a slash
Per passare da ottetti a slash, bisogna prima di tutto convertire ogni singolo ottetto in slash. Prendiamo ad esempio la maschera `255.255.240.0`. Il numero 255 è facilmente convertibile: sono otto bit tutti a 1. Per il terzo ottetto, 240, bisogna scomportlo in binario. Ci sono vari metodi che avete studiato a TPSI; io uso il seguente modo semi-empirico, ma vanno tutti bene.

Mi scrivo la seguente tabellina.

|128|64|32|16|8|4|2|1|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|_|_|_|_|_|_|_|_|

Ora metto degli 1 in modo che la somma dei numeri che stanno sopra mi dia esattamente il numero che cerco. Nel nostro caso, per ottenere 240, devo mettere 1 nelle prime quattro caselle.

|128|64|32|16|8|4|2|1|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|1|1|1|1|_|_|_|_|

In tutte le altre caselle metto 0, ottenendo infine il seguente risultato.

|128|64|32|16|8|4|2|1|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|1|1|1|1|0|0|0|0|

Mi sono calcolato così che il numero `240` in decimale si converte in `11110000` in binario.

Ora metto tutti gli ottetti in fila.

<p class="centered">
<strong>
255.255.255.0<br>
11111111.11111111.11110000.00000000
</strong>
</p>

Conto gli uno a partire dall'inizio, sono 8 + 8 + 4 = 20. Sono arrivato alla fine: la subnet mask in slash notation vale proprio 20!

<p class="centered xxl-font">
<strong>
255.255.240.0 -> /20
</strong>
</p>

### Da slash a ottetti
Bisogna fare l'operazione inversa del paragrafo precedente. Ipotizziamo di avere la subnet `\27`. Per convertirla in ottetti, metto 27 bit a 1 di fila, separandoli a gruppi di 8 bit.

<p class="centered xxl-font">
<strong>
11111111.11111111.11111111.11100000
</strong>
</p>

I primi tre ottetti si calcolano immediatamente, perché essendo tutti 1 valgono 255. Per l'ultimo ottetto, faccio il calcolo, sempre usando la tabella di prima.

|128|64|32|16|8|4|2|1|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|1|1|1|0|0|0|0|0|

Quindi il numero che cerco è 128+64+32, che vale `224`. A questo punto abbiamo finito, la conversione diventa come segue.

<p class="centered xxl-font">
<strong>
/27 -> 255.255.255.224
</strong>
</p>
