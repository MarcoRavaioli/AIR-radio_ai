# Database Schema

## 1. Overview
The Radio-AI database is designed as a relational system, optimized for PostgreSQL. It manages user identities, generative session states, synchronized listening rooms, and thematic advertising campaigns. The schema utilizes JSONB fields for flexible metadata storage (e.g., AI-extracted intents and targeting parameters) while maintaining strict relational integrity for core entities.

## 2. Entity Relationships
The following logical connections define the system's data flow:
* **Users and Content**: A User creates multiple Prompts and Episodes.
* **Generative Loop**: Each Episode is linked to a single Prompt and consists of multiple sequential Chunks.
* **Social Sync**: A Room is hosted by a User and revolves around a specific Episode.
* **Advertising**: A Campaign contains multiple Ad Spots, which are dynamically inserted as Chunks into various Episodes based on thematic matching.

## 3. Core Tables

### 3.1 Users
Stores platform participant data, including listeners and advertisers.
* **id** (UUID, PK): Unique user identifier.
* **auth_provider** (VARCHAR): OAuth provider (e.g., spotify, apple).
* **auth_subject** (VARCHAR): External ID from the provider.
* **email** (VARCHAR, Optional): User email address.
* **display_name** (VARCHAR): Profile name.
* **account_type** (ENUM): {free, premium, advertiser}.
* **created_at / updated_at** (TIMESTAMP).

### 3.2 Prompts
Captures the raw and processed input that triggers episode generation.
* **id** (UUID, PK): Unique prompt identifier.
* **user_id** (UUID, FK): Reference to the creator.
* **raw_text** (TEXT): Original user input.
* **normalized_text** (TEXT): AI-regenerated description for public display.
* **intents_json** (JSONB): Extracted intents (theme, mood, rubrics, music preferences).
* **created_at** (TIMESTAMP).

### 3.3 Episodes
Represents a generated radio show instance.
* **id** (UUID, PK): Unique episode identifier.
* **user_id** (UUID, FK): Owner of the episode.
* **prompt_id** (UUID, FK): Originating prompt.
* **title** (VARCHAR): AI-generated title.
* **description** (TEXT): Extended description (normalized prompt).
* **duration_sec** (INT): Total estimated length.
* **status** (ENUM): {draft, generated, published, archived}.
* **metadata_json** (JSONB): Active themes, moods, and speaker styles.
* **created_at** (TIMESTAMP).

### 3.4 Chunks
Atomic units of spoken content or audio inserts.
* **id** (UUID, PK): Unique chunk identifier.
* **episode_id** (UUID, FK): Parent episode.
* **chunk_index** (INT): Sequence order in the timeline.
* **chunk_type** (ENUM): {intro, bridge, rubric, ad, outro}.
* **script_text** (TEXT): The source text for the speech.
* **audio_url** (VARCHAR): CDN location of the rendered TTS file.
* **start_offset_sec** (INT): Timing relative to episode start.
* **version** (INT): Version number for regenerations.

### 3.5 Rooms
Manages synchronized listening sessions.
* **id** (UUID, PK): Unique room identifier.
* **episode_id** (UUID, FK): Base episode being played.
* **host_user_id** (UUID, FK): The user controlling the room.
* **status** (ENUM): {active, closed}.
* **current_timestamp_sec** (INT): Shared playback timestamp.
* **created_at / closed_at** (TIMESTAMP).

## 4. Advertising Tables

### 4.1 Campaigns
Defines brand objectives and thematic targets.
* **id** (UUID, PK): Unique campaign identifier.
* **advertiser_id** (UUID, FK): User/Organization account.
* **objective** (ENUM): {sales, traffic, awareness}.
* **budget_total** (NUMERIC): Total campaign allocation.
* **start_date / end_date** (DATE).
* **targeting_json** (JSONB): Target themes, moods, and musical genres.
* **status** (ENUM): {draft, active, paused, completed}.

### 4.2 Ad Spots
Tracks individual ad placements and performance.
* **id** (UUID, PK): Unique spot identifier.
* **campaign_id** (UUID, FK): Parent campaign.
* **episode_id** (UUID, FK): Target episode.
* **chunk_id** (UUID, FK): Audio chunk used for the spot.
* **placement_type** (ENUM): {intro, midroll, preroll_song, postroll_song, outro}.
* **impressions** (INT): Total number of listens.
* **completion_rate** (NUMERIC): Percentage of the spot played.