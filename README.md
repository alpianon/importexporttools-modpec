# importexporttools_modPEC

## Note for non-Italian users
This is a MOD of a well-known Thunderbird Addon, 
specifically intended to add functionalities to backup [Italian certified email messages](https://en.wikipedia.org/wiki/Certified_email).

If you are not using Italian Certified Email ("PEC") nor you need to create a 
hash list of your messages saved in EML format, you probably do not need this 
MOD at all. 

For the above reason, the remainder of this README file is in Italian language, and the active localizations are only Italian and English-US.

## A cosa serve?
Questo MOD nasce aggiunge all'addon importexporttools delle funzionalità che aiutano l'utente a fare il backup dei messaggi di PEC in modo da poterne provare in futuro l'autenticità, nel rispetto della privacy e della riservatezza della corrispondenza. Per saperne di più, leggete più avanti il paragrafo relativo agli aspetti legali.

* **NOTA**: Come ulteriore funzionalità aggiunta, questo MOD consente di scegliere, nelle opzioni di importexporttools, di **tagliare il percorso completo dei file esportati a 140 caratteri** invece che "solo" a 256 caratteri; questo perchè, se nella generalità dei filesystem il limite è 256 caratteri, quando si usa Ecryptfs (tipicamente, se si sceglie di avere la cartella home cifrata in Ubuntu) il limite è di fatto 140 caratteri, come spiegato meglio [qui](https://unix.stackexchange.com/questions/32795/what-is-the-maximum-allowed-filename-and-folder-size-with-ecryptfs)). Con questa opzione, è possibile salvare i messaggi da importexporttools anche in una cartella cifrata con Ecryptfs senza incorrere nell'errore `NS_ERROR_FILE_NAME_TOO_LONG` se l'oggetto dell'email (dal quale importexporttools genera il nome del file) è troppo lungo.

**ATTENZIONE Questo MOD è ancora work-in-progress, non è ancora stato testato in produzione in modo adeguato, ed è inteso unicamente come applicazione da provare in ambienti di test e sviluppo. Si declina qualsiasi responsabilità per qualsiasi uso in produzione e a fini professionali.**

## Installazione
**Importante: se avete importexporttools (versione originale) installato, dovete disinstallarlo, prima di installare questo MOD.**

Per installare importexporttools "moddato" è sufficiente scaricare il sorgente come ZIP da github, scompattarlo, copiare la cartella `importexporttools@pianon.eu` dentro alla sottocartella "extensions" del proprio profilo Thunderbird (in linux generalmente è `~/.thunderbird/NOMEPROFILO/extensions/`, in windows è `?????????????`) e infine riavviare Thunderbird.

## Come si usa?
Alle tradizionali opzioni di menu di importexporttools, questo MOD aggiunge un'opzione per salvare i messaggi *"come file EML con hash list e verifica SMIME (Backup PEC)"* (nella finestra "cerca ed esporta" l'opzione è indicata come *"EML+hash list+verifica SMIME"* per motivi di spazio ma la funzionalità è la stessa).

Selezionando tale opzione, verrà creata una cartella (con il nome della cartella di Thunderbird e la data e ora di esportazione, se viene esportata un'intera cartella; con il prefisso "Backup_PEC" e la data e ora di esportazione, se vengono esportati solo i messaggi selezionati o cercati). 

All'interno di questa cartella, alla fine dell'esportazione, troverete una sottocartella "messaggi" (contenente i messaggi di PEC esportati in formato EML) e due file, `lista_hash.txt` e `lista_hash_con_nomi_file.txt`: il contenuto del primo andrà inserito in apposita dichiarazione da firmare digitalmente e marcare temporalmente, il secondo andrà conservato insieme al backup come riferimento futuro (vd. più avanti il paragrafo relativo agli aspetti legali).


  * **Importante**: Il contenuto del file `lista_hash_con_nomi_file.txt` è volutamente identico all'output di un comando `sha256sum *` lanciato nella sottocartella `messaggi` dentro alla cartella di backup, in modo da consentire di fare una verifica incrociata sul corretto funzionamento dell'addon.

Durante l'esportazione dei messaggi di PEC, viene anche effettuata una **verifica della firma digitale del provider di PEC (Aruba, Legalmail, ecc.)** all'interno di ciascun messaggio: se la firma di alcuni messaggi non è valida o è scaduta, alla fine dell'esportazione viene visualizzato un messaggio di errore, con indicazione di guardare, per i dettagli, il file `errori_verifica_PEC.txt` nella cartella di esportazione. 

  * **Attenzione**: nel caso vengano rilevati degli errori su alcuni messaggi esportati, la lista degli hash viene comunque generata; ma l'operazione di firma digitale e marcatura temporale su tale lista non ha alcun valore/senso dal punto di vista legale, o meglio non ne ha relativamente ai messaggi sui quali sono stati rilevati degli errori (vd. sempre più avanti il paragrafo relativo agli aspetti legali).

## Aspetti legali relativi al backup dei messaggi di PEC 
### Perchè, nel caso dei messaggi di PEC, un backup "tradizionale" non basta?
da scrivere


### La marca temporale su un archivio di messaggi di PEC: problemi di privacy 
da scrivere

### Una soluzione per fare il backup dei messaggi di PEC nel rispetto della privacy
descrivere la soluzione (lista hash, lista hash con nomi file, cosa si fa se qualcuno chiede di poter verificare un messaggio backuppato ecc.)




