### **Scansione delle porte**

Metasploit ha un certo numero di **moduli per scansionare** le **porte aperte** sul sistema e sulla rete di destinazione. Puoi **elencare** i potenziali **moduli** di scansione delle porte disponibili usando il **`search portscan`** comando.

**I moduli di scansione delle porte richiederanno di impostare alcune opzioni**

![image](https://github.com/user-attachments/assets/ba92915e-0b44-4205-89f5-f832e9c642b5)

- **CONCURRENCY:** Numero di target da scansionare simultaneamente.
- **PORTS:** Intervallo di porte da scansionare. Si noti che 1-1000 qui non sarà lo stesso che usare Nmap con la configurazione predefinita. Nmap scansionerà le 1000 porte più usate, mentre Metasploit scansionerà i numeri di porta da 1 a 10000.
- **RHOSTS:** Target o rete di destinazione da sottoporre a scansione.
- **THREAD:** Numero di thread che verranno utilizzati contemporaneamente. Più thread daranno luogo a scansioni più veloci.

### You can directly perform Nmap scans from the msfconsole prompt as shown below faster:

![image](https://github.com/user-attachments/assets/1d9047f4-42c7-4a70-8dd5-7591859b7c4c)

### **UDP service Identification**

Il modulo **`scanner/discovery/udp_sweep`**  ti consentirà di **identificare rapidamente** i **servizi** che girano su **UDP** (User Datagram Protocol). Questo modulo non eseguirà una scansione estesa di tutti i possibili servizi UDP , ma fornisce un modo rapido per **identificare servizi** come **DNS** o **NetBIOS**.

![image](https://github.com/user-attachments/assets/d2a96f08-23d1-4345-a5ee-d3612a6026eb)

### **SMB Scans**

Metasploit offre diversi moduli ausiliari utili che ci consentono di analizzare servizi specifici. Di seguito è riportato un esempio per SMB . Particolarmente utile in una rete aziendale sarebbe **`smb_enumshares`** e **`smb_version`**

![image](https://github.com/user-attachments/assets/aa047940-b1db-4ef6-9551-f0a99ed8c4b5)


