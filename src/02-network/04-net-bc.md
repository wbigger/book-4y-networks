# Calcolo degli indirizzi di rete e broadcast
Quando abbiamo un host con un certo indirizzo IP ed una subnet mask, un'operazione che dobbiamo frequentemente fare è sapere l'indirizzo della rete alla quale appartiene ed il relativo indirizzo di broadcast.

In questa sezione vedremo come fare.

## Classful
Nel caso di indirizzamento classful, è facile calcolare l'indirizzo della rete e di broadcast.

Ad esempio ipotizziamo di avere un host con il seguente IP e maschera:
<p class="centered">
<strong>
192.168.7.55/24
</strong>
</p>

È un indirizzo di classe C, quindi l'indirizzo di rete è il primo della classe e il broadcast l'ultimo.

| IP/subnet   | IP rete       | IP broadcast|
| ------------- |:-------------:| -----:|
| 192.168.7.55/24 | 192.168.7.0 | 192.168.7.255 |


Analogamente per la classe B e la classe A si ottengono risultati analoghi.
Ipotizziamo di avere gli host con gli IP nella prima colonna, nelle altre due ci sono i relativi indirizzi di rete e broadcast.

| IP/subnet   | IP rete       | IP broadcast|
| ------------- |:-------------:| -----:|
| 172.16.4.8/16 | 172.16.0.0 | 172.16.255.255 |
| 10.12.0.44/8 | 10.0.0.0 | 10.255.255.255 |

## Classless

Le cose diventano un po' più complesse quando abbiamo degli indirizzi classless: dobbiamo far ricorso ad un po' di matematica.

Ipotizziamo lo stesso indirizzo di prima, ma con una diversa maschera di sottorete:

<p class="centered">
<strong>
192.168.7.55/28
</strong>
</p>

Per prima cosa dobbiamo convertire l'indirizzo IP dell'host in binario.

| Decimale   |  | Binario       |
| ------------- |:-------------:|:-------------:|
| 192 | --> |11000000 |
| 168 | --> | 10101000 |
| 7 | --> | 00000111 |
| 55 | --> | 00110111 |

Che ci porta quindi ad avere il seguente risultato:

| IP   |  | Binario       |
| ------------- |:-------------:|:-------------:|
| 192.168.7.55 | --> |11000000 10101000 00000111 00110111 |

Calcoliamo ora anche la maschera di sottorete in binario. È sufficiente mettere tanti 1 quanto il valore della maschera, e aggiungere 0 fino ad arrivare a 32.

| Subnet   |  | Binario       |
| ------------- |:-------------:|:-------------:|
| /28 | --> |11111111 11111111 11111111 11110000 |


Ora siamo pronti a calcolare indirizzo IP della rete e broadcast.

### Indirizzo di rete

Per l'indirizzo di rete, dobbiamo fare l'operazione logica `AND` tra l'indirizzo IP.

La tabella di verità per l'operatore logico `AND` è il seguente:

| A | B | A and B |
| ------------- |:-------------:|:-------------:|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

Quindi, abbiamo un valore 1 in uscita se e solo se entrambi i valori in ingresso sono 1.

Effettuiamo ora l'operazione.

|  |  |
| ----------------------------------- | --- |
| 11000000 10101000 00000111 00110111 | AND |
| 11111111 11111111 11111111 11110000 |  =  |
| ___________________________________ |     |
| 11000000 10101000 00000111 00110000 |     |

Bene, ci siamo quasi! Ora dobbiamo riconvertire da binario a decimale l'indirizzo appena calcolato, ed otteniamo il seguente risultato:

<p class="centered">
<strong>
IP di rete: 192.168.7.48
</strong>
</p>

### Broadcast
Ci manca di calcolare l'indirizzo di broadcast. Abbiamo diverse opzioni, ne propongo qui due.

#### Metodo empirico
Come prima possibilità, posso calcolare il numero di IP contenuti nella rete e sommare tale numero all'indirizzo IP della rete.

Nel nostro caso, abbiamo una maschera /28, quindi il numero di IP disponibili nella rete è:

<p class="centered">
2 ^ (32-28) = 2 ^ 4 = 16
</p>

Quindi sommando l'indirizzo di rete al numero di host e sottraendo uno (in quanto devo contare anche l'IP di rete di partenza):

<p class="centered">
192.168.7.48 + 16 - 1 = 192.168.7.63
</p>

Da cui l'indirizzo di broadcast:
<p class="centered">
<strong>
IP di broadcast: 192.168.7.63
</strong>
</p>

#### Metodo numerico
Posso effettuare anche un operazione logica per il calcolo del broadcast, simile a quello che abbiamo fatto prima per l'indirizzo di rete. Dobbiamo però usare l'operatore `OR` ed al posto della maschera di sottorete, il suo valore _negato_. Vediamo nel dettaglio.

L'operatore logico `OR` ha la seguente tabella di verità.

| A | B | A or B |
| ------------- |:-------------:|:-------------:|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

Con l'operatore `OR`, abbiamo un valore 1 in uscita se uno dei due valori in ingresso è pari a 1.

Inoltre, come detto, nella nostra operazione dobbiamo usare il valore _negato_ della maschera di rete, ovvero dobbiamo invertire tutti gli 0 con 1 e viceversa. La negazione si chiama anche operatore `NOT`.

| Subnet mask  | NOT Subnet mask |
| ------------- | :-------------:|
| 11111111 11111111 11111111 11110000 |00000000 00000000 00000000 00001111 |


Effettuiamo ora l'operazione `OR` tra l'indirizzo IP di partenza ed il valore negato della maschera di sottorete.

|  |  |
| ----------------------------------- | --- |
| 11000000 10101000 00000111 00110111 | OR |
| 00000000 00000000 00000000 00001111 |  =  |
| ___________________________________ |     |
| 11000000 10101000 00000111 00111111 |     |

Infine convertiamo da binario a decimale e otteniamo

<p class="centered">
<strong>
IP di broadcast: 192.168.7.63
</strong>
</p>

Che ovviamente è lo stesso indirizzo calcolato in precedenza con l'altro metodo. Ognuno può usare il metodo che preferisce, in base alle proprie attitudini o esperienze.

## Esercizi di preparazione al compito
Per prepararsi al compito, Riempire la seguente tabella.

| IP/subnet   | IP rete       | IP broadcast|
| ------------- |:-------------:| -----:|
| 192.168.0.122/24 |  |  |
| 192.168.0.122/26 |  |  |
| 192.168.0.122/28 |  |  |
| 192.168.0.122/23 |  |  |
| 192.168.0.122/20 |  |  |
| 7.15.22.90/24 |  |  |
| 7.15.22.90/26 |  |  |
| 7.15.22.90/28 |  |  |
| 7.15.22.90/23 |  |  |
| 7.15.22.90/20 |  |  |