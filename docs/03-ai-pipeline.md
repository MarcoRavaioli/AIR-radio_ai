# AI Pipeline and Logic

## 1. Overview
The AI Pipeline is the core intelligence of Radio-AI. It transforms raw, often colloquial user input into a structured, narratively coherent, and factually verified radio broadcast. The pipeline follows a strictly sequential flow to ensure that every spoken word is contextually relevant to the music and verified for accuracy.

## 2. Intent Extraction and Interpretation
The first stage of the pipeline converts natural language into machine-readable instructions.
* **Semantic Analysis**: The system identifies the primary theme, the desired tone (e.g., energetic, empathetic, or technical), and the specific rubrics requested by the user.
* **Contextual Deduction**: The AI infers the user's mood and situational goals (e.g., "studying for an exam" or "driving to the airport") to adapt the speaker's cadence and the frequency of musical interludes.
* **Parameter Normalization**: Conflicting instructions are resolved, and missing parameters are filled using heuristics to ensure a standardized JSON output for the subsequent modules.

## 3. Script Generation
The Script Generator constructs the narrative arc of the episode.
* **Modular Structure**: Every episode is composed of sequential segments, including an opening intro, bridges between tracks, thematic rubrics, and a concluding outro.
* **Chunked Methodology**: To minimize latency, the script is generated in 30 to 90-second "chunks." This allows the system to start rendering audio for the beginning of the show while the middle and end are still being written.
* **Live Adaptability**: Because the script is generated in chunks, users can update their prompt mid-episode. The generator will preserve already played segments and rewrite only the future chunks to reflect the new instructions.

## 4. Fact-Checking Engine (RAG)
To prevent hallucinations common in standard LLMs, Radio-AI employs a Retrieval-Augmented Generation (RAG) pipeline.
* **Entity Extraction**: The generator identifies names, dates, and historical claims within the draft script.
* **Verification Loop**: These entities are queried against trusted databases (e.g., MusicBrainz, Wikipedia).
* **Alignment and Correction**: If a claim is unverified or incorrect, the engine automatically rewrites the script to ensure factual accuracy or omits the claim entirely. This ensures a clear distinction between verified cultural trivia and creative radio fiction.

## 5. Text-to-Speech (TTS) and Rendering
The final stage converts the verified script into high-fidelity audio.
* **Dual-Tier Rendering**:
    * **Fast Mode**: Uses low-latency neural models to render the first two chunks of an episode in under 2 seconds, ensuring an immediate start for the user.
    * **High-Quality (HQ) Mode**: Renders subsequent chunks or saved episodes using premium models with advanced prosody and emotional depth.
* **Voice Personalization**: Parameters such as timbre, pitch, and vocal posture (e.g., "dramatic" or "intimate") are applied to the speaker based on the episode's mood.

## 6. Logic Flow Summary
1. **User Prompt** -> Raw Text.
2. **Intent Extractor** -> Intent JSON.
3. **Script Generator** -> Draft Script (Chunked).
4. **Fact-Checker** -> Verified Script.
5. **TTS Orchestrator** -> Audio Stream (CDN).