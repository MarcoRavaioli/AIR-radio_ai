# Development Guidelines & Setup

## 1. Prerequisites

Assicurati di avere installati sulla tua macchina:

- Docker e Docker Compose
- Node.js (v20+)
- Python (v3.11+)
- Git

## 2. Local Environment Setup (Docker)

Per garantire la massima coerenza tra i vari membri del team, l'intero backend e l'infrastruttura girano su Docker.

1.  Clona il repository principale.
2.  Copia il file `.env.example` in `.env` e riempilo con le chiavi API necessarie (Spotify Developer, OpenAI/LLM provider, ecc.).
3.  Avvia i servizi con:
    ```bash
    docker-compose up -d --build
    ```

Il `docker-compose.yml` avvierà di base:

- **PostgreSQL**: Sulla porta 5432.
- **Redis**: Sulla porta 6379 (utilizzato per code e gestione sessioni WebSocket).
- **Backend Node.js (NestJS)**: Sulla porta 3000 (Orchestration & API Gateway).
- **Backend Python (FastAPI)**: Sulla porta 8000 (AI Pipeline).

## 3. Code Conventions

### Branching Strategy (Git Flow)

Utilizziamo un workflow basato su `main` e `feature branches`.

- **`main`**: Codice di produzione, stabile, protetto. Ogni rilascio viene taggato.
- **`feature/[nome-task]`**: Rami per lo sviluppo di nuove funzionalità (es: `feature/auth-spotify`). Partono sempre da `main`.
- **`bugfix/[nome-bug]`**: Per la risoluzione di problemi riscontrati. Partono da `main`.
- **`hotfix/[nome-emergenza]`**: Per correzioni critiche immediate direttamente su `main`.

### Commit Guidelines

Segui le specifiche del **Conventional Commits**:

- `feat:` per nuove feature.
- `fix:` per bug risolti.
- `docs:` per modifiche ai markdown nella cartella `/docs`.
- `refactor:` per modifiche strutturali senza cambio di feature.
- `chore:` per aggiornamenti di dipendenze e configurazioni.

Esempio: `feat(ai): aggiunta estrazione aneddoti tramite MusicBrainz API`

### Stile del Codice

- **Node.js/React Native**: Prettier e ESLint (configurazione standard TypeScript).
- **Python**: Black e Flake8/isort. Uso intensivo di Type Hints (Pydantic per validazione).
