### Assegnazione degli indirizzi di rete
Da dove viene questo numero? Quali numeri possiamo usare e quali no?

La risposta è ovviamente...dipende. Se stiamo gestendo una rete completamente indipendente dal resto del mondo, possiamo scegliere gli indirizzi di rete che preferiamo, e nessuno verrà a lamentarsi con noi, perché non diamo fastidio a nessuno. Ma se vogliamo connettere la nostra rete ad una rete più grande, magari all'Internet globale.

<p class="img-container">
<img class="right_side w10" title="ICANN" alt="ICANN" src="assets/icann.png">

C'è chiaramente bisogno di un organizzazione super partes che organizzasse le cose. Questa organizzazione si chiama [ICANN](https://www.icann.org/) (Internet Corporation for Assigned Names and Numbers) che, come dice il nome, si occupa proprio di assegnare i nomi ed in numeri di Internet in maniera da non creare conflitti.
</p>

ICANN attualmente funziona nel seguente modo:
- assegna degli indirizzi pubblici agli Internet Service Provider (es. TIM, Vodafone, Fastweb, Linkem, Civitanet, Aruba, etc.) che ne fanno richiesta
- riserva alcuni indirizzi per utilizzi speciali, ad esempio per delle reti locali private

#### Indirizzi di reti locali private
ICANN riserva i seguenti indirizzi da utilizzare per creare delle reti private all'interno della propria casa o della propria azienda:

- 10.0.0.0/8, che va quindi da 10.0.0.0 a 10.255.255.255, con una maschera di sottorete di default di 8 bit (classe A)
- 172.16.0.0/12, che va quindi da 172.16.0.0 a 172.31.255.255, con una maschera di sottorete di default di 16 bit (classe B)
- 192.168.0.0/16, che va quindi da 192.168.0.0 to 192.168.255.255, con una maschera di sottorete di default di 24 bit (classe C)

Chiunque può utilizzare questi indirizzi senza dover chiedere il permesso a qualcuno. Fate attenzione però: questi indirizzi **non** possono far parte della rete internet globale, ma devono connttersi tramite un router che da un lato avrà un indirizzo locale, e dall'altro un indirizzo globale fornito da un ISP.



Dimensionamento di una rete... (es. ho 10 pc, quanto deve essere grande la sottorete?)


Conversione da notazione slash ad ottetti...

Classi di indirizzi IP...
