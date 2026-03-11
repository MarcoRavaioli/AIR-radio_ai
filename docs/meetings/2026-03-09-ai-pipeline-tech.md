# Riassunto Verbale: 9 Marzo 2026

**Data:** 9 Marzo 2026
**Partecipanti:** Marco, Samuele, Gabriele
**Argomento:** Definizione tecnica della pipeline AI e requisiti tecnici.
**File Originale:** `Meeting Minutes/Meeting Transcription - air 09:03:2026.pdf`

## Decisioni Chiave
1.  **Ricerca Musicale tramite Spotify:** Abbandonata l'idea di scaricare il database musicale offline per via di costi/tempo. Si passa al piano dove l'AI estrae "Audio Features" (es. energia, ritmo) dal prompt testuale dell'utente e interroga le API di Spotify.
2.  **Chunking Obbligatorio (Low Latency):** Il modulo AI non deve restituire il testo in un blocco unico, ma generando eventi temporali in JSON (Chunk 1, Chunk 2). Questo serve per riprodurre subito la prima canzone senza far aspettare l'utente.
3.  **Generazione "Speech" (Conduttore AI):** È stato approvato l'utilizzo di Retrieval-Augmented Generation (RAG). L'AI non inventerà gli aneddoti sugli artisti/brani, ma li recupererà da fonti vere (MusicBrainz/Wikipedia) per impedire le allucinazioni.

## Action Items
- **Gabriele:** Testare LLM per la produzione di *audio features* ed estrazione testi da prompt.
- **Gabriele:** Formulare i tempi previsti per l'implementazione JSON (Chunked) e generare il preventivo per mercoledì.
