# ⚠️ DA COMPLETARE: JSON Schema e Api Contracts

*Questo file è un segnaposto e un promemoria per completare i contratti API reali.*

Attualmente il file `04-api-contracts.md` è discorsivo. È necessario definire la struttura ESATTA dei JSON che i servizi si scambieranno.

## Strutture da Definire
- [ ] **Payload `POST /api/generate-radio`**: Come il client invia il prompt al backend.
- [ ] **Payload in Uscita dell'AI (Chunking)**: La struttura esatta del JSON generato da Gabriele. Esempio bozza:
```json
{
  "chunk_id": 1,
  "type": "speech", // o "music"
  "text": "Benvenuti in AIR...",
  "duration_ms": 4500,
  "background_music_spotify_id": "3A3..."
}
```
- [ ] **Eventi WebSocket Radio Rooms**: Formato dei messaggi scambiati per la sincronizzazione.
