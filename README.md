Metasploit è un framework **open-source** usato per il penetration testing e lo **sviluppo** di **exploit**. **Fornisce** una vasta gamma di **exploit** creati dalla comunità e numerosi **vettori** di **attacco** che si possono utilizzare **contro diversi sistemi** e **tecnologie**. Inoltre, può essere utilizzato per creare ed automatizzare i propri exploit.

Questo tool può essere utilizzato con diverse interfacce grafiche:

- Interfaccia Web
- Riga di comando
- Una console: MSFConsole

# Come funziona?

Una volta avviato da console, vedremo che saranno **disponibili** migliaia di **exploit** e **peyload**. **Insieme** sono racchiusi in un **modulo** che noi useremo come vettore di attacco in relazione alla vulnerabilità trovata.

# Comandi utili

- **setg** imposta lo stesso valore per ogni payload che utilizzeremo fino a quando ma macchina è accesa
- **unsetg** rimuove il valore fisso
- **exploit o run** fa partire l’exploit
- **host** visualizza info host
- **services** visualizza info services
- **loot** viene utilizzato per gestire e visualizzare i dati raccolti durante una sessione di penetrazione. informazioni come credenziali file di configurazione, chiavi private, dump di memoria e altro ancora.
- **creds** stampa a schermo tutte le credenziali che siamo riusciti a trovare
- **analyze** analizza tutto cio’ che abbiamo trovato sull’ host target e mostra quali exploit possono essere sfruttate.
- **vulns** mostra le vulnerabilita’ trovate
- **`exploit -z`** eseguirà l'exploit e metterà in background la sessione non appena verrà aperto.
- **check** controllerà se il sistema di destinazione è vulnerabile senza sfruttarlo.
- **sessions** visualizzare le sessioni esistenti.
- **sessions -i NUMERO_SESSIONE** per interagire con una sessione specifica
- **search portscan** scansione porte aperte sul sistema e sulla rete di destinazione
- **scanner/discovery/udp_sweep** modulo ti consentirà di identificare rapidamente i servizi che girano su UDP e info su DNS e NetBios
- **`smb_enumshares`** e
- **`smb_version`** fingerprint **OS**

### Database comand

- **`systemctl start postgresql`** avvia il database PostgreSQL
- **msfdb init** inizializza il database (da eseguire dopo il comando sopra)
- **`db_status`** controlla lo stato del database
- **workspace** elenca gli spazi di lavoro disponibili
- **workspace -h** help manual
- **workspace -a NOME_WORKSPACE** crea un nuovo spazio di lavoro
- **workspace -d NOME_WORKSPACE** elimina spazio lavoto
- **workspace NOME_WORKSPACE** ti sposti in quell’area di lavoro
- **db_nmap -OPZIONI -IP_TARGET** scansione del database con nmap (ricorda che memorizza le info)

### Hosts (sei all’interno del database e memorizza tutto)

- **hosts** info su hosts
- **hosts -h** apre manuale
- **hosts -R** aggiunger parametro a RHOSTS

### Services

- **services** info su service
- **seriveces -h** apre manuale
- **services -S** **SERVIZIO** consentirà di cercare servizi specifici nell'ambiente. ****

# Come troviamo il modulo giusto?

- **search** <termine di ricerca> da riga di comando possiamo determinare i valori di ricerca

# Esempio

**1)** Con Nessus troviamo un vulnerabilità **smb**. Cerchiamo, con **serach**,in Metasploit i moduli per effettuare un attacco all’ smb

![Untitled](https://github.com/user-attachments/assets/cd8f1d75-aa38-4397-8cb9-76957e968001)

2) trovato il modulo possiamo copiarlo ed incollarlo su riga di comando per avviarlo

![Untitled](https://github.com/user-attachments/assets/debf4ec1-3b43-464d-8649-0803f0af75c4)

3)Ora dovremo controllare le opzioni del modulo con il comando show options che ci permetterà di capire quali dati modificare. Notiamo che alcuni sono obbligatori. 

![Untitled](https://github.com/user-attachments/assets/c5ef24a1-698a-4014-a9e6-b2912858f7ce)

**4)** in questo caso modifichiamo i parametri **RHOST** ed **RPORT** 

- **set RHOSTS 192.168.1.150**
- **set RPORT 80**

5) a questo punto dovremo caricare il payload del relativo modulo con il comando **show payloads**

![Untitled](https://github.com/user-attachments/assets/c43a410c-5bc5-44c1-8b66-581f6ad08e23)

6)impostiamo il payload scelto con il comando 

- **set payload NOME_PAYLOAD**

7) Possiamo visualizzare le opzioni del payload tramite il comando show options
 
![Untitled](https://github.com/user-attachments/assets/fbf7f5c3-26fd-4cc4-a047-96a803263da8)

8) E modificarle con **set PARAMETRO_PAYLOAD** in questo esempio modificheremo LHOST. Notiamo  che per ogni parametro c’è una descrizione.  In questo caso, LHOST ed LPORT sono rispettivamente l’indirizzo IP e la PORTA sulla macchina locale, dove vogliamo che un determinato servizio resti in ascolto

- **set LHOST 127.0.0.1**

9)Dopo aver scelto exploit e payload ed aver configurato le opzioni per entrambi, **bisogna lanciare l’attacco** con il comando:

- **exploit**

  





