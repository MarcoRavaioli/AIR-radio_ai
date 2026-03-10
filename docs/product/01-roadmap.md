# Project Roadmap (MVP: 0-6 Months)

## Fase 0: Setup Iniziale e Fondamenta

**Obiettivo:** Creare l'ambiente di sviluppo e l'architettura di base.

- Configurazione repository (GitHub/GitLab).
- Strutturazione folder e monorepo (Backend NestJS, Frontend React Native, AI Python).
- Setup Docker e `docker-compose` locale per database (PostgreSQL/Redis) e microservizi.
- Implementazione del sistema di Autenticazione (JWT base, predisposizione social login).

## Fase 1: Sviluppo AI Pipeline Base (Il Motore)

**Obiettivo:** Trasformare il prompt in dati strutturati e audio.

- Integrazione API Spotify per ricerca brani tramite _audio-features_.
- Addestramento/Tuning LLM (Gabriele) per generare le _audio-features_ dal prompt testuale.
- **Implementazione RAG:** Recupero aneddoti storici (MusicBrainz/Wikipedia) prima della generazione dello script.
- Generazione strutturata a _Chunk_ (JSON temporale).
- Integrazione provider Text-to-Speech (TTS) per il rendering audio dei chunk.

## Fase 2: Orchestrazione e Playback

**Obiettivo:** Sincronizzare la musica locale con la voce AI.

- Sviluppo layer di Mixing Audio sull'app mobile.
- Integrazione SDK nativi Spotify/Apple Music.
- Gestione "Ducking" (abbassamento volume musica durante lo speech AI).
- Gestione della coda (Queueing) basata sui Chunk generati.

## Fase 3: UX, Sviluppo Mobile e Refinements

**Obiettivo:** Un'app usabile, stabile e pronta per il beta testing.

- Sviluppo UI/UX principale (Home, Radio Room, Player).
- Gestione stato persistente (salvataggio episodi/prompt).
- Bugfixing, ottimizzazione latenza e fluidità transizioni audio.

---

## Assegnazione Carico di Lavoro (Stima Settimanale)

- **Marco**: ~7 ore a settimana. Focus su Architettura, Backend Orchestration (NestJS), Integrazione App Mobile e Audio Mixing.
- **Giuseppe**: ~2 ore a settimana. Focus su setup DevOps, infrastruttura Database/Docker, supporto Backend.
- **Gabriele (External Collaborator)**: Ore a progetto (da definire preventivo). Focus esclusivo su AI Pipeline (LLM prompt engineering, RAG, Intent Extraction, output JSON a chunk).
