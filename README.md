Il modulo è composto da exploit e payload. **L’exploit** è come se fosse un piede di porco, ovvero un **modo per entrare**, mentre il **payload** è come se fosse il contenuto di una siringa, ci dice che **tipo** di **attacco** stiamo facendo

1. **Avvio** del **servizio** MSFConsole: **msfconsole**
2. **Ricerca dell’exploit**:  con il comando **search** seguito dal **nome**, **sistema operativo**, **servizio** da **attaccare** o **CVE** della vulnerabilità e poi utilizzarlo con **use, numero o path**
3. **Controllo dei parametri necessari per lanciare l’exploit: show options,** i parametri con **YES** sono necessari per avviare il modulo
4. **RHOST**: IP Vittima
5. **RPORT**: porta vulnerabile
6. **SSL/TLS:** vanno messi su yes quando l’attacco viene effettuare su HTTPS, porta 443
7. **Ricerca e selezione del payload: show payloads** ci mostra i payload compatibili con quell’exploit, una volta trovato ciò che fa al caso nostro lo impostiamo con **set payload** seguito dal **path** del payload o dal **numero**
8. **Controllo dei parametri necessari per utilizzare il payload: show options** 
9. **LHOST**: inseriamo il nostro IP
10. **Exploit Target**: alcuni payload hanno piu di un sistema target, selezionare quello che ci interessa tra windows/unix/android. di solito è automatico 


1. **Esecuzione dell’attacco: run** o **exploit**
2. **Test:** con i comandi **ifconfig** o **whoami**

# Differenza dey payload BIND e REVERSE

- **bind:** in questa modalità si **inietta** un **processo** sulla **macchina obiettivo**. Questo processo si metterà in **ascolto** su una determinata **porta**, attendendo connessioni dall’esterno. Nella modalità bind_tcp il **servizio** di **shell** è **attivo** sulla **macchina attaccante** e la **connessione avviene dalla macchina dell’attaccante alla macchina target.**
- **reverse**: in questa modalità si inietta un **processo** sulla macchina obiettivo, che questa volta **effettuerà dalla macchina target** **una connessione verso la macchina dell’attaccante** mettendo a disposizione una shell. **La differenza con il bind_tcp è che nel reverse_tcp è la macchina target che inizia la connessione verso la macchina dell’attaccante.**

# Qual’è la differenza?

Per bipassare i firewall statici si utilizza la reverse in quanto permette la fuoriuscita di dati dall’interno verso l’esterno. di conseguenza con la reverse abbiamo piu probabilità che l’attacco funzioni.

# Differenza di moduli tra exploit ed auxiliary

**auxiliary** è un modulo che non funge da attacco ma piu da **OS fingerprintig**, in questo caso da scanner.

Gli **auxiliary non sono composti da payload**
