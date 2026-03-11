# Product Manifesto & Vision

## The Problem
The contemporary audio ecosystem is divided into three distinct formats, each with significant limitations:
1.  [cite_start]**Music Streaming**: Offers infinite catalogs but lacks context, narrative, and companionship[cite: 15].
2.  [cite_start]**Podcasts**: High-quality content but static, unresponsive to the listener's immediate context, and production-heavy[cite: 16].
3.  [cite_start]**Traditional Radio**: Offers companionship and spontaneity but cannot adapt to the specific tastes or moods of the individual listener[cite: 17].

## The Solution: Radio-AI
Radio-AI bridges these gaps by creating a personalized radio experience. It is not just a playlist generator; it is a companion that understands context. [cite_start]It fuses the catalog depth of streaming services with the warmth of a radio host, powered by generative AI[cite: 19].

## Core Pillars

### 1. The "Smart Remote" Architecture
Radio-AI does not distribute copyrighted music. Instead, it acts as an intelligent orchestration layer. [cite_start]It controls the user's existing premium accounts (Spotify/Apple Music) to play music locally while seamlessly injecting AI-generated audio chunks (TTS) from our servers[cite: 144, 239]. **Nota Bene**: Spotify fungerà da puro riproduttore multimediale; la selezione musicale "intelligente" e le transizioni emotive sono gestite internamente dai nostri algoritmi proprietari (AI Engine) per superare le limitazioni delle API esterne.

### 2. Verified Storytelling (Truth in AI)
A core differentiator is the reliability of the narrative. Unlike standard LLM wrappers that may hallucinate, Radio-AI implements a strict **Fact-Checking Engine**.
* [cite_start]**Rule**: If the AI mentions a date, a historical event, or an artist anecdote, it must be verified via a Retrieval-Augmented Generation (RAG) pipeline against a trusted knowledge graph[cite: 148].
* **Result**: Users learn real facts while being entertained. [cite_start]Fiction is reserved strictly for creative segments (e.g., imaginary caller sketches) and explicitly framed as such[cite: 502].

### 3. Contextual Advertising
We reject the demographic-heavy tracking of traditional ad-tech. The **Radio Ads Manager** introduces "Thematic Targeting." Advertisers target moods, atmospheres (e.g., "Night Drive," "Focus," "Workout"), and narrative contexts rather than invading user privacy. [cite_start]Ads are generated to fit the sonic texture of the show[cite: 318, 345].

### 4. Social Synchronization
Listening to music is often a solitary experience in the streaming era. Radio-AI reintroduces the communal aspect of radio through **Radio Rooms**. [cite_start]Using low-latency WebSocket synchronization, users can host rooms where everyone hears the same music and the same AI voice at the exact same time, regardless of where they are[cite: 246].

## MVP Goals (0-6 Months)

The initial release (Minimum Viable Product) focuses on validating the core technical loop:
1.  [cite_start]**Hybrid Playback**: Stable synchronization between the TTS audio player and the Spotify/Apple Music SDKs[cite: 1081].
2.  [cite_start]**The Pipeline**: A functional flow from User Prompt -> Intent Extraction -> Script Generation -> TTS Rendering[cite: 1075].
3.  [cite_start]**Modes A & B**: Support for generating shows from both existing user playlists and AI-curated selections[cite: 1082].
4.  [cite_start]**Basic Persistence**: Saving episodes, prompts, and user history[cite: 1083].

## Long-Term Vision
Beyond the MVP, Radio-AI aims to evolve into a creative ecosystem including:
* [cite_start]**Creator Studio**: Tools for users to craft custom formats and share them[cite: 1125].
* [cite_start]**Voice Marketplace**: Licensing premium voices (e.g., celebrities or distinct characters)[cite: 1127].
* [cite_start]**Live-Adaptive Streaming**: Shows that react to real-time events (weather, traffic, news)[cite: 1126].