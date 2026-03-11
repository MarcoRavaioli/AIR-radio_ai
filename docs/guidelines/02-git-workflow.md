# Git Workflow e Linee Guida per Collaboratori

Questo repository utilizza Git per mantenere la cronologia e organizzare il lavoro simultaneo su microservizi diversi (Backend, AI, Frontend).

## 1. Architettura dei Branch

- `main` (o `master`): Il codice in produzione, sempre stabile e funzionante. Mai committare direttamente qui.
- `develop`: Il ramo centrale di integrazione delle nuove funzionalità. Da qui si staccano i branch di lavoro.
- `feature/[nome-feature]`: Branch per sviluppare novità. Esempio: `feature/auth-spotify`, `feature/llm-prompt-parser`.
- `bugfix/[nome-bug]`: Branch per risolvere problemi. Esempio: `bugfix/fix-audio-latency`.

*Nota:* Attualmente esiste un branch locale `develop/api-gateway`. Se state usando uno schema `[rama]/[progetto]`, va bene, ma si consiglia un prefisso esplicito (es: `feature/api-gateway`).

## 2. Flusso di Lavoro (Il "Git Flow")

Quando inizio a lavorare su una nuova modifica, seguo questo flusso:

1. **Sincronizzo il repo locale**:
   ```bash
   git checkout develop
   git pull origin develop
   ```
2. **Creo il mio branch**:
   ```bash
   git checkout -b feature/la-mia-nuova-feature
   ```
3. **Sviluppo e faccio commit**:
   Mentre scrivo codice, faccio commit piccoli e chiari, seguendo la convenzione Conventional Commits:
   - `feat:` per nuove implementazioni.
   - `fix:` per bug.
   - `docs:` per modifiche ai `.md`.
   - `refactor:` codice migliorato senza aggiungere feature.
   
   ```bash
   git add .
   git commit -m "feat(ai): aggiunto parsing del mood dal prompt"
   ```
4. **Push e Pull Request (PR)**:
   ```bash
   git push origin feature/la-mia-nuova-feature
   ```
   * Su GitHub apro una "Pull Request" verso `develop`.
   * Chiedo a Marco o Giuseppe di fare una rapida Review.
   * Una volta approvata, la PR viene mergiata in `develop`. E posso cancellare il mio branch in remoto.

## 3. Gestire i Conflitti (Merge Conflict)

Se due persone hanno modificato lo stesso file:
1. Mentre sono sul mio branch, recupero i file aggiornati: `git pull origin develop`.
2. Git mi avviserà che c'è un conflitto.
3. Apro Visual Studio Code: i file in conflitto avranno blocchi `<<<<<<< HEAD` (le mie modifiche) e `>>>>>>> develop` (le loro modifiche).
4. Scelgo quale tenere o le unisco.
5. Salvo, poi lancio `git add .` e `git commit -m "fix: risolto merge conflict"`.

## 4. Evitare gli errori comuni
- **Mai pushare dati sensibili**: Le chiavi API vanno nel file `.env`, e il file `.env` deve essere elencato dentro `.gitignore`. Usare `.env.example` per far capire ai colleghi quali chiavi servono senza esporne il valore.
- **Commit frequenti**: Non scrivere mille righe e fare un solo commit. Committa per blocchi logici per facilitare i rollback in caso di errore.
