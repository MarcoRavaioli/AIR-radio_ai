# UI/UX Design Guidelines

## 1. Design Philosophy

L'interfaccia di Radio-AI deve trasmettere un senso di avanguardia, immersività e minimalismo. Non è un classico lettore musicale, ma un "telecomando intelligente" per un compagno virtuale.

- **Vibrant & Dark**: Utilizzo predefinito della dark mode con gradienti fluidi e accenti di colore vivaci (Deep Purples, Neon Blues) che reagiscono al _mood_ della sessione radiofonica attuale.
- **Gestural First**: Navigazione pensata per l'uso in auto o in movimento (swipe grandi, pulsanti generosi).
- **Focus On The Narrative**: Evidenziare chi sta parlando (il conduttore AI) e qual è l'argomento (il testo generato), in parallelo alla copertina del brano di Spotify.

## 2. Pagine Principali (Core Views)

### 2.1 The Prompt Dashboard (Home)

Il punto di ingresso dell'app, progettato per stimolare l'input testuale.

- **Input Area Protagonista**: Un grande campo di testo in cui l'utente può descrivere come si sente o cosa vuole ascoltare ("Sono in auto verso Roma e piove, fammi compagnia con un po' di rock anni '90 e parlami di storia").
- **Mood Presets (Pills)**: Suggerimenti rapidi in formato pillola per avviare una radio con un tap (es. "Focus Work", "Late Night Vibes", "Morning Energy").
- **History**: Storico degli "episodi" o radio generate recentemente.

### 2.2 The Radio Player (Now Playing)

Il cuore dell'esperienza. Molto più di un semplice player musicale.

- **Smart Canvas**: Sfondo dinamico basato sull'album in riproduzione o sull'atmosfera della puntata.
- **Dual State UI**:
  - _Stato Musica_: Centrato sulla cover art, titolo canzone e controlli musicali base (Skip, Like).
  - _Stato Speech (AI)_: Quando il DJ parla, l'UI si trasforma dolcemente mettendo a fuoco l'onda vocale o l'avatar del conduttore, con un box opzionale che mostra i sottotitoli (il Chunk corrente).
- **Live Injection Control**: Un pulsante rapido per inviare un messaggio al volo al conduttore ("Cambia genere", "Non mi piace, metti pop"). L'AI aggiusterà il copione nei "chunk" successivi.

### 2.3 Radio Rooms (Social Listen)

Interfaccia per le sessioni condivise (WebSocket sync).

- **Room Avatar Bubble**: Lista circolare degli utenti attualmente connessi e sincronizzati con la trasmissione.
- **Reactions**: Possibilità di mandare reazioni live (emoji) che fluttuano sullo schermo di tutti in tempo reale.

## 3. Micro-Iterazioni e Feedback

La latenza è il più grande nemico dell'UX in un'app basata su AI.

- **Generating State**: Durante la creazione del primo "Chunk" (i 2-5 secondi iniziali), lo schermo non deve essere un loader noioso. Deve mostrare lo status dell'AI in tempo reale (es. "Analizzando il mood...", "Recuperando aneddoti su Kurt Cobain...", "Mixando i brani...").
- **Haptic Feedback**: Feedback tattili lievi a ogni transizione importante tra Musica e Voce.
