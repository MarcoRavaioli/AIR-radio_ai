1. La Scelta Strategica: Perché l'Opzione 2 è il perfetto MVP

Il valore reale risiede nei dati acustici: L'Opzione 2 non si limita a passare parole chiave a Spotify, ma estrae le audio features (energy, valence, tempo) per calcolare la distanza matematica tra la richiesta dell'utente e il brano. Questo garantisce il vero "matching" emotivo che distingue AIR da una normale playlist.

Bocciatura dell'Opzione 3 (Playlist Planning): * Motivazione finanziaria: Il salto di prezzo (da ~1.000€ a ~2.000€) e di tempi (da 10 a 20 giorni) non è giustificato per l'MVP.

Motivazione tecnica: Se l'Opzione 2 calcola già il ranking e la distanza dei brani dal prompt, l'ordinamento (planning) per creare una "curva di energia" è un banale algoritmo di sorting che possiamo implementare noi a valle, senza pagare un premium.

Bocciatura dell'Opzione 4 (Semantic Search Locale):

Troppo prematura. Costruire un Vector DB locale per milioni di brani ha costi infrastrutturali mensili che l'MVP non richiede. Deleghiamo la ricerca a Spotify (Opzione 2) per abbattere i costi di server in questa fase.

2. Condizione Vincolante A: Architettura a Bassa Latenza (Chunking)

Il problema della latenza (Il rischio UX): L'approccio standard proposto dal collaboratore prevede che l'AI generi l'intera scaletta e scriva l'intero copione prima di inviare i dati. Questo significa che l'utente aspetterebbe dai 10 ai 20 secondi fissando uno schermo prima di sentire la musica. Inaccettabile per un'app moderna.

La soluzione richiesta: Output a Blocchi (Chunk):

Il JSON restituito dal modulo AI non deve essere un blocco di testo unico, ma un array strutturato di eventi temporali (es. [Intro, Track 1, Bridge, Track 2]).

Questo ci permette di avviare il motore Text-to-Speech (TTS) e lo streaming del primo brano musicale nel momento esatto in cui viene generato il "Chunk 1", mentre l'AI continua a scrivere i "Chunk" successivi in background.

Impatto sull'integrazione: Solo con questa struttura il nostro Backend (NestJS) può orchestrare correttamente l'abbassamento del volume (ducking) di Spotify e l'inserimento della voce AI al momento giusto.

3. Condizione Vincolante B: Affidabilità Editoriale (Integrazione RAG)

Il problema delle Allucinazioni (Il rischio Brand): Lasciare che un LLM generi liberamente il testo dello speaker ("LLM genera speaker text") porta inevitabilmente a "allucinazioni". L'AI inventerà date, aneddoti sugli artisti o fatti storici pur di riempire il vuoto.

La soluzione richiesta: Fact-Checking Base:

Il collaboratore deve inserire nel suo modulo uno step di Retrieval-Augmented Generation (RAG), anche basilare per l'MVP.

Prima di far scrivere lo script all'LLM, il sistema deve recuperare un'informazione verificata (es. tramite le API di Wikipedia o MusicBrainz) sull'artista o sul brano che sta per essere riprodotto.

L'LLM deve ricevere un System Prompt rigoroso: "Usa SOLO i fatti forniti per presentare il brano. Non inventare aneddoti storici."

Impatto commerciale: Garantisce che Radio-AI sia percepita come un prodotto premium e curato, differenziandoci dai "wrapper" di ChatGPT di bassa lega.

4. Definizione della Roadmap Definitiva (Cosa chiedere al collaboratore)

Alla fine della riunione, il mandato da passare a Gabriele Rubboli Petroselli deve essere questo (Definition of Done per autorizzare il pagamento dell'Opzione 2):

Input: Endpoint che accetta il prompt utente.

Processing: Utilizzo di LLM per estrarre l'intento e query a Spotify per recuperare un pool di brani.

Ranking: Filtraggio dei brani basato sulle audio features reali (non solo sui generi).

Fact-Checking: Recupero di 1-2 aneddoti reali sugli artisti selezionati.

Output (Deliverable): Un payload JSON strutturato a "Chunk" (es. type: "speech" | "music", con i rispettivi ID di Spotify e i testi validati), pronto per essere iniettato nel nostro orchestratore audio.







domande per GA:

1. se noi iniziassimo con il l'opzione 2 per l'MVP, poi se per la versione definitiva voelssimo usare un'altra opzione, i prezzi si sommano o si intersecano?
