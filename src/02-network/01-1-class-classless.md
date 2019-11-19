# Classful e classless
Prima di andare avanti, è necessario fare un approfondimento storico, per capire meglio il presente.

Il metodo che abbiamo visto di calcolare la maschera di sottorete utilizzando il numero esatto di bit, è attualmente lo standard e viene chiamato CIDR (Classless Inter-Domain Routing). Fate attenzione alla parola _classless_, che in italiano si può tradurre con "senza classi": per capire a cosa si riferisce, bisogna addentrarsi un po' nella storia.

## Classi di indirizzi IP
Quando è nato Internet, negli anni '70, la maschera di sottorete era unica e fissa per tutti gli indirizzi IP, ed era di 8 bit. C'erano quindi solo 254 reti, ognuna con circa 16 milioni di dispositivi.

Quando negli anni '80 la tecnologia di Internet prese piede a livello mondiale, ci fu la necessità di mettere a disposizione un maggior numero di reti. Si decise quindi di cambiare un po' strategia e di assegnare delle maschere di rete in automatico in base ai primi bit dell'indirizzo IP.

Decisero di divedere gli indirizi IP in tre _classi_:
- **classe A**: il primo bit dell'indirizzo è 0, mantiene la maschera a 8 bit
- **classe B**: il primo bit dell'indirizzo è 1 e il secondo 0, viene assegnata una maschera a 16 bit
- **classe C**: i primi due bit dell'indirizzo sono entrambi 1, viene assegnata una maschera a 24 bit

In questo modo, il numero di reti assegnabili aumentò notevolmente e per un po' si andò avanti così.

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

TODO: Conversione da notazione slash ad ottetti...
