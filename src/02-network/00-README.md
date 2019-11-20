# Network layer

Finora abbiamo visto come mettere in comunicazione fra di loro un numero relativamente piccolo di computer, ovvero quelli che possono essere connessi ad un singolo switch. Per connettere ancora più computer, potremmo mettere degli switch a cascata, collegati tra di loro: si può fare, ma al crescere dei computer e degli switch, si cominciano ad avere una serie di problemi di inefficienza e sicurezza che devono essere risolti.

Per creare reti di computer di grandi dimensini, la pila ISO/OSI introduce il concetti di _rete_ e _sottorete_, e passiamo quindi al terzo livello, il "network layer".

## La nascita di Internet
La soluzione più utilizzata oggi è quella di assegnare un altro indirizzo ad ogni macchina, chiamato **IP Address**, formato da 4 byte, che lo identifica univocamente all'_interno di una sottorete_. All'indirizzo IP deve sempre essere associato un altro numero, chiamato maschera di sottorete (**subnet mask**), anch'esso di 4 byte, che definisce la grandezza della sottorete in cui ci troviamo. Le reti sono connesse tra di loro da dei dispositivi di rete dedicate, tipicamente dei **router** (instradatori). Questo sistema venne inventato agli inizi degli anni '70 e venne chiamato **Internet**, ed è proprio quello che utilizziamo oggi quotidianamente.

<p class="img-container">
<img class="right_side w35p" title="vint-bob" alt="vint-bob" src="assets/vint-bob.jpg">

> I padri fondatori di Internet sono [Vint Cerf](https://it.wikipedia.org/wiki/Vint_Cerf) e [Bob Kahn](https://it.wikipedia.org/wiki/Robert_Kahn) che nel **1972** circa, mentre lavoravano presso il DARPA (Agenzia per i Progetti di ricerca avanzata per la Difesa), in America, hanno messo le basi per questa tecnologia ed i relativi protocolli.
</p>

> Internet non è l'unico sistema che è nato negli anni 70, ma è quello che nel tempo ha preso il sopravvento rispetto a tutti gli altri.

Una nota sull'uso della parola "Internet": tecnicamente, una qualsiasi rete di computer connessi tra di loro con indirizzi IP è una rete Internet. Tuttavia, nell'uso quotidiano usiamo questa parola per indicare la rete _globale_ di computer. In questo testo si specificherà "rete Internet globale" quando necessario per evitare fraintendimenti.
