# Git Workflow Professionale (AIR Repository)

Questo documento definisce il workflow ufficiale per lo sviluppo del progetto AIR. L'obiettivo è mantenere la stabilità del `main` e garantire che ogni modifica sia tracciata, revisionata e verificata.

*Per una panoramica rapida su come iniziare a contribuire, consulta il file [CONTRIBUTING.md](../../CONTRIBUTING.md) nella root del repository.*

## 1. Architettura dei Branch

- **`main`**: Il ramo principale e protetto. Contiene sempre codice stabile, testato e pronto per la produzione. **Mai committare direttamente su `main`.**
- **`feature/[nome-task]`**: Per lo sviluppo di nuove funzionalità (es: `feature/auth-spotify`).
- **`bugfix/[nome-bug]`**: Per la risoluzione di problemi (es: `bugfix/fix-audio-sync`).
- **`hotfix/[nome-emergenza]`**: Per correzioni critiche immediate direttamente da applicare su `main`.

---

## 2. Il Ciclo di Sviluppo (Step-by-Step)

Seguire rigorosamente questi passaggi per ogni modifica:

### 1. Pianificazione
Ogni attività deve nascere da una **Issue su GitHub**.
- Descrive il problema o la funzionalità.
- Serve come riferimento per la Pull Request.

### 2. Sviluppo Locale
Crea un branch dedicato partendo dall'ultimo stato di `main`:
```bash
git checkout main
git pull origin main
git checkout -b feature/nome-della-tua-feature
```
Fai commit piccoli, frequenti e con messaggi chiari (usando [Conventional Commits](https://www.conventionalcommits.org/)):
- `feat:` nuove feature.
- `fix:` correzione bug.
- `docs:` modifiche documentazione.
- `refactor:` miglioramento del codice esistente.

### 3. Proposta (Pull Request)
Quando il lavoro è pronto, fai il push su GitHub e apri una **Pull Request (PR)** verso `main`:
```bash
git push origin feature/nome-della-tua-feature
```
Nella PR:
- Collega la Issue (es: "Closes #12").
- Aggiungi i **Reviewers** obbligatori.

### 4. Revisione (Code Review)
Il team (o l'agente AI incaricato) revisiona il codice:
- Approva se tutto è corretto.
- Richiede modifiche se necessario. Lo sviluppatore aggiorna il codice sul branch e fa nuovamente push.

### 5. Merge
Una volta ottenuta l'approvazione e verificato che i test (se presenti) passino:
- Si esegue il merge della PR su GitHub.
- Si consiglia il metodo "Squash and Merge" per mantenere pulita la cronologia di `main`.

### 6. Pulizia
Dopo il merge:
- Elimina il branch remoto tramite GitHub (pulsante "Delete branch").
- Aggiorna il repository locale ed elimina il branch locale:
```bash
git checkout main
git pull origin main
git branch -d feature/nome-della-tua-feature
```

---

## 3. Regole d'Oro per Agenti AI e Umani

1. **Non rompere il Main**: Prima di aprire una PR, verifica che il codice compili e non introduca regressioni.
2. **Sincronizzazione continua**: Se lavori su un branch per più giorni, aggiornalo regolarmente con `git merge main` (o `git rebase main`) per evitare conflitti giganti alla fine.
3. **No dati sensibili**: Mai includere file `.env`, chiavi API o password nel repository. Usa sempre `.gitignore`.
4. **Trasparenza**: Commenta le tue scelte tecniche nella descrizione della Pull Request.
