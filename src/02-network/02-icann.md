# Assegnazione degli indirizzi di rete
Finora abbiamo parlato di reti ed indirizzi IP, ma la domanda sorge spontanea: quali indirizzi posso utilizzare io per la mia rete, e quali no? Come faccio a saperlo?

La risposta è ovviamente...dipende. Nell'ipotesi in cui stessimo gestendo una rete completamente indipendente dal resto del mondo, potremmo scegliere gli indirizzi di rete che preferiamo, nessuno verrà a lamentarsi con noi, perché non diamo fastidio a nessuno.  

<p class="img-container">
<img class="right_side w10" title="ICANN" alt="ICANN" src="assets/icann.png">

Ma se vogliamo connettere la nostra rete ad una rete più grande, magari all'Internet globale, c'è chiaramente bisogno di un organizzazione super partes che organizzi le cose. Questa organizzazione si chiama [ICANN](https://www.icann.org/) (Internet Corporation for Assigned Names and Numbers) che, come dice il nome, si occupa proprio di assegnare i nomi ed in numeri di Internet in maniera da non creare conflitti.
</p>

ICANN attualmente funziona nel seguente modo:
- assegna degli indirizzi pubblici agli Internet Service Provider (es. TIM, Vodafone, Fastweb, Linkem, Civitanet, Aruba, etc.) che ne fanno richiesta
- riserva alcuni indirizzi per utilizzi speciali, ad esempio per le reti locali private

> A volte può capitare di sentir parlare di [IANA] (https://www.iana.org/)(Internet Assigned Numbers Authority). Non è in contraddizione con quanto detto prima: IANA è una emanazione dell'ICANN, con lo specifico compito di gestire gli indirizzi IP.

## Indirizzi di reti locali private
ICANN riserva i seguenti indirizzi da utilizzare per creare delle reti private all'interno della propria casa o della propria azienda:

- **10.0.0.0/8**, che va quindi da 10.0.0.0 a 10.255.255.255, con una maschera di sottorete di default di 8 bit (classe A)
- **172.16.0.0/12**, che va quindi da 172.16.0.0 a 172.31.255.255, con una maschera di sottorete di default di 16 bit (classe B)
- **192.168.0.0/16**, che va quindi da 192.168.0.0 a 192.168.255.255, con una maschera di sottorete di default di 24 bit (classe C)

Chiunque può utilizzare questi indirizzi senza dover chiedere il permesso a qualcuno. Fate attenzione però: questi indirizzi **non** possono far parte della rete internet globale, ma devono connettersi tramite un router che da un lato avrà un indirizzo locale, e dall'altro un indirizzo globale fornito da un ISP.
