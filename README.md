# **CHE COS’è**

E’ un **port scanner,** che ci permette di verificare, in un range di porte, se esse siano aperte o chiuse, quindi se permettono al comunicazione con lo scambio di pacchetti **TCP o UDT.**

Con l’apertura di una porta possiamo per esempio metterci in ascolto su quella porta e comunicare per messaggi.

# Reverse Shell

Ci sono *molti* modi per eseguire una shell, quindi inizieremo esaminando i listener.

La **sintassi** per avviare un listener **netcat** utilizzando Linux è la seguente:

**`nc -lvnp <port-number>`**

- **-l** viene utilizzato per dire a netcat che questo sarà un **ascoltatore**
- **-v** viene utilizzato per **richiedere** un **output dettagliato**
- **-n** dice a netcat di non **risolvere i nomi host o di non usare DNS.**
- **-p** indica che seguirà la specifica della **porta**.

Realisticamente **potresti utilizzare qualsiasi porta** tu voglia, **purché** n**on ci sia già un servizio che la utilizzi**. Tieni presente che se scegli di utilizzare una **porta inferiore a 1024, dovrai utilizzarla `sudo`**quando avvii il tuo listener. Detto questo, è spesso una buona idea utilizzare un numero di porta noto (80, 443 o 53 sono buone scelte) poiché è più probabile che superi le regole del firewall in uscita sulla destinazione.

Un esempio pratico di ciò sarebbe:

**`sudo nc -lvnp 443`**

Possiamo quindi ricollegarci a questo con un numero qualsiasi di payload, a seconda dell'ambiente del bersaglio.

# Bind Shell

Se stiamo cercando di ottenere una shell di bind su un target, allora possiamo supporre che ci sia già un listener che ci aspetta su una porta scelta del target: tutto ciò che dobbiamo fare è connetterci ad esso. La sintassi per questo è relativamente semplice:

**`nc <target-ip> <chosen-port>`**

Qui utilizziamo netcat per creare una connessione in uscita verso la destinazione sulla porta scelta.
