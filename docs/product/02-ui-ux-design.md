# UI/UX Design Guidelines \& Assets

Questo documento consolida le specifiche UI/UX avanzate di Radio-AI.

## 1. Design System \& Temi
L'interfaccia si propone come un "telecomando intelligente" immersivo:
- **Tema Chiaro (Light Mode)**: Selezionabile volontariamente. Adatto per maggiore leggibilità; sfondi neutri bianchi con accent-color identitari che mantengono il glass-effect leggibile.
- **Tema Scuro (Dark Mode)**: (Predefinito per immersività) Sfoca copertine e adatta pannelli a toni scuri per evidenziare contenuti e onda speaker.

## 2. Navigazione Globale (Componenti Base)
1.  **Menu Hamburger (Alto Sx)**: Apre slide-over con impostazioni, piano, profilo e help.
2.  **Notifiche (Alto Dx)**: Apre layer stile-Instagram con gli activity log.
3.  **Suggerimenti (Lampadina)**: Inserisce prompt consigliati. Tap ciclano tra opzioni, long-press apre lista overlay centrale dedicata.
4.  **Cronologia (Orologio)**: Inserisce ultimi prompt. Long Press apre cronologia completa per recuperare sessioni vecchie.
5.  **Prompt Bar (Centro)**: Campo Focus dove l'utente digita intenzioni.
6.  **Seleziona Playlist (Basso Sx)**: Apre overlay (vedi sotto) per forzare importazione musica.
7.  **Conferma (Dx)**: Invia prompt e valida input. *Modale Bloccante:* Se non è selezionato un brano, chiede all'utente "Vuoi aggiungere una playlist manuale o procede AI libera?".
8.  **Tab Navigator (Basso)**: Radio Rooms (Sx), Esplora (Centro), Profilo (Dx).

## 3. Selezione Musica (Overlay Pannello)
L'utente può fare swipe laterale per scegliere la musica prima del via:
- **Left Pane (Link/Playlist)**: Incolla link Spotify/Apple. Tasto import massivo.
- **Right Pane (Manuale)**: Ricerca fuzzy stile "Instagram Stories", tocca per aggiungere brano ed elenca tutti quelli pronti (dropdown dedicato per rimozione rapida).

## 4. Transizioni \& Schermata di Loading (Pre-Generazione)
Rompere la noia della latenza AI in 3-10 secondi:
- Animazione fluida di onde al centro dello schermo.
- "Teasers" rotanti che cambiano con piccoli tap: *"Sto selezionando aneddoti su Michael Jackson..."*, *"Componendo i bridge musicali..."*.
- *Icona Matita:* Ferma momentaneamente il mix permettendo edit testuali dell'ultimo momento (Checkpointing).
- *Gestione Ambiguità:* Avvisi non bloccanti (es. *"Michele Jachson corretto in Michael Jackson"*).

## 5. La Radio Room: "Now Playing" Experience
Schermo dinamico senza affaticamento visivo.
- **Titolo Editable**: In linea in cima, suffissato in `*.fm` per le sessioni pubbliche.
- **Player Centrale Fluid**: L'avatar dell'IA respira ritmicamente. Durante i brani fa cross-fade automatico sulla Cover Art del disco in riproduzione da Spotify/Apple Music.
- **Quote Overlay**: Accesso diretto per leggere il *Live Transcript* generato dall'AI nel caso sfugga una frase.
- **Radio Room Comments**: Al tap sul centro, slide-up (height 60%) da sotto con commenti WebSocket live non invasivi, messaggi host appuntati. Permessi customizzabili (Chi commenta? Chi modera? Anti-abuso AI).

## 6. Quote Cards (Condivisione Social)
Trasformazione del testo parlato dall'IA in Card Condivisibili.
- *Layout*: Virgolette, Timestamp, Cyt principal(3 righe max), Nome Utente, Logo AIR.
- Possibilità di *Swipe Orizzontale* per ruotare template visivi tra Chiaro, Scuro, Glass-Azzurro. Esportazione automatica nello Share-Sheet (WhatsApp, Insta, Salvataggio Rullino locale).
