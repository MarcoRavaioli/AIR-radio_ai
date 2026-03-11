# Guida alla Contribuzione (AIR Project)

Benvenuto nel progetto AIR! Questo documento fornisce le linee guida per contribuire in modo efficace e professionale al repository.

## 🚀 Il Nostro Workflow (GitHub Flow)

Seguiamo rigorosamente il modello **GitHub Flow**:

1.  **Cerca o apri una Issue**: Ogni sviluppo o bugfix deve essere tracciato.
2.  **Crea un Branch**: `feature/descrizione`, `bugfix/descrizione` o `hotfix/descrizione` partendo da `main`.
3.  **Sviluppa e Committa**: Usa i [Conventional Commits](https://www.conventionalcommits.org/) (es. `feat: ...`, `fix: ...`).
4.  **Apri una Pull Request (PR)**: Usa il template predefinito e linka la Issue correlata.
5.  **Passa i Controlli (CI/CD)**: Le GitHub Actions verificheranno automaticamente il tuo codice.
6.  **Code Review**: Almeno un membro del team deve approvare le modifiche.
7.  **Merge e Cleanup**: Una volta approvata, eseguiamo lo "Squash and Merge" e cancelliamo il branch.

## 📘 Risorse Utili

Per dettagli approfonditi sulle procedure Git, consulta la nostra guida dedicata:
👉 **[Git Workflow Dettagliato](docs/guidelines/02-git-workflow.md)**

## 🛠️ Setup di Sviluppo

Il progetto è un monorepo suddiviso in:
- `apps/api-gateway`: Backend NestJS.
- `apps/ai-engine`: Python FastAPI.
- `apps/mobile`: React Native.

Consulta i README all'interno di ogni cartella (quando disponibili) per istruzioni specifiche sull'installazione delle dipendenze e l'esecuzione dei test.

## ⚖️ Regole d'Oro
- **Mai pushare dati sensibili**: Controlla sempre di non includere file `.env`.
- **Test d'obbligo**: Non aprire PR senza aver verificato il codice localmente.
- **Documentazione**: Aggiorna i file `.md` se le tue modifiche cambiano l'architettura o le API.

Grazie per la tua collaborazione!
