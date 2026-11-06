# Straordinari e Reperibilità

App web (installabile sul telefono) per registrare gli straordinari, la reperibilità e le ore guida, con report mensile e annuale esportabili in PDF e CSV.

Funziona interamente nel browser. Non c'è nessun server: i dati restano nella memoria del dispositivo e non vengono inviati a nessuno.

## Cosa fa

- **Quattro tipi di prestazione**: straordinario normale, straordinario in reperibilità, reperibilità, ore guida. Ognuno ha il suo colore.
- **Inserimento** con data e ora di inizio e di fine (anche su più giorni), note, modifica e cancellazione.
- **Fasce orarie automatiche**: diurno, notturno, festivo, festivo notturno. Le festività italiane (Pasqua compresa) sono già incluse. L'inizio e la fine della notte e il sabato festivo sono regolabili.
- **Regola delle prime 2 ore** di straordinario di ogni giornata, con tariffe diverse per le ore successive.
- **Importo stimato** in base alle tariffe orarie che inserisci. Sotto ogni tariffa viene mostrata la percentuale rispetto alla retribuzione di riferimento.
- **Reperibilità**: le ore di intervento vengono tolte dalla reperibilità (opzione attiva di default).
- **Riposo compensativo** dopo gli interventi: l'app indica se spetta mezza giornata, una giornata o un'altra quantità di riposo, e a che ora si rientra.
- **Report**: mensile e annuale, con le ore in centesimi e in h:mm. La vista **"Per busta paga"** mette insieme i turni dei mesi giusti, in base ai ritardi di pagamento.
- **Esportazioni**: PDF e CSV del mese, dell'anno e di tutti i dati. **Backup** e ripristino in JSON.

## Come si usa

1. Apri il sito dell'app dal telefono con Chrome.
2. Dal menu ⋮ scegli **Aggiungi a schermata Home** (o **Installa app**). Si apre a schermo intero, anche senza internet.
3. Alla prima apertura vai in **⚙**:
   - inserisci la **retribuzione lorda mensile** e il **divisore orario** (servono per le percentuali);
   - inserisci le **tariffe orarie** (€/h, già comprensive di maggiorazione) che trovi sulla tua busta paga, dividendo l'importo di ogni voce per le sue ore;
   - controlla l'inizio e la fine della **notte**, l'orario di lavoro e le altre regole.
4. Usa **Inserisci** per aggiungere le prestazioni e **Mese** o **Anno** per i report.

Le tariffe non sono preimpostate, perché dipendono dall'inquadramento, dagli scatti e dagli accordi di ciascuno.

## Dati, backup e aggiornamenti

- I dati sono salvati nel browser (`localStorage`) **di quel dispositivo e di quell'indirizzo**. Se cancelli i dati di Chrome, cambi telefono o cambia l'indirizzo del sito, li perdi.
- Fai ogni tanto **Salva backup**. Il file JSON contiene anche le impostazioni. Per spostare i dati su un altro dispositivo usa **Ripristina backup**.
- Gli aggiornamenti arrivano da soli: con internet l'app carica sempre l'ultima versione. Il numero di versione è in fondo alla scheda ⚙.

## Avvertenze

1. **Strumento personale.** L'app serve a registrare le proprie ore e a ottenere una stima dei compensi. Non è un software di elaborazione paghe.
2. **Possibili errori.** Tariffe, percentuali, fasce orarie e festività sono impostazioni modificabili e possono essere incomplete o non aggiornate. I contratti e gli accordi aziendali possono cambiare o prevedere regole diverse da quelle ipotizzate.
3. **Nessuna responsabilità.** L'autore non si assume alcuna responsabilità per errori, omissioni o differenze tra i risultati dell'app e la busta paga, né per decisioni prese sulla base di tali risultati.
4. **Nessun valore ufficiale.** Report, PDF ed esportazioni non costituiscono documenti ufficiali e non devono essere usati come prova o per contestazioni con il datore di lavoro. Per verifiche e rivendicazioni occorre fare riferimento alla busta paga, al contratto collettivo applicato e agli uffici competenti (ufficio paghe, sindacato, consulente del lavoro).
5. **Dati.** I dati restano sul dispositivo e non vengono inviati a terzi. L'utente è responsabile dei propri backup.

## Per chi sviluppa

Il progetto è composto da pochi file statici, senza passaggi di compilazione:

```
index.html              l'app (HTML, CSS e JavaScript)
manifest.webmanifest    dati per l'installazione sul telefono
sw.js                   service worker: uso offline
icons/                  icone dell'app
vendor/                 jsPDF 2.5.1 (licenza MIT), per generare i PDF
```

Per provarla in locale serve un piccolo server, perché il service worker non funziona aprendo il file direttamente:

```
python3 -m http.server 8000
```

e poi `http://localhost:8000`.

### Pubblicazione con GitHub Pages

Nelle impostazioni del repository: **Settings → Pages → Build and deployment → Deploy from a branch**, branch `main`, cartella `/ (root)`. Dopo un minuto il sito è disponibile su `https://<utente>.github.io/ore-lavoro/`.

Quando cambi il codice in modo che i file memorizzati dal service worker siano diversi, aggiorna `VERSIONE` in `sw.js` e il numero in `index.html`.

## Licenza

La libreria [jsPDF](https://github.com/parallax/jsPDF) in `vendor/` è distribuita con licenza MIT (vedi `vendor/LICENSE-jspdf.txt`).
