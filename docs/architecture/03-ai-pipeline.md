# AI Pipeline and Logic

## 1. Overview

The AI Pipeline is the core intelligence of Radio-AI. It transforms raw, often colloquial user input into a structured, narratively coherent, and factually verified radio broadcast. The pipeline follows a strictly sequential flow to ensure that every spoken word is contextually relevant to the music and verified for accuracy.

## 2. Intent Extraction and Interpretation

The first stage of the pipeline converts natural language into machine-readable instructions.

- **Semantic Analysis**: The system identifies the primary theme, the desired tone (e.g., energetic, empathetic, or technical), and the specific rubrics requested by the user.
- **Contextual Deduction**: The AI infers the user's mood and situational goals (e.g., "studying for an exam" or "driving to the airport") to adapt the speaker's cadence and the frequency of musical interludes.
- **Parameter Normalization**: Conflicting instructions are resolved, and missing parameters are filled using heuristics to ensure a standardized JSON output for the subsequent modules.

## 3. Script Generation

The Script Generator constructs the narrative arc of the episode.

- **Modular Structure**: Every episode is composed of sequential segments, including an opening intro, bridges between tracks, thematic rubrics, and a concluding outro.
- **Chunked Methodology (Binding Constraint)**: To minimize latency to acceptable UX limits, the JSON returned by the AI module MUST NOT be a single text block. It must be a structured array of temporal events (e.g. `[Intro, Track 1, Bridge, Track 2]`). This exact structure allows the backend (NestJS) to begin TTS and Spotify streaming of "Chunk 1" immediately, while the AI writes subsequent "Chunks" in the background.
- **Live Adaptability**: Because the script is generated in chunks, users can update their prompt mid-episode. The generator will preserve already played segments and rewrite only the future chunks to reflect the new instructions.

## 4. Fact-Checking Engine (RAG) (Binding Constraint)

To prevent hallucinations common in standard LLMs (e.g. inventing dates or historical anecdotes), Radio-AI employs a strict Retrieval-Augmented Generation (RAG) pipeline, even for the MVP.

- **Entity Extraction & Retrieval**: Before letting the LLM write the script, the system retrieves 1-2 verified facts/anecdotes via APIs (e.g., MusicBrainz or Wikipedia) about the selected artist or track.
- **Constrained System Prompt**: The LLM must receive a rigorous prompt: _"Usa SOLO i fatti forniti per presentare il brano. Non inventare aneddoti storici."_
- **Alignment and Correction**: This guarantees brand reliability, showing Radio-AI as a premium product vs. low-level ChatGPT wrappers.

## 5. Text-to-Speech (TTS) and Rendering

The final stage converts the verified script into high-fidelity audio.

- **Dual-Tier Rendering**:
  - **Fast Mode**: Uses low-latency neural models to render the first two chunks of an episode in under 2 seconds, ensuring an immediate start for the user.
  - **High-Quality (HQ) Mode**: Renders subsequent chunks or saved episodes using premium models with advanced prosody and emotional depth.
- **Voice Personalization**: Parameters such as timbre, pitch, and vocal posture (e.g., "dramatic" or "intimate") are applied to the speaker based on the episode's mood.

## 6. Logic Flow Summary

1. **User Prompt** -> Raw Text.
2. **Intent Extractor** -> Intent JSON.
3. **Script Generator** -> Draft Script (Chunked).
4. **Fact-Checker** -> Verified Script.
5. **TTS Orchestrator** -> Audio Stream (CDN).
