**Metasploit** ha una funzione di **database** per semplificare la gestione del progetto ed evitare possibili confusioni durante l'impostazione dei valori dei parametri quando si cerca di attaccare piu target

Per **prima** cosa dovrai **avviare** il **database PostgreSQL**, che Metasploit utilizzerà con il seguente comando:

- **`systemctl start postgresql`**
- Sarà quindi necessario inizializzare il database Metasploit utilizzando il **`msfdb init`**comando.

![image](https://github.com/user-attachments/assets/0922dbf8-700e-489a-8e2c-c7dccce216d9)

- Ora è possibile avviare **`msfconsole`**e controllare lo stato del database utilizzando il **`db_status`**comando.
- La funzionalità database ti consentirà di **creare spazi** di **lavoro** per isolare progetti diversi. Al primo avvio, dovresti trovarti nello spazio di lavoro predefinito. Puoi **elencare** gli **spazi** di **lavoro** disponibili utilizzando il **`workspace`** comando.

 ![image](https://github.com/user-attachments/assets/80370e40-5c47-4647-b026-77869c3c6366)

 Possiamo eseguire scansioni con Nmap utilizzando il db_nmapcomando mostrato di seguito, tutti i risultati verranno salvati nel database. 

 ![image](https://github.com/user-attachments/assets/a5150dad-6554-4b20-b199-cfbae0c5876e)

 Ora è possibile accedere alle informazioni rilevanti per gli host e i servizi in esecuzione sui sistemi di destinazione rispettivamente con i comandi hostse services . 

 ![image](https://github.com/user-attachments/assets/c88bf571-b6bf-4dce-9bda-1cbf6505dfc6)

Una volta che le informazioni sull'host sono memorizzate nel database, è possibile utilizzare il **`hosts -R`** comando per aggiungere questo valore al parametro RHOSTS

# Esempio flusso di Lavoro

1. Utilizzeremo il modulo di scansione delle vulnerabilità che rileva potenziali vulnerabilità MS17-010 con il **`use auxiliary/scanner/smb/smb_ms17_010`**comando.
2. Impostiamo il valore RHOSTS utilizzando **`hosts -R` o set rhosts**
3. Abbiamo digitato **`show optionsdb_nmap`**per verificare se tutti i valori sono stati assegnati correttamente. (In questo esempio, 10.10.138.32 è l'indirizzo IP che abbiamo scansionato in precedenza utilizzando ilcomando)
4. Una volta impostati tutti i parametri, lanciamo l'exploit utilizzando il comando **`runexploit`**or **exploit or run**

![image](https://github.com/user-attachments/assets/5b93e404-0820-4149-a55a-11b10b464346)

Se nel database è salvato più di un host, quando **hosts -R** si utilizza il comando verranno utilizzati tutti gli indirizzi IP.

In un tipico intervento di penetration testing, potremmo avere il seguente scenario:

- Trovare gli host disponibili utilizzando il database **`db_nmap`** 
    
- Scansionarli per ulteriori vulnerabilità o porte aperte (utilizzando un modulo di scansione delle porte)

Il comando services utilizzato con il **`-S`**parametro consentirà di cercare servizi specifici nell'ambiente.

![image](https://github.com/user-attachments/assets/8acd48cd-5398-4c5c-9d79-f3abce478ce0)

# Ecco alcune vulnerabilità che potrai trovare tri i servizi

- **HTTP**: potrebbe potenzialmente ospitare un'applicazione web in cui è possibile trovare vulnerabilità come l'iniezione SQL o l'esecuzione di codice remoto (RCE).
- **FTP**: potrebbe consentire l'accesso anonimo e fornire l'accesso a file interessanti.
- **SMB**: potrebbe essere vulnerabile a exploit SMB come MS17-010
- **SSH**: potrebbe avere credenziali predefinite o facili da indovinare
- **RDP**: potrebbe essere vulnerabile a Bluekeep o consentire l'accesso al desktop se vengono utilizzate credenziali deboli.






  
