# API Contracts and Integration

## 1. Overview
Radio-AI utilizes a hybrid API architecture. External communication between the mobile/web clients and the API Gateway is handled via REST and WebSockets. Internal communication between microservices is optimized using gRPC for low-latency synchronous calls and an Event Bus (Kafka/RabbitMQ) for asynchronous tasks like chunk rendering.

## 2. External APIs (Public)

### 2.1 Authentication and Music Linking
* **POST /auth/login**: Standard login via third-party providers including Spotify, Apple, or Google.
* **POST /auth/link-music-provider**: Securely links the user's Spotify or Apple Music account to allow playlist access.
* **POST /auth/refresh**: Issues a new JWT session token.

### 2.2 Episode Management
* **POST /episodes/create**: Initiates a new generation session.
    * *Payload*: raw_prompt (string), playlist_id (optional), voice_params (object), duration (int).
* **GET /episodes/{id}**: Retrieves episode metadata, including the AI-regenerated description and current status.
* **GET /episodes/{id}/stream**: Provides a timeline of signed URLs for voice chunks and the associated music sequence.
* **PATCH /episodes/{id}/prompt**: Updates the prompt for an ongoing episode, triggering the regeneration of future chunks.

### 2.3 Radio Rooms (Real-time)
* **POST /rooms/create**: Initializes a synchronized listening room for a specific episode.
* **POST /rooms/{id}/join**: Allows a participant to enter an existing room.
* **WS /rooms/{id}/sync**: A WebSocket connection for broadcasting timestamps, playback commands (play/pause/seek), and drift correction.

### 2.4 Social and Content
* **POST /quotes/create**: Generates a Quote Card based on a transcript snippet.
* **GET /feed/public**: Retrieves a curated feed of publicly shared episodes and cards.

## 3. Internal Service APIs (Private)

### 3.1 Synchronous (gRPC)
* **Prompt Interpreter Service**: `InterpretPrompt(request) -> IntentJSON`.
* **Playlist Service**: `GetPlaylistMetadata(id)` and `GenerateAIPlaylist(intent_json)`.
* **TTS Orchestrator**: `SynthesizeChunk(text, params)` returns the S3 URL of the rendered audio.

### 3.2 Asynchronous (Event-Driven)
* **Topic: script.generate**: Triggered after intent extraction to produce the chunked narrative script.
* **Topic: ads.match.episode**: Triggered during episode generation to find thematic advertising matches.

## 4. Third-Party Integrations

### 4.1 Music Providers
* **Spotify Web API / Apple Music API**: Used for playlist metadata retrieval and playback control via native SDKs.
* **OAuth 2.0**: The standard for managing secure external authorizations.

### 4.2 AI and Infrastructure
* **LLM Providers**: GPT models for interpretation and scriptwriting.
* **TTS Providers**: OpenAI TTS and ElevenLabs for voice synthesis.
* **Payment (Stripe)**: Manages premium subscriptions and advertiser billing.
* **CDN (CloudFront)**: Ensures global low-latency delivery of voice audio files.