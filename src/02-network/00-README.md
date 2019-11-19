# Network layer

Finora abbiamo visto come collegare fra di loro un numero relativamente piccolo di computer, ovvero quelli collegabili ad un singolo switch. Per connettere ancora più computer, potremmo mettere degli switch a cascata, collegati tra di loro: si può fare, ma al crescere dei computer e degli switch, si cominciano ad avere una serie di problemi di inefficienza e sicurezza che devono essere risolti in altro modo. Entrano ora in gioco i concetti di rete e sottorete, in altre parole il "network layer".

## La nascita di Internet
Per far crescere il numero di computer connessi tra loro, dobbiamo dividerli in dei gruppi separati che comunicano tra di loro in modo controllato.

La soluzione più utilizzata oggi è quella di assegnare un altro indirizzo ad ogni macchina, chiamato _IP Address_, formato da soli 4 byte, che lo identifica univocamente all'interno di una sottorete. A questo indirizzo viene sempre associato un altro numero, chiamato maschera di sottorete (_subnet mask_), anch'esso di 4 byte, che definisce la grandezza della sottorete in cui ci troviamo. Le reti sono connesse tra di loro da delle macchine dedicate, tipicamente dei _router_ (instradatori). Questo sistema venne inventato agli inizi degli anni '70 e venne chiamato **Internet**, ed è proprio quello che utilizziamo oggi quotidianamente.

<p class="img-container">
<img class="right_side w35p" title="vint-bob" alt="vint-bob" src="assets/vint-bob.jpg">

I padri fondatori di Internet sono considerati [Vint Cerf](https://it.wikipedia.org/wiki/Vint_Cerf) e [Bob Kahn](https://it.wikipedia.org/wiki/Robert_Kahn) che nel **1972** circa, mentre lavoravano presso il DARPA (Agenzia per i Progetti di ricerca avanzata per la Difesa), in America, hanno messo le basi per questa tecnologia ed i relativi protocolli.
</p>

> Internet non è l'unico sistema che è nato negli anni 70, ma è quello che nel tempo ha preso il sopravvento rispetto a tutti gli altri.

Internet si appoggia sul livello 2 della pila ISO/OSI (che _non_ sostituisce!), e si colloca immediatamente sopra, quindi nel livello 3, che è appunto il livello di rete (network layer).

Una nota sull'uso della parola "Internet": tecnicamente, una qualsiasi rete di computer connessi tra di loro con indirizzo IP è una rete Internet. Tuttavia, nell'uso quotidiano usiamo questa parola per indicare la rete _globale_ di computer. In questo testo si specificherà "rete Internet globale" quando necessario per evitare fraintendimenti.
