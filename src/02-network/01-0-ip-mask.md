# Indirizzi IP e maschere di sottorete
L'indirizzo IP (_Internet Protocol_) come detto è formato da 4 byte e viene rappresentato come segue:

<p class="centered xxl-font">
<strong>
172.16.254.1
</strong>
</p>

Ognuno dei numeri rappresenta un byte e può quindi assumere un valore da 0 a 255.

Un indirizzo IP può rappresentare in alternativa una delle seguenti cose:
- indirizzo IP che identifica una rete
- indirizzo IP che identifica un dispositivo appartenente ad una rete
- indirizzo IP di broadcast, per comunicare facilmente con tutti i dispositivi appartenenti ad una determinata rete.

Come già detto, ad un indirizzo IP è _sempre_ associata la subnet mask che indica la grandezza della rete a cui appartiene. Non può esistere un indirizzo IP senza subnet mask!

## Indirizzo di rete
Tutto parte con l'indirizzo che assegniamo ad una rete. Alcuni esempi di indirizzi di rete validi sono:
- 10.0.0.0
- 10.168.232.64
- 192.168.43.0
- 216.58.198.0

Attenzione: gli indirizzi di rete **non** possono essere assegnati a dispositivi, siano essi computer o router. Sono indirizzi che individuano la rete e non corrispondono a nessun oggetto fisico reale.

Quanti dispositivi può contenere una rete? Questo numero dipende dal secondo numero fondamentale a cui abbiamo accennato, ovvero la maschera di sottorete.

## Maschera di sottorete
Come facciamo a sapere quanti computer possono far parte di una rete? Mettendoci nei panni dei creatori di Internet, proviamo a ragionare su quale potrebbe essere un metodo comodo per raggiungere questo scopo.

Sappiamo che, da come è stato definito l'indirizzo IP, la grandezza massima teorica di una rete è 4 byte, quindi 32 bit (circa 4 miliardi di computer). Non è tecnicamente possibile avere reti IP più grandi.

> Per esattezza, esiste un altro standard IP che usa 16 byte per l'indirizzo e quindi può ospitare molti più computer. Questo standard è nato alla fine degli anni '90 e si chiama *IPv6*, è supportato ormai da tutti i sistemi operativi e dispositivi di rete, e viene regolarmente utilizzato anche se noi non ce ne accorgiamo. La sua ulteriore diffusione è legata, tra le altre cose, agli sviluppo del 5G e dell'Internet of Things. Vedremo cosa succederà! In questo capitolo noi ci occupiamo solo dello standard tradizionale, l'IPv4.

Per calcolare la dimensione minima di una rete bisogna prestare leggermente più attenzione. Nel caso limite, una rete è formata da minimo 2 computer (una rete di un singolo computer infatti... non è una rete :)) Ai due indirizzi assegnati ai computer dobbiamo aggiungere l'indirizzo IP della rete e quello di broadcast. Abbiamo quindi bisogno di 4 indirizzi IP per la rete più piccola possibile. Per identificare 4 indirizzi servono esattamente 2 bit.

Ora, attenzione: per convenzione la maschera di sottorete indica il numero di bit della parte _fissa_ del nostro indirizzo IP, ovvero quella parte iniziale che _non_ cambia. Una rete della massima grandezza _non_ avrà una parte fissa, e quindi la maschera di sottorete sarà esattamente 0. Se invece noi abbiamo una rete con due soli computer, avremo solo gli ultimi 2 bit variabili, e la nostra maschera di sottorete varrà 30.

In generale, la formula per calcolare la maschera di sottorete è:

<p class="centered">
<strong>
maschera di sottorete: 32 - numero di bit per la dimensione della rete
</strong>
</p>

Questo numero convenzionalmente viene messo subito dopo l'indirizzo IP, separato da uno slash (`/`); per questo motivo viene chiamata anche _slash notation_.

Facciamo alcuni esempi validi di indirizzi di rete con subnet mask:
- 10.0.0.0/8
- 10.168.232.64/20
- 192.168.43.0/24
- 216.58.198.0/30

### Un caso particolare
Prima di concludere, esaminiamo un caso particolare:
<p class="centered large-font">
<strong>
0.0.0.0/0
</strong>
</p>

A cosa corrisponde questa rete? Vediamo di analizzarla nel dettaglio:
- 0.0.0.0 corrisponde al primo indirizzo IP disponibile in assoluto
- /0 significa che non ci sono bit fissi della rete, e quindi è tutta assegnabile a dei dispositivi.
Detto in altre parole, la rete 0.0.0.0/0 include _tutti gli indirizzi IP possibili_ e corrisponde quindi a _tutto Internet_, sia esso locale o globale!
