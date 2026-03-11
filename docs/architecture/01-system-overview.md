# System Architecture

## 1. Architectural Vision

Radio-AI (Project AIR) is built on a loosely coupled microservices architecture. This design ensures horizontal scalability, independent service updates, and efficient resource management for computationally intensive tasks such as LLM inference and TTS rendering.

## 2. Macro-Area Segmentation

The system is divided into three primary functional layers:

### 2.1 User Input Layer

This layer handles the initial interaction where the user defines the show's parameters.

- **Prompt Definition**: Captures natural language instructions regarding themes and moods.
- **Music Preferences**: Sincronizzazione dei metadati delle playlist utente da Spotify o Apple Music (titoli, artisti).
- **Voice Configuration**: Selection of AI speaker timbres and styles.

### 2.2 AI Pipeline Layer

The logical core responsible for content generation and verification.

- **Prompt Interpretation**: Translates raw text into structured JSON intent.
- **Fact-Checking (RAG)**: Validates cultural data against external knowledge bases using RAG. _Requirement constraint: RAG step is mandatory before LLM script generation to prevent hallucinations._
- **Script Generation (Chunking)**: Produces a chunked narrative (30-90 second blocks). _Requirement constraint: JSON output must be a structured array of temporal events (e.g., [Intro, Track 1, Bridge...]) to allow immediate playback._
- **TTS Rendering**: Converts text to speech through high-fidelity neural providers.

### 2.3 Output Layer

The playback and distribution level.

- **Audio Orchestration**: Synchronizes local music playback with remote AI voice chunks.
- **Social Sync**: Manages real-time data broadcasting for Radio Rooms via WebSockets.

## 3. Core Software Modules

### 3.1 API Gateway

Acts as the unified entry point for all client requests. It manages authentication (OAuth2/JWT), rate limiting, and internal service routing.

### 3.2 AI Engine (Python-based)

- **Intent Extractor**: Normalizes and validates instructions for the pipeline.
- **Fact-Checking Engine**: Retrieves data from MusicBrainz, Wikipedia, and proprietary knowledge graphs to eliminate AI hallucinations.
- **Script Generator**: Constructs the narrative timeline, including intros, bridges, and outros.

### 3.3 Orchestration Services (Node.js-based)

- **Session Service**: Maintains the state of active episodes, including current chunk indices and timestamps.
- **Playlist Service**: Manages music metadata and interfaces with Spotify/Apple Music APIs.
- **Streaming Orchestrator**: Coordinates the device-level mixer to ensure seamless transitions between music and speech.

### 3.4 Radio Rooms Service

Utilizes a dedicated WebSocket Hub and Sync Server to maintain a shared clock across multiple devices. It includes a Drift Controller to correct latency differences between listeners.

## 4. Data Flow Sequence

1. **Ingestion**: User submits a prompt and optional playlist ID.
2. **Analysis**: The AI Engine extracts semantic intents (mood, topic, rubrics).
3. **Verification**: The Fact-Checking Engine validates cultural trivia requested in the prompt.
4. **Scripting**: The system generates a full script divided into sequential chunks.
5. **Synthesis**: TTS providers render the audio chunks, which are then cached on the CDN.
6. **Delivery**: The mobile client plays music from the external provider and voice chunks from the Radio-AI CDN in perfect sync.

## 5. Technology Stack Summary

### 5.1 Backend & Infrastructure

- **Microservices**: Node.js (TypeScript) for high-concurrency tasks and Python (FastAPI) for AI services.
- **Communication**: gRPC for high-performance internal service calls and REST JSON for standard APIs.
- **Database**: PostgreSQL for relational data and Redis for session caching and synchronization.
- **Vector DB**: Pinecone or Qdrant for RAG-based fact-checking.

### 5.2 Mobile & Playback

- **Framework**: React Native for cross-platform iOS and Android support.
- **Integration**: Native SDKs for Spotify and Apple Music to handle direct music streaming.
- **Audio Mixing**: A custom layer within the app manages audio focus and volume ducking.
