# Tech Stack \& Strumenti del Progetto AIR

## 1. Architettura Backend
**Scelto: NestJS (Node.js/TypeScript)**
*   *Perché:* Tipizzazione forte, struttura modulare derivata da Angular (Dependency Injection), perfetta per un API Gateway e per l'orchestrazione. Ha un modulo nativo per i WebSocket (Radio Rooms) e integrazioni solide per Microservices.
*   *Alternative Valutate:*
    *   **Express/Fastify**: Troppo leggeri, rischiano di diventare disordinati in un progetto con molte logiche orchestrative e interazioni db complesse.
    *   **Golang**: Molto performante, ma curva di apprendimento più alta e meno librerie già mature per l'ecosistema React Native rispetto a Node.js.

## 2. Motore AI (AI Pipeline Layer)
**Scelto: Python (FastAPI)**
*   *Perché:* Python è lo standard *de facto* per l'AI e il Machine Learning. FastAPI è asincrono, veloce e usa Pydantic, perfetto per validare i JSON in ingresso e uscita dagli LLM.
*   *Modelli LLM (Local vs Cloud):*
    *   **Cloud (OpenAI gpt-4o-mini / Anthropic Claude 3 Haiku)**: Bassa latenza, nessun costo di infrastruttura fisso GPU, JSON outputs garantiti. Scelta consigliata per l'MVP iniziale per validare il prodotto.
    *   **Lokale (Ollama / vLLM + Llama-3-8B)**: Azzera i costi per token, ma richiede noleggiare server GPU (es. AWS g4dn / Azure) che costano fisso centinaia di euro al mese. I modelli piccoli da 8B faticano a generare JSON perfetti e complessi al primo colpo senza tecniche come *Outlines*.

## 3. Database \& Caching
**Scelto: PostgreSQL + Redis**
*   *Perché:* Postgres è solido per dati relazionali (utenti, episodi, prompt, quote cards). Redis è vitale per le Radio Rooms (gestione stato sessioni WebSocket, sync temporale) e caching.
*   *ORM:* **Prisma** (per NestJS) e **SQLAlchemy** (per Python).

## 4. Text-To-Speech (TTS)
**Scelto: ElevenLabs o Azure Neural Voices**
*   *Perché:* In questo momento, la qualità prosodica e l'intonazione emotiva di ElevenLabs o Azure superano le soluzioni open-source o locali, un fattore critico per una "radio" che deve sembrare umana.
*   *Alternative (Locali):* Modelli come *Coqui TTS* o *Piper*. Sono gratis e veloci, ma la voce suona più robotica. Utili per test locali o MVP a costo zero.

## 5. Front-End (Mobile App)
**Scelto: React Native (Expo)**
*   *Perché:* Codice condiviso tra iOS e Android. Ampio ecosistema per i player audio (es. `react-native-track-player`) e per animazioni fluide (Reanimated).

---

# ⚠️ CRITICITÀ BLOCCANTE: API di Spotify (Aggiornamento 2026)

**Problema riscontrato nel fact-checking:**
Tutta l'ipotesi "Opzione 2" (costruire la radio estraendo le *audio-features* dal prompt e interrogando Spotify) **NON POTRÀ FUNZIONARE PER LE NUOVE APP.**

A partire da fine 2024 e per tutto il 2025/2026, **Spotify ha deprecato massicciamente gli endpoint Web API essenziali**, rimuovendo l'accesso pubblico a:
1.  **Audio Features**: Non si possono più richiedere `danceability`, `energy`, `valence`, ecc.
2.  **Recommendations**: Endpoint per generare playlist seed-based rimosso.
3.  **Audio Analysis**: Struttura dei brani rimossa.

La documentazione e il piano finora si basavano sulla convinzione che Spotify restituisse questi dati liberamente. Allo stato dell'arte odierno (Marzo 2026), un'app in Development Mode non ha più accesso a questi endpoint, limitando l'API Spotify praticamente solo al play/pause dei brani noti e informazioni base del catalogo (non testuali/emozionali).

### Soluzioni Alternative (Da valutare per la Roadmap):
1.  **MusicBrainz + AcousticBrainz**: Database aperti che permettono l'analisi e classificazione, ma coprono meno brani o sono datati (come citato nel documento *Music Metadata* redatto).
2.  **Soluzione Commerciale Alternativa (es. Apple Music API / Deezer)**: Apple fornisce l'API *MusicKit*, ma non offre metriche dettagliate come l'energy.
3.  **Cataloghi Locali/Statistici**: Passare a dataset come Kaggle solo come Seed Database. L'AI cercherà il titolo/artista su Spotify basandosi sui dati appresi internamente, ma Spotify fungerà da **mero riproduttore**, senza fornire la classificazione umorale.
