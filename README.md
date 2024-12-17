**Netcat** è il tradizionale "coltellino svizzero" del networking. Viene utilizzato per eseguire manualmente tutti i tipi di interazioni di rete, tra cui cose come il banner grabbing durante l'enumerazione, ma, cosa più importante per i nostri usi, può essere utilizzato per ricevere shell inverse e connettersi a porte remote collegate a shell di binding su un sistema di destinazione. Le shell Netcat sono molto instabili (facili da perdere) di default, ma possono essere migliorate tramite tecniche che tratteremo in un prossimo task.

**Socat** è come netcat sotto steroidi. Può fare tutte le stesse cose, e *molte* di più. Le shell Socat sono solitamente più stabili delle shell Netcat appena uscite dalla scatola. In questo senso è di gran lunga superiore a Netcat; tuttavia, ci sono due grandi problemi:

1. La sintassi è più difficile
2. Netcat è installato di default su praticamente ogni distribuzione
    
    Linux
    
    . Socat è installato di default molto raramente.
    

Esistono soluzioni alternative per entrambi i problemi, che esamineremo più avanti.

Sia Socat che Netcat dispongono di versioni .exe utilizzabili su Windows.

**Metasploit -- multi/handler:**

Il **`exploit/multi/handler`**modulo del framework Metasploit è, come socat e netcat, utilizzato per ricevere reverse shell. Essendo parte del framework Metasploit, multi/handler fornisce un modo completamente sviluppato per ottenere shell stabili, con un'ampia varietà di ulteriori opzioni per migliorare la shell catturata. È anche l'unico modo per interagire con una shell *meterpreter* ed è il modo più semplice per gestire payload *in staging* 

**Msfvenom:**

Come multi/handler, msfvenom fa tecnicamente parte del Metasploit Framework, tuttavia, viene fornito come strumento autonomo. Msfvenom viene utilizzato per generare payload al volo. Mentre msfvenom può generare payload diversi da reverse e bind shell, questi sono ciò su cui ci concentreremo in questa stanza. Msfvenom è uno strumento incredibilmente potente.

---

Oltre agli strumenti che abbiamo già trattato, ci sono alcuni repository di shell in molti linguaggi diversi. Uno dei più importanti è [Payloads all the Things](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md) . Anche il PentestMonkey [Reverse Shell Cheatsheet](https://web.archive.org/web/20200901140719/http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet) è comunemente usato. Oltre a queste risorse online, Kali Linux è anche preinstallato con una varietà di webshell che si trovano in **`/usr/share/webshells`**. Il [repository SecLists](https://github.com/danielmiessler/SecLists) , sebbene usato principalmente per le wordlist, contiene anche del codice molto utile per ottenere shell.
