# Project Roadmap (Dettagliata)

Sulla base delle decisioni architetturali del team, ecco la roadmap estesa per l'MVP.

## 1. Setup dell'Ambiente e Architettura Monorepo
**Obiettivo:** Stabilire le fondamenta infrastrutturali e i contratti tra i servizi.
- [ ] **1.1 Inizializzazione Workspace**: Setup di `pnpm workspaces` o Turborepo per dipendenze condivise, `apps/api-gateway` (NestJS) e `apps/ai-engine` (Python con Poetry o uv). Configurare ESLint/Prettier (Node) e Ruff/Black (Python).
- [ ] **1.2 Containerizzazione**: Scrittura di `docker-compose.yml`, con servizi PostgreSQL (con volume e script init) e Redis (persistenza base), e reti Docker interne.
- [ ] **1.3 Database e ORM**: Configurare Prisma per NestJS e creare le migrazioni tabelle (Users, Prompts, Episodes). 
- [ ] **1.4 Auth Iniziale**: Predisporre l'autenticazione a token e/o login social.

## 2. Intent Extraction (Il Cervello AI)
**Obiettivo:** Un microservizio Python orchestrato via FastAPI.
- [ ] **2.1 Core FastAPI**: Creare `main.py`, middleware logging, errore e router POST `/api/v1/interpret`.
- [ ] **2.2 Pydantic Validation**: Definire in `schemas.py` la formattazione di `PromptRequest` e `IntentResponse` (theme, mood, target\_bpm\_range, preferred\_artists).
- [ ] **2.3 Local LLM Evaluation**: 
    - Setup Inference (Ollama/vLLM).
    - Selezione modelli open-source (es. Llama-3-8B quantizzati).
    - Costringere output JSON validi via grammatiche (es. libreria `Outlines`).
    - Few-Shot Prompting.
    - Benchmarking: Confronto Affidabilità, Latenza (TTFT), e Costo tra gpt-4o-mini e il modello local.

## 3. Playlist Builder (Motore di Selezione)
**Obiettivo:** Mappare l'intento estratto su un set di brani reali.
*(Nota: L'integrazione di default via "Spotify Audio Features" è bloccata API-side, andrà usato un approccio alternativo)*
- [ ] **3.1 Mock Data**: Interfaccia `TrackDTO`. Creazione `mock_catalog.json` per test senza API.
- [ ] **3.2 Algoritmo Ranking**: Hard-filtering (BPM/genre) e Soft-scoring.
- [ ] **3.3 Generazione Scaletta**: Ordinamento per "curva d'energia" e limitazione per durata puntata.

## 4. Script Generation & Fact-Checking (RAG Base)
**Obiettivo:** Generare l'intercalare testuale sincronizzato, verificato e pronto per il TTS.
- [ ] **4.1 Schema Chunk**: Aggiornamento Pydantic con l'array di eventi narrativi (intro/bridge/outro).
- [ ] **4.2 Mock RAG Engine**: Dizionario locale di "fatti" per 10 artisti da estrarre dinamicamente per testare l'assenza di allucinazioni AI.
- [ ] **4.3 LLM Scripting Pipeline**: Generazione system prompt per Speaker ("Tone of Voice"). Parsing dati traccia avanti/indietro, fatti estratti e rubriche.
- [ ] **4.4 Validazione Narrativa**: Controllo lunghezza per stime durata (30-40 secondi a pezzo parlato).

## 5. API Gateway & Integrazione (NestJS Orchestrator)
**Obiettivo:** Esporre al frontend un endpoint unico "Play".
- [ ] **5.1 Setup HTTP Client**: `@nestjs/axios` per l'`AiEngineService` chiamante Python.
- [ ] **5.2 Controller Principale**: Definire `EpisodesController` ed estrazione DTO tramite `class-validator`.
- [ ] **5.3 Orchestrazione DB**: Salvare Prompt "processing" -> Chiamare Python -> Mappare il JSON restituito nel DB relazionale (Episode, Tracks, Chunks). Avvolgere tutto in transazione SQL per consistenza.
- [ ] **5.4 Restituzione Client**: Inviare JSON aggregato al layer riproduzione frontend.
