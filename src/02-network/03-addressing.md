# IP addressing
Ora abbiamo tutti gli strumenti essenziali per fare consapevolmente il nostro lavoro di sistemista!

Nella pratica del lavoro di un amministratore di rete, una delle prime e fondamentali competenze è saper creare correttamente reti e sottoreti. Non c'è necessariamente una scelta giusta ed una sbagliata: come al solito, dipende dalle esigenze del cliente, dai vincoli di spesa e da requisiti di sicurezza ed efficienza. Sicuramente però un'adeguata scelta delle sottoreti permetterà di semplificare molto il lavoro in futuro, ed una scelta infelice può portare a notti insonni e malfunzionamenti. Gli alleati migliori in questo lavoro sono come al solito studio, esperienza e saper chiedere aiuto quando necessario :)

## Esempio di indirizzamento
Ipotizziamo che una scuola abbia appena messo in rete i propri computer e noi siamo i nuovi amministratori di rete. Per prima cosa, dobbiamo decidere come assegnare gli indirizzi IP.

I PC della scuola sono così distribuiti:
- 3 laboratori con 20 computer ognuno
- l'amministrazione usa 10 computer
- ci sono circa 100 docenti con ognuno uno o due dispositivi da connettere alla rete

OK. Per ogni rete che identifichiamo, dobbiamo individuare l'indirizzo di rete e la maschera di sottorete. Faccio notare che in questo momento non ci interessa se i dispositivi siano connessi fisicamente via switch oppure siano wireless. Nel nostro livello 3 della pila ISO/OSI, questo non ci importa. Detto questo...via!

Per prima cosa decidiamo di mettere ogni laboratorio in una propria sottorete, in modo che i docenti e gli assistenti di laboratorio possano trattarli in maniera indipendente. I computer dell' amministrazione ed i computer dei docenti sono altre due reti distinte, ed arriviamo quindi ad un totale di cinque reti. Per la rete dei docenti, ci conviene considerare il caso peggiore in cui tutti i docenti abbiamo due dispositivi: quindi consideriamo 200 host per il dimensionamento della rete.

Dobbiamo in pratica riempire la seguente tabella:

| Numero host        | IP rete           | Subnet  |
| ------------- |:-------------:| -----:|
| 20 |  |  |
| 20 |  |  |
| 20 |  |  |
| 10 |  |  |
| 200 |  |  |

## Indirizzo IP della rete
Dobbiamo decidere che indirizzo di partenza dobbiamo dare all'intera rete, considerando che poi tutte le reti saranno a partire da quella. Sicuramente useremo degli indirizzi IP privati, visto che i computer della scuola non dovranno essere singolarmente raggiungibili da internet, e quindi non necessitano di un indirizzo IP pubblico. Ma quale indirizzi usiamo?

Visto che siamo una scuola, possiamo metterci comodi e scegliere di usare gli indirizzi privati `10.0.0.0/8`, in modo da avere tutti gli indirizzi IP che ci servono.

A questo punto abbiamo davanti a noi due strade:
1. fare un indirizzamento "facile", in cui assegniamo a tutte le reti la stessa maschera
1. fare un indirizzamento "stretto", in cui assegniamo ad ogni rete la sua maschera minima.

Quale scegliere? Ovviamente... dipende. Se non ci sono particolari vincoli, può essere utile la prima scelta: più semplice e veloce, meno errori. Se invece vogliamo per qualche motivo risparmiare indirizzi IP, scegliamo sicuramente la seconda strada.

Di seguito vediamo entrambi i casi.

## Caso 1: stessa subnet mask per tutte le reti
Scegliamo per tutti la stessa subnet mask. In più, per essere ancora più comodi, scegliamo una maschera che sia un multiplo di 8, così tutti i conti ci vengono semplici.

Quale subnet scegliamo? Dovendone scegliere una per tutte, prendiamo in considerazione quella con il maggior numero di host, in questo caso quella per i docenti: 200 computer.

Si vede abbastanza facilmente che va bene una rete di classe C, cioé `/24`, che può contenere fino a 256 host. La nostra tabella può quindi essere riempita come segue.

| Numero host        | IP rete           | Subnet  |
| ------------- |:-------------:| -----:|
| 20 | 10.0.0.0 | /24 |
| 20 | 10.0.1.0 | /24 |
| 20 | 10.0.2.0 | /24 |
| 10 | 10.0.3.0 | /24 |
| 200 | 10.0.4.0 | /24 |


## Caso 2: subnet mask minima per ogni rete
In questo caso vogliamo invece calcolare per ogni rete la dimensione minima della subnet.

Il primo passo che ci conviene fare è ordinare le reti dalla più grande alla più piccola, come segue.

| Numero host   | IP rete       | Subnet|
| ------------- |:-------------:| -----:|
| 200 |  |  |
| 20  |  |  |
| 20  |  |  |
| 20  |  |  |
| 10  |  |  |

A questo punto calcoliamo il numero di bit che ci servono per il dimensionamento di ogni rete. Ricordiamoci che al numero di host va aggiunto un indirizzo per la rete e uno per il broadcast, quindi il calcolo è:

<p class="centered">
<strong>
numero IP = numero host + 2
</strong>
</p>

Per la prima rete dei docenti, devo assegnare 202 indirizzi. La potenza di due maggiore di 202 più vicina è 256, che corrisponde a 8 bit. Quindi la parte fissa della nostra rete sarà, come abbiamo già visto, `32 - 8 = 24 bit`, che corrisponde alla subnet mask.

| Numero host   | IP rete       | Subnet|
| ------------- |:-------------:| -----:|
| 200 | 10.0.0.0 | /24 |
| 20  |  |  |
| 20  |  |  |
| 20  |  |  |
| 10  |  |  |

Passiamo alla seconda rete. La prima cosa da fare è calcolare l'IP della rete. Come facciamo? Dobbiamo calcolare il primo indirizzo IP libero dopo la rete precedente. Siccome la rete dei docenti parte da 10.0.0.0 e ha 256 IP, il primo indirizzo IP disponibile è 10.0.1.0.

| Numero host   | IP rete       | Subnet|
| ------------- |:-------------:| -----:|
| 200 | 10.0.0.0 | /24 |
| 20  | 10.0.1.0 |  |
| 20  |  |  |
| 20  |  |  |
| 10  |  |  |

Per il calcolo della maschera, considerando che i laboratori hanno 20 computer, abbiamo bisogno di `20 + 2 = 22` IP. La potenza di due più vicina è 32, che corrisponde a 5 bit. La subnet è quindi `32 - 5 = 27 bits`.

Ricapitolando, per la seconda rete la situazione è la seguente.

| Numero host   | IP rete       | Subnet|
| ------------- |:-------------:| -----:|
| 200 | 10.0.0.0 | /24 |
| 20  | 10.0.1.0 | /27 |
| 20  |  |  |
| 20  |  |  |
| 10  |  |  |

Ora, per calcolare l'IP di partenza della rete successiva bisogna prestare un po' di attenzione. La rete che abbiamo appena calcolato parte da `10.0.1.0` e ha 32 IP. Quindi la rete successiva partirà da `10.0.1.32`. La maschera di rete è la stessa, avendo lo stesso numero di host all'interno.

| Numero host   | IP rete       | Subnet|
| ------------- |:-------------:| -----:|
| 200 | 10.0.0.0 | /24 |
| 20  | 10.0.1.0 | /27 |
| 20  | 10.0.1.32 | /27 |
| 20  |  |  |
| 10  |  |  |

Ripetendo il ragionamento anche per la quarta rete, arriviamo alla seguente situazione.

| Numero host   | IP rete       | Subnet|
| ------------- |:-------------:| -----:|
| 200 | 10.0.0.0 | /24 |
| 20  | 10.0.1.0 | /27 |
| 20  | 10.0.1.32 | /27 |
| 20  | 10.0.1.64 | /27 |
| 10  |  |  |

Infine, calcoliamo IP e subnet della rete amministrativa, l'ultima. Lascio a voi di ripetere i calcoli precedenti e verificare che la tabella completa è come segue.

| Numero host   | IP rete       | Subnet|
| ------------- |:-------------:| -----:|
| 200 | 10.0.0.0 | /24 |
| 20  | 10.0.1.0 | /27 |
| 20  | 10.0.1.32 | /27 |
| 20  | 10.0.1.64 | /27 |
| 10  | 10.0.1.96 | /28 |
