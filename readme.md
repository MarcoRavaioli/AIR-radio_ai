# AIR (Project Radio-AI)

Radio-AI is an audio streaming platform that transforms standard music playlists into personalized, dynamic radio shows. By leveraging Large Language Models (LLMs) for script generation and a Retrieval-Augmented Generation (RAG) pipeline for fact-checking, the system creates an AI speaker that introduces tracks, narrates cultural trivia, and interacts with the user in real-time.

The platform operates as a "smart remote control" for existing streaming services (Spotify, Apple Music), synchronizing locally played music with server-side generated AI voice chunks.

## Repository Structure

This project follows a monorepo structure to unify the mobile application, backend services, and AI engines.

* **apps/mobile**: React Native (TypeScript) application for iOS and Android. Handles the dual-audio playback logic (Music SDK + TTS Player).
* **apps/api-gateway**: Node.js (NestJS) backend. Manages user sessions, authentication, WebSocket connections for Radio Rooms, and API routing.
* **apps/ai-engine**: Python (FastAPI). The core logic for Prompt Interpretation, Intent Extraction, RAG Fact-Checking, and interfacing with LLM/TTS providers.
* **docs**: Architectural documentation and project specifications.

## Key Features

* **Hybrid Playback**: Combines third-party music streaming (Spotify/Apple Music) with high-fidelity AI speech.
* **Two Listening Modes**:
    * *Mode A (User Playlist)*: Generates a show based on a pre-existing user playlist.
    * *Mode B (AI Playlist)*: Generates the music selection based on a user prompt and mood analysis.
* **Fact-Checking Engine**: A RAG pipeline ensures all cultural and historical anecdotes narrated by the AI are verified against trusted sources.
* **Radio Rooms**: WebSocket-based synchronized listening rooms allowing multiple users to experience the same show simultaneously with low-latency sync.
* **Radio Ads Manager**: A thematic advertising system that targets moods and atmospheres rather than user demographics.

## Documentation

For detailed architectural decisions and data models, refer to the documentation folder:

* [00-manifesto.md](./docs/00-manifesto.md): Product vision and core objectives.
* [01-architecture.md](./docs/01-architecture.md): System design, data flow diagrams, and component breakdown.
* [02-database-schema.md](./docs/02-database-schema.md): ER diagrams and SQL definitions.
* [03-ai-pipeline.md](./docs/03-ai-pipeline.md): Prompt engineering, intent extraction, and RAG workflows.
* [04-api-contracts.md](./docs/04-api-contracts.md): API definitions (Draft).

## Technology Stack

* **Mobile**: React Native, TypeScript.
* **Backend**: Node.js, NestJS, gRPC.
* **AI/Data**: Python, FastAPI, LangChain/LlamaIndex, Pinecone (Vector DB).
* **Infrastructure**: AWS (EKS, S3, CloudFront), PostgreSQL, Redis.

## Getting Started

*(Placeholder for local development setup instructions, env variable configuration, and Docker compose commands)*
