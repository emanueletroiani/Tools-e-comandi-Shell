Per **scaricare** Nessus, andiamo su https://www.tenable.com/products/nessus e procediamo al download di Nessus essential, cliccando prima «download» poi scegliendo la **versione** corretta per la nostra **Kali Linux** (debian) dalla lista delle versioni disponibili (**controllate** la vostra distribuzione **Kali** con il comando «**uname** –**a»** prima di scaricare la versione di Nessus. Una volta scaricata, eseguite il seguente comando per installare il pacchetto .deb.

![Untitled](https://github.com/user-attachments/assets/279ac50a-5ac8-495e-912d-1151bdfc46d3)


Facciamo partire il servizio con il comando seguente: 

![Untitled](https://github.com/user-attachments/assets/eb251f3f-be6b-432a-a777-5e71dc781d6a)


Una volta che il servizio è stato avviato, possiamo collegarci alla pagina [https://kali:8834](https://kali:8834/) per la configurazione dello scanner (lo scanner si mette in ascolto di default sulla 8834 dell’indirizzo locale). Scegliamo Nessus essentials, ed inseriamo nome cognome ed email per ricevere il codice di attivazione (se non fatto già in precedenza). Inseriamo il codice per iniziare, Nessus inizierà il download del plugin necessari per gli scan. (il download / installazione può prendere un po’ di tempo).

La licenza gratuita essential include un massimo di scansioni di 16 target, oltre alle quali è necessario ripetere la procedura dall’inizio con una nuova licenza. Dall’interfaccia principale, possiamo notare che Nessus mette a disposizione una quantità di scan notevole. Cliccando su uno dei template preimpostati, Nessus ci permette di inserire tutte le info per identificare univocamente i target da scansione e la modalità di scan. Vedremo in dettaglio come configurare un basic scan nelle lezioni di dettaglio sul vulnerability assessment.

**CODICE PER FARLO PARTIRE**

![Untitled](https://github.com/user-attachments/assets/91e840d6-1421-4692-9514-ef34d69b4b4e)


https://kali:8834/ sarebbe https://127.0.0.1:8834/ 

### **COME SI CONFIGURA?**

su : [https://kali:8834](https://kali:8834/)

1. create a new scan
2. Scegliere la tipologia di scansione da utilizzare (ogni scansione ha delle policy preconfigurate)
3. **Scegliamo Basic Network Scan** 

![Untitled](https://github.com/user-attachments/assets/3df21a1a-62e9-47d1-9644-409fc2c026f4)


- **Settings**: dove andremo ad inserire circa la scansione
- **Credentials**:  se necessario inserire le credenziali per autenticarci sui sistemi da scansionare
- **Plugins:** identificano i controlli di sicurezza o famiglie di controlli da abilitare durante la scansione.

# Basic

![Untitled](https://github.com/user-attachments/assets/1aba5091-b428-4444-b75a-8d9c4d8c530f)


- **Basic:**  in questa sezione si inseriscono **informazioni** di carattere generale sulla scansione come **nome, descrizione**, **sistemi target**

# Discovery

![Untitled](https://github.com/user-attachments/assets/04c1fcad-e607-4f88-a6af-b12e902f730f)

- **Discovery**:  in questa sezione si inseriscono le modalità per **effettuare l’host discovery** ed il **port scanner**. Come vedete si può scegliere uno dei template di default «port scan common ports / all ports» oppure optare per una configurazione custom

![Untitled](https://github.com/user-attachments/assets/d2983eb0-d5ef-495a-9580-0548af9bed2a)

- **Host discovery**: si **definiscono** le politiche per l’host discovery, ad esempio il **protocollo** / la **modalità** di **ping** da effettuare.
- **Port Scanning**: in questa sezione si definisce il **tipo** di **scansione** da effettuare, ad esempio, come abbiamo visto anche per i port scanner,  se effettuare una scansione **SYN o** una **TCP**
- **Service Discovery:** che definisce le politiche di «**mapping**» **porta:servizio**

# Assessment

![Untitled](https://github.com/user-attachments/assets/17544900-a68f-465b-ac6c-2f34c9e7df8f)

- **Assessment**:  in questa sezione si inseriscono le modalità per effettuare la **valutazione** delle **vulnerabilità**.  Possiamo **sceglierne** una dove i **valori** sono in parte **predefiniti** oppure una «**custom**» dove tutte le politiche dovranno essere configurate. **Scegliamo «custom»**
1. **General:** Scegliere l’attività di valutazione, un valutazione **troppo accurata** potrebbe avere un impatto **invasivo sui sistemi**.
2. **Brute Force:** in presenza di **schermata** di **login** si può scegliere o di far utilizzare allo strumento solo le credenziali nella scheda «**credentials**» **oppure** di abilitare il **brute force**. Lo strumento proverà in fase di test a «bucare» eventuali login. Notate che qui **vanno dati** i **file** di **username** e **password in input** allo strumento.
3. **Web Application**: si può abilitare o meno il **flag** per la **scansione** delle **web application**.
4. **Windows:**  si possono selezionare o meno alcune **impostazioni** di **enumerazione**
5. **Database**: si possono selezionare o meno **impostazioni** per **autenticazione** su **DB**

# Report

![Untitled](https://github.com/user-attachments/assets/a163bf88-97fb-47f9-b31c-f95dace8c83e)


- **Report**:  in questa sezione si **inseriscono** le linee **guida** che utilizzerà lo strumento per **creare** i **report**.

# Advanced

![Untitled](https://github.com/user-attachments/assets/cdc84e0d-cbbe-411c-9ebf-f0640e6a8d5c)


- **Advanced**:  in questa sezione si possono scegliere delle **impostazioni** avanzate circa l’ottimizzazione e **performance** della **scansione**. Come al solito, possiamo scegliere un **profilo** di **default**, **oppure** uno **custom**. **Vediamo** quello **custom**
1. **General**: in questa sezione possiamo **inserire** delle **esclusioni dalla scansione, )** oppure scegliere i **thread paralleli** e le **performance generali** della **scansione.** Infine, si può scegliere il **livello** di **auditing** e **logging per** eventuale **debug**

SI PRENDE IN **CONSIDERAZIONE** IL REPORT **BASIC NETWORK SCAN**

![Untitled](https://github.com/user-attachments/assets/90b04a1d-589a-4ec8-91f3-d2b25e67a399)

- Possiamo **scegliere** diversi **formati** per il nostro report. **HTML, PDF, CSV.**
- Possiamo scegliere il livello di **dettaglio** delle **info contenute**. Per il report che vedremo abbiamo **scelto** «**detailed vulnerability by host».**

# 1 Info Criticità trovate

E’ una vista di alto livello sulle **vulnerabilità trovate divise** per **colore** / **priorità**: 

- Critical
- High
- Medium
- Low
- Info

![Untitled](https://github.com/user-attachments/assets/7b05f11d-5903-4db3-8d48-1add4aa0b5f6)


# 2 Info Scansione

![Untitled](https://github.com/user-attachments/assets/909a75bd-96e4-481d-9195-d1de72eac27b)

- Scansione (start / end time)
- Host (name, IP, OS)

# 3 info Vulnerabilità

![Untitled](https://github.com/user-attachments/assets/9e7524ee-27f1-4c39-91c6-2ad9016f3fa8)

- Nome della vulnerabilità
- Descrizione dettagliata
- Link correlati

# 4 Info soluzione

![Untitled](https://github.com/user-attachments/assets/37a32831-c6ae-42a6-97ba-7b92cbdcc985)

- Soluzione
- Fattore di rischio
- Score nel sistema CVSS (common vulnerability scoring system)
- Informazioni sul plugin di Nessus che ha identificato la vulnerabilità

# 5 Info Output di comando test vulnerabilità (ip

![Untitled](https://github.com/user-attachments/assets/5be0f0a9-9c0f-42e8-a745-b90a21957ef7)

# Info importarti nel report

- Lo **scoring system**: perché ci **supporta** a prioritizzare eventuali **remediation action** al termine della fase di exploit qualora la vulnerabilità dovesse essere confermata
- **Solution**: in molti casi **coincide con** la **remediation action** da implementare, **o** comunque ci **fornisce** una **linea guida** per **eliminare** la **vulnerabilità**.

Il **report** deve essere utilizzato non solo come fonte di informazioni, ma anche come **strumento** per **approfondire**.

- Per le **vulnerabilità conosciute**, è sempre buono farsi una **lettura** dei **link** che Nessus ci mette a disposizione per **consolidare** sempre meglio i **concetti**
- Per le **vulnerabilità** che **non conosciamo**, è fondamentale **utilizzare** il **report** come base di partenza per **documentarsi** e capire di che si tratta.
