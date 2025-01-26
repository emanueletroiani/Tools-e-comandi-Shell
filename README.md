E’ una **shell** potente che può essere **installata su** diversi sistemi operativi e tecnologie come  **Android, Java, Linux, Windows** e molte altre. 

Per abbassare la percentuale di rilevamento su una macchina target da Antivirus, IPS and IDS viene eseguite nella memoria RAM.

Le **funzionalità avanzate** di Meterpreter consentono movimenti laterali per **entrare** sempre più **nei sistemi**, fino ad **ottenere accesso completo alle rete** obiettivo.

Può essere **utilizzato anche** per **raccogliere informazioni** circa il **target**, **trasferire file** sulla macchine target, **installare backdoor** e molto altro ancora

# 2 modi per ottenere una shell sul target

- **bind_tcp:** in questa modalità si **inietta** un **processo** sulla **macchina obiettivo**. Questo processo si metterà in **ascolto** su una determinata **porta**, attendendo connessioni dall’esterno. Nella modalità bind_tcp il **servizio** di **shell** è **attivo** sulla **macchina attaccante** e la **connessione avviene dalla macchina dell’attaccante alla macchina target.**
- **reverse_tcp**: in questa modalità si inietta un **processo** sulla macchina obiettivo, che questa volta **effettuerà dalla macchina target** **una connessione verso la macchina dell’attaccante** mettendo a disposizione una shell. **La differenza con il bind_tcp è che nel reverse_tcp è la macchina target che inizia la connessione verso la macchina dell’attaccante.**

# Qual’è la differenza?

Per bipassare i firewall statici si utilizza la reverse in quanto permette la fuoriuscita di dati dall’interno verso l’esterno. di conseguenza con la reverse abbiamo piu probabilità che l’attacco funzioni.

# Esempio

- **search meterpreter** alla selezione dei **peyloads** scegliere quello specifico per la tecnologia

![Untitled](https://github.com/user-attachments/assets/b3473dec-e7a4-49a3-86ba-20f36078c543)

Dopo aver impostato il payload in base alle esigenze, **l’attacco si esegue** con il **comando** «**exploit**» visto in precedenza.

Se l’attacco va a buon fine, si ottiene una sessione Meterpreter.

# Funzioni Meterpreter

**Information gathering**

- **Sistema operativo** e informazioni generali sulla macchina
- **La configurazione della rete** in uso
- **La tabella di routing** della vittima
- **Informazioni sull’utente** che sta eseguendo il processo exploitato

Lista comandi

- **sysinfo**  info varie

![Untitled](https://github.com/user-attachments/assets/84096b0e-f6ba-49bd-ba10-c98b12ede37b)

- route impostazioni di routing della macchina

![Untitled](https://github.com/user-attachments/assets/8a638b91-7163-4f09-b99e-0b7cde02b8af)

- upload e download ci permettono rispettivamente di caricare file dalla nostra macchina sulla macchina vittima e viceversa. La figura mostra la sintassi dei due comandi.

![Untitled](https://github.com/user-attachments/assets/b220bab9-0701-4b72-a9a6-6500db113270)










