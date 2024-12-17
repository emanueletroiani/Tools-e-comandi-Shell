# SHELL  LINUX COMANDI

### **SPOSTARS TRA LE CARTELLE**

- **cd** torniamo all directory sorgente
**cd -** andiamo ella directory precedente
**cd ..** torniamo indietro di una directory
- **cd ../..** torniamo indietro di 2 directory
- **cd ../directory** torniamo indietro e apriamo un’altra directory
- **~/** evitiamo di scrivere /home/kali/etc fino alla directory principale

### MUOVERE,COPIARE, ELIMINARE FILE E DIRECTORY

- **mv NOME_FILE /PERCORSO_DESTINAZIONE** Sposta il file o directory
- **mv NOME_FILE NUOVO_NOME_FILE** rinomina il file o directory
- **cp NOME_FILE /PERCOSO** copia il file nella directory del percorso
- **cp -r NOME_DIRECTORY /PERCOSO** copia una directory
- **rm** cancella file
- **rm -r DIRECTORY** elimina la directory

### CARATTERI JOLLY * ?

- **PAROLA*** seleziona tutti i caratteri prima dell’alsterisco ed ignora quelli dopo
    - **ls -l mi*** esempio che fa vedere solo le cartelle contenenti i caratteri mi e gli vanno bene tutti i caratteri dopo *
- ls -l *.txt esempio che fa vedere solo i caratteri contenenti .txt, gli vanno bene tutti i caratteri prima del *
- ls -l * prova * trova tutti i file contenenti prova, non gli interessa di cercare caratteri prima e dopo l’asterisco
- ls -l ci fa vedere tutti i contenuti delle cartelle nella directory perchè non abbiamo impostato nessun carattere
- **?** sostituisce un qualsiasi carattere da cercare
- ls -l prova??.* indico di visualizzare solo i file contenente la parola prova,2 caratteri extra e un’estenzione qualsiasi

### **CREAZIONE CARTELLE**

- **mkdir** crea cartella
- **mkdir “nome cartella”** crea cartella con uno spazio nel nome
- **mkdir -p DIRECTORY/DIRECTORY2** crea una cartella non esistente dentro una cartella non esistente
    - L'opzione `-p` consente di creare una directory insieme a tutte le sue directory padre necessarie, se non esistono già.

### **INFO CARTELLE E FILE**

- **ls** visualizza cartelle e file di una directory
- **ls -l** visualizza cartelle e file di una directory con piu info
- **ls -lt**  di ordinare i file e le directory per data e ora di modifica
- **ls -lh** visualizza dimensioni file
- **ls -a** Mostra tutti i file, inclusi i file nascosti
- **ls -A** Mostra tutti i file nascosti, ma esclude le directory
- **df** (disk free) viene utilizzato per visualizzare lo spazio libero e utilizzato su filesystem
    - `-h` (human-readable) formatta l'output in un formato leggibile per gli esseri umani
    - **`a`**: Mostra tutti i filesystem, incluso quelli con 0 blocchi.
    - **`i`**: Mostra informazioni sugli inode invece che sullo spazio.
    - **`T`**: Mostra il tipo di filesystem.
    - **`t`**: Mostra solo i filesystem del tipo specificato.
    - **`x`**: Esclude i filesystem del tipo specificato.
- **df -h /PERCORSO** visualizza info filesystem solo del percorso
- **du** disk usage
    - stesse opzioni di df

### **CREAZIONE FILE**

- **touch** utilizzato per creare file vuoti.
    - **touch nomefile.txt**
- **echo**  creare un file e scrivere del contenuto al suo interno
    - **echo "Questo è il contenuto del file" > nomefile.txt**
- **nano nomefile.txt** file con editor di testo nano
- **vi nomefile.txt** file con editor di testo VIM
    - Per salvare e uscire, premi `Esc`, poi digita `:wq` e premi `Invio`.
- **dd**
    - **dd if=/dev/zero of=nuovoFile.txt bs=1M count=1**
        - crea un file chiamato `nuovoFile.txt` di 1 MB riempito con zeri.

### PERMESSI FILE E CARTELLE rwx e CREAZIONE UTENTI

- **id** info utente corrente
- **w** dettagli dell’utente appena loggato
- **useradd -m NOME** crea user
    - **--allow-bad-names** se non prende il nome utente
- **userdel NOME** cancella utente
- **groupadd NOME** crea un nuovo gruppo
- **usermod -aG NOME_GRUPPO NOME_USER** assegniamo un user ad un gruppo
- **chown NOME_USER NOME_GRUPPO NOME_FILE** cambia il proprietario e il gruppo di un file
- **chown NOME_GRUPPO NOME_FILE** cambiamo il gruppo di appartenenza del file
- **sudo passwd NOME_USER** cambiamo password di un utente
- **useradd -m USERNAME -G GROUPNAME** per creare ed inserire un nome utente in un gruppo

### **VISUALIZZARE I FILE NELLA SHELL**

- **cat FILE** fa visualizzare tutto il contenuto all'interno della shell
- **cat FILE1 FILE2 FILE3** permette la visualizzazione di 3 file o piu
- **head** restituisce le prime righe di un file di testo. Di default, mostra le prime 10 righe
- **head -n FILE.TXT** mostrerà le prime 20 righe del file file.txt
- **tail** restituisce le ultime righe di un file di testo. Di default, mostra le ultime 10 righe
- **tail -n 15 file.txt** mostrerà le ultime 15 righe del file file.txt.
- **less** permette di visualizzare il file direttamente nella console:
    - **q** per uscire.
    - **/** per ricercare parole.
    - **space** per andare avanti di pagina

### **CALENDARIO**

- **cal** calendario di questo anno
- **cal ANNO** per vedere il calendario di uno specifico anno

### Info sulla macchina

- **uname -a**
- **sysinfo**
- **route**
- **dmesg** vedere lo stato del sistema

### Word counter

- **wc -m NOME_FILE** otteniamo al grandezza in byte de file

### **SCORCIATOIE**

- **history** visualizza tutti i comandi digitati
    - **!numero** comando ripete il comando
- **alias nome_scorciatoia nano /home/kali/windows/castle etc etc** permette di creare una scorciatoia di un comando
    - **~/.gshrc** serve per visualizzare la lista degli alias ed inserisci

### **ESEGUIRE UN PROGRAMMA**

- **programma**
- **programma&** e commerciale alla fine per avviarlo in background
- **./FILE** aprire un file come un programma

### **VEDERE CONTENUTO DI TUTTE LE DIRECTORY**

- **ls -R** fa visualizzare tutte le cartelle e sotto cartelle
- **tree** visualizza come albero genealogico

### **CERCARE QUALCOSA ALL'INTERNO DELLE DIRECTORY**

- **locate FILE** cerca la posizione del file in tutta kali
- **find** funziona con la seguente stringa:
    - **find /percorso** **-opzioni criteri**
- **find /percorso -type f -iname ‘*parola*’**
    - **`find /percorso`**: Indica il percorso di partenza per la ricerca.
    - **`-type f`**: Specifica che il comando deve cercare solo file (non directory).
    - **`-iname '*parola*'`**: Cerca file i cui nomi contengono la parola "parola", **ignorando** la distinzione tra **maiuscole** e **minuscole**. è importante racchiudere il pattern tra apici singoli
- **find /percorso -type f -iname ‘*parola*’** **-print**
    - per stampare il percorso completo dei file trovati
- **find /percorso -type f -size +1M**
    - **-size +1M** Cerca file con una dimensione maggiore di 1 megabyte. Il prefisso `+` indica che la dimensione deve essere superiore a quella specificata. La `M` sta per megabyte.
        - **`c`**: byte (default)
        - **`k`**: kilobyte (1024 byte)
        - **`M`**: megabyte (1024 kilobyte)
        - **`G`**: gigabyte (1024 megabyte)
- **find . -type d -name nome_directory** trova il percorso della directory
    - **`-type d`**: Specifica che il comando deve cercare solo directory
    - Cerca directory con un nome esattamente **uguale** a `nome_directory`

### **IL PIPE**

- **|** utilizzato per collegare l'output di un comando all'input di un altro comandoù
- **head -n 20 FILE.txt | tail -n +10** 
legge le prime 20 righe di `FILE.txt` e poi, da queste 20 righe, stampa dalla riga 10 alla riga 20.
    - head -n 20 FILE.txt
        - `head` è un comando che stampa le prime `n` righe di un file.
        - `-n 20` specifica che desideri le prime 20 righe del file `FILE.txt`.
    - `|` è un operatore che passa l'output del comando precedente come input al comando successivo.
    - tail -n +10
        - `tail` è un comando che stampa le ultime `n` righe di un file o dell'input ricevuto tramite la pipe.
        - `-n +10` specifica che desideri iniziare dalla riga 10 e continuare fino alla fine dell'input ricevuto (in questo caso, l'output delle prime 20 righe fornito da `head`).

### **VISUALIZZARE I PROCESSI**

- **ps** crea lista di tutti i processi associati all' utente corrente nella shell corrente.
- **ps -e**  è possibile visualizzare una lista di tutti i processi di tutti gli utenti.
- **ps -F** è possibile visualizzare informazioni più dettagliate, inclusi i dettagli dell'ambiente, dei percorsi dei comandi, dei tempi di avvio, ecc.
- **ps -l** alcuni dettagli
- **ps PID** permette di visualizzare informazione dettagliate su numero del processo inserito
- **ps -s** permette di vedere lo stato dei processi PENDING,BLOCKED,IGNORED,CAUGHT
- **pstree** crea un albero genealogico con tutti i processi avviati dall'utente
- **pstree -p [PID]** permette di vedere la strutta genealogica del processo indicando il numero di PID
- **pstree -s PID** permette di vedere tutti i processi associati a quel PID sin dall'origine
- **pstree -p $$** viene utilizzato per visualizzare l'albero dei processi a partire dal processo corrente, ‘$$’ è un valore che sostituisce il processo corrente

### **KILLARE UN PROCESSI**

- **kill PID** permette di arrestare il processo corrispondente al PID inserito
- **kill -s KILL [PID]** o con la sua forma abbreviata 'kill -9 PID' permette di arrestare un processo immediatamente senza che esse avvia la procedura di uscita, può portare alla perdita di dati
- **kill -s TERM [PID]** serve per terminare nella maniera corretta un processo, è CONSIGLIATO USARE QUESTO

### **COMANDI ‘<’  ‘>’ ‘2>’  ‘>>’**

Il reindirizzamento di input `< FILE_INPUT`permette di fornire facilmente l'input ai comandi dai file. È particolarmente utile negli script e quando si vuole rendere il codice più leggibile.

Il reindirizzamento dell'output con `>`  consente di salvare l'output dei comandi in file per una successiva consultazione o elaborazione. Ricorda di usare `>` per sovrascrivere e `>>` per aggiungere all'output esistente.

L'uso del reindirizzamento `2>`  Può essere utilizzato per catturare, analizzare e gestire errori in modo più efficace, migliorando il debug e la gestione degli script.

- **comando < FILE_INPUT** stampa l’input del comando eseguito all’interno del file su schermo.
- **awk '{sum += $1} END {print sum}' < numeri.txt** legge i numeri da numeri.txt, li somma utilizzando awk e stampa il risultato della prima colonna
    - **`awk`**: linguaggio di scripting utilizzato per la manipolazione di file di testo.
    - **`{sum += $1}`**: dice ad `awk` di aggiungere il valore della prima colonna di ogni riga alla variabile `sum`.
    - `$1` rappresenta il primo campo (o colonna) di una riga. Ogni volta che `awk` legge una riga, esegue questa operazione.
    - **`END {print sum}`**: dopo che `awk` ha letto tutte le righe del file. Stampa il valore totale della variabile `sum`.
    - **`< numeri.txt`**: Questo reindirizza l'input da `numeri.txt` al comando `awk`, così `awk` legge le righe da `numeri.txt`.
    
    ---
    
- **comando > FILE_OUTPUT** viene utilizzato per reindirizzare l'output di un comando a un file, creando il file se non esiste o sovrascrivendo il file se esiste già.
- **echo "Hello, World!" > FILE_OUTPUT** 
scrive la stringa "Hello, World!" nel file `FILE_OUTPUT`
- **ls FILE** elencherà le informazioni sul FILE nella directory corrente.
- **ls FILE > percorso/FILE.txt** copia il contenuto dentro il percorso scelto sovrascrivendo il contenuto
- **ls FILE >> percorso/FILE.txt** con il doppio segno maiuscolo non sovrascrive il file
- **> FILE_OUTPUT  (**Sovrascrivere il contenuto di un file) crea un file vuoto chiamato `FILE_OUTPUT` se non esiste o svuota il contenuto del file esistente.
- **echo "Another line" >> FILE_OUTPUT**
    - **>>** aggiungere (append) l'output a un file esistente senza sovrascriverlo
- **`/dev/null`**, i dati vengono semplicemente eliminati in un buco nero **la sintassi precisa è di sotto**
- **‘comando > /dev/null/’** crea un buco nero che scarta l'output standard.
- ‘**comando > /dev/null/**’ crea un buco nero che scarta gli errori standard.

---

- **comando 2> FILE_OUTPUT** invia gli **errori standard** dentro il file  FILE_OUTPUT’
- **ls /nonexistentdirectory 2> error_log.txt** Reindirizzare l'output di errore standard (stderr) a un file
    - **ls /nonexistentdirectory** genera un messaggio di errore perché la directory non esiste.
    - **2> error_log.txt** L'output di errore viene reindirizzato a `error_log.txt`.
- **ls /nonexistentdirectory > output_log.txt 2> error_log.txt** Reindirizzare sia stdout che stderr a file separati
    - In questo esempio, qualsiasi output standard del comando `ls` verrà scritto in `output_log.txt`, mentre gli errori verranno scritti in `error_log.txt`.
- **ls /nonexistentdirectory > output_log.txt 2> /dev/null**
    - Questo comando reindirizza l'output standard a `output_log.txt` e scarta tutti gli errori inviandoli a `/dev/null`.
- **ls /nonexistentdirectory > combined_log.txt 2>&1** sia l'output standard che gli errori verranno scritti in `combined_log.txt`.

### **CERCARE PAROLE DENTRO I FILE**

- **grep PAROLA FILE** cerca le stringhe dei file che contengono quella parola
- **grep -i PAROLA FILE** cercherà la parola indifferentemente se è scritta maiuscola o minuscola
- **grep -l PAROLA FILE** Questo comando restituirà solo i nomi dei file che contengono la parola specificata, anziché le stringhe effettive in cui è presente il modello

### **CERCARE PAROLE DENTRO LE DIRECTORY E LE SUB DIRECTORY**

- **find . -type f -exec grep -H parola_da_cercare '{}' \;**
    - **`find .`**: Avvia la ricerca partendo dalla directory corrente e tutte le sue sotto-directory.
    - **`type f`**: Limita la ricerca ai soli file.
    - **`exec grep -H parola_da_cercare '{}' \;`**: Per ciascun file trovato, esegue il comando **`grep -H parola_da_cercare '{}'`**, dove:
        - **`grep`**: È un comando utilizzato per cercare stringhe all'interno di file.
        - **`H`**: Mostra il nome del file insieme alle corrispondenze trovate.
        - **`parola_da_cercare`**: È la parola che **`grep`** cerca all'interno di ciascun file.
        - **`'{}'`**: Viene sostituito con il nome del file corrente trovato da **`find`**.
        - **`\;`**: Indica la fine del comando **`exec`**.

- **find . -type f -exec grep -l parola_da_cercare '{}' \; | xargs mv -v -t ~/**
1. **`find . -type f -exec grep -l parola_da_cercare '{}' \;`**:
    - Trova tutti i file (non directory) nella directory corrente (**`.`**) e nelle sue sotto-directory.
    - Per ciascun file trovato, esegue **`grep -l parola_da_cercare '{}'`**, dove:
        - **`grep -l parola_da_cercare '{}'`** cerca la parola  all'interno di ciascun file.
        - **`l`** fa sì che **`grep`** restituisca solo il nome del file anziché le righe che corrispondono.
    - L'output di questo comando sarà una lista di file che contengono la parola
2. **`| xargs mv -v -t ~/`**:
    - L'operatore **`|`** (pipe) collega l'output del primo comando all'input del secondo.
    - **`xargs`** è un comando utilizzato per trasformare l'output di un comando in argomenti per un altro comando.
    - **`mv -v -t ~/`** sposta (rinomina) i file specificati nella directory specificata (**`~/`** è la tua directory home) -tcon il flag **`v`** che indica a **`mv`** di essere verboso, cioè di mostrare quali file vengono spostati.
    - **`-t`** permette di specificare la directory di destinazione prima dei file da spostare.

### **INFO SU UN FILE**

- **file NOME_FILE** Permette di sapere le info del file, in caso di stegonografia è utilissimo

### **SCANSIONE SCHEDA DI RETE**

**route -n** vediamo la nostra tabella di routing

**arp-scan -I(i maiuscola) SCHEDA DI RETE --localnet** otterremo una scansione locale della scheda di rete selezionata. (eth0, eth1) 



### **IL PING**

- **ping -c 1** **IP_TARGET** Eseguiamo un ping
    - -**c 1** singolo pacchetto
- **ping -c 1** **IP_TARGET -R** ping con Trace router
    - -**R** trace router
- **fping –a –g intervallo_ip** pingare piu reti contemporaneamente
    - **–a**, serve per restringere il numero dei **risultati** ai **soli host attivi**
    - **–g**, ci permette di inserire un **range** di **ip** in formato **CIDR oppure** specificando il **primo IP** dell’intervallo **e l’ultimo** (ad esempio: fping –g 192.168.1.1 192.168.1.150)

### **GENERARE CODICI HASH DI UN FILE**

- **md5sum FILE_NAME** è poco usato
- **sha256sum FILE_NAME**

### **APRIRE VPN DI HACK THE BOX**

- **sudo openvpn NOME_FILE**

### CAMBIARE IMPOSTAZIONI DI RETE

- sudo nano /etc/network/interfaces

### AGGIORNAMENTO SISTEMA

- **sudo apt-get update** (stiamo dicendo al sistema cosa c’è disponibile come aggiornamento)
- **sudo apt-get upgrade** (aggiornamento dei pacchetti)
- **sudo apt-get install NOME_SOFTWARE**
- **sudo apt-get remove NOME_SOFTWARE (**disinstalla il programma senza cancellare i file di configurazione del programma stesso)
- **sudo apt-get --purge remove NOME_SOFTWARE (**cancella software e file di configurazione)

### COMANDI SSH

- **`p` (Porta)**:
Specifica una porta diversa per la connessione SSH (di default è la porta 22).
    - ssh -p 2222 nomeutente@IP
- **`i` (chiave asimmetrica)**:
Usa una chiave privata specifica per l'autenticazione.
    - ssh -i ~/.ssh/id_rsa nomeutente@IP
- **`L` (Port Forwarding Locale)**:
Effettua un tunneling locale, mappando una porta locale a una porta remota.
    - ssh -L 8080:localhost:80 nomeutente@IP
- **`R` (Port Forwarding Remoto)**:
Effettua un tunneling remoto, mappando una porta remota a una porta locale.
    - ssh -R 8080:localhost:80 nomeutente@IP
- **`N` (No comando remoto)**:
Stabilisce una connessione SSH senza eseguire comandi remoti (utile per il port forwarding).
    - ssh -N -L 8080:localhost:80 nomeutente@IP
- **`T` (Disabilita pseudo-terminale)**:
Non alloca un terminale sulla macchina remota (spesso usato per tunneling o esecuzione di script remoti).
    - ssh -T nomeutente@IP
- **`C` (Compressione)**:
Abilita la compressione dei dati per migliorare la velocità su connessioni lente.
    - ssh -C nomeutente@IP
- **`o` (Opzioni specifiche)**:
Permette di specificare varie opzioni di configurazione direttamente dalla riga di comando, come l'algoritmo di crittografia da usare.
    - ssh -o Cipher=blowfish nomeutente@IP
- **`q` (Modalità silenziosa)**:
Sopprime i messaggi di errore e avvisi, utile per esecuzioni di script automatizzati.
    - ssh -q nomeutente@IP
- **`X` (Forwarding X11)**:
Abilita il forwarding X11 per eseguire applicazioni grafiche su un server remoto (come discusso in precedenza).
    - ssh -X nomeutente@IP

### 1. **SCP (Secure Copy Protocol)**

`scp` permette di copiare file in modo sicuro tra un host locale e uno remoto, o tra due host remoti, usando SSH per la connessione.

### Esempi di comandi SCP:

- **Copia di un file dal tuo computer locale al server remoto:**
    - scp /percorso/del/file nomeutente@IP:/percorso/remoto/
- **Copia di un file dal server remoto al tuo computer locale:**
    - scp nomeutente@IP:/percorso/remoto/file /percorso/locale/
- **Copia di una directory (con l'opzione `r` per la ricorsione):**
    - scp -r /percorso/della/cartella nomeutente@IP:/percorso/remoto/
- **Specifica una porta SSH diversa (con `P`):**
    - scp -P 2222 /percorso/del/file nomeutente@IP:/percorso/remoto/

---

### 2. **SFTP (SSH File Transfer Protocol)**

`SFTP` fornisce un'interfaccia interattiva simile a FTP, ma su SSH. Puoi esplorare le directory e trasferire file in modo sicuro.

### Esempi di comandi SFTP:

- **Connettersi a un server remoto via SFTP:**
    - sftp nomeutente@IP
    
    Una volta connesso, puoi eseguire comandi come `get`, `put`, `ls`, `cd`, ecc.
    
- **Scaricare un file dal server remoto al computer locale:**
    - get /percorso/remoto/file /percorso/locale/
- **Caricare un file dal computer locale al server remoto:**
    - put /percorso/locale/file /percorso/remoto/
- **Scaricare una directory in modo ricorsivo:**
    - get -r /percorso/remoto/directory /percorso/locale/
- **Caricare una directory in modo ricorsivo:**
    - put -r /percorso/locale/directory /percorso/remoto/

### Differenze tra SCP e SFTP:

- **SCP** è un comando semplice per trasferire file o directory in modo diretto e veloce.
- **SFTP** offre un'interfaccia interattiva simile a un client FTP, consentendo di esplorare il file system remoto e trasferire file in modo più flessibile.

Entrambi i metodi utilizzano SSH per garantire la sicurezza dei trasferimenti di file.
