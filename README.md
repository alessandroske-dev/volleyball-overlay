# 🏐 Volleyball Overlay

Overlay grafico in tempo reale per lo streaming di partite di pallavolo (indoor e beach volley), pensato per essere usato come **browser source** in [Prism Live Studio](https://prismlive.com/) (o OBS) e pilotato a distanza tramite una pagina di controllo separata.

I dati (punteggio, set, nomi squadre, banner sponsor, ticker) vengono sincronizzati in tempo reale tra `control.html` e `overlay.html` tramite **Firebase Realtime Database**, così chi gestisce il punteggio da bordo campo (o da remoto) può aggiornare l'overlay senza toccare il software di streaming.

## 📁 Struttura del progetto

| File | Descrizione |
|---|---|
| `overlay.html` | Overlay principale da caricare come browser source nello streaming software |
| `control.html` | Pannello di controllo per aggiornare punteggio, set e testi in tempo reale |
| `beach_volley.html` | Variante dell'overlay per il beach volley |
| `beach_volley_control.html` | Pannello di controllo dedicato alla variante beach volley |
| `tema.html` | Gestione/anteprima del tema grafico dell'overlay |
| `cheatsheet_calendario.html` | Cheatsheet per il calendario partite |
| `test-audio.html` | Pagina di test per verificare che l'audio venga riprodotto come browser source (beep a 440 Hz o mp3 in loop) |

## ⚙️ Come funziona

1. `control.html` scrive gli aggiornamenti (punteggio, set, sponsor, ticker) su un percorso di **Firebase Realtime Database**.
2. `overlay.html` è in ascolto su quello stesso percorso e si aggiorna automaticamente non appena arriva un cambiamento.
3. In Prism Live Studio (o OBS), `overlay.html` viene aggiunto come **browser source** in sovraimpressione al video della partita.

```
control.html  --(scrive)-->  Firebase Realtime Database  --(legge in real-time)-->  overlay.html --> Browser Source in Prism/OBS
```

## 🚀 Utilizzo

1. Configura un progetto Firebase con Realtime Database abilitato e imposta le **Security Rules** in modo appropriato (vedi la sezione Sicurezza).
2. Se usi un progetto Firebase diverso dal tuo, sostituisci l'oggetto `firebaseConfig` in `overlay.html`, `control.html`, `beach_volley.html`, `beach_volley_control.html` e `tema.html`.
3. Pubblica i file (ad esempio con [GitHub Pages](../../settings/pages) oppure su un tuo hosting) per ottenere URL utilizzabili come browser source. Con GitHub Pages attivo gli indirizzi sono:
   - Overlay: `https://alessandroske-dev.github.io/volleyball-overlay/overlay.html`
   - Controllo: `https://alessandroske-dev.github.io/volleyball-overlay/control.html`
4. Apri `control.html` da telefono/tablet a bordo campo e `overlay.html` come browser source nel software di streaming.

### Test audio

`test-audio.html` accetta questi parametri nell'URL:

- `?mode=beep` (predefinito): tono a intermittenza generato dal browser.
- `?mode=mp3&src=https://.../file.mp3`: riproduce un mp3 in loop.
- `?delay=3`: secondi prima del tentativo di avvio automatico (predefinito 3).

La pagina mostra se l'audio è partito o è stato bloccato dal browser.

## 🔒 Sicurezza

La configurazione Firebase lato client (`apiKey`, `databaseURL`, ecc.) è visibile nei file HTML: è normale per le app web, ma significa che **la protezione dei dati dipende interamente dalle Security Rules del Realtime Database**. Consigli:

- Consenti la lettura pubblica solo dei percorsi usati dall'overlay.
- Limita la scrittura (ad esempio con autenticazione) in modo che solo il pannello di controllo possa modificare punteggio e testi.
- Restringi la API key ai domini da cui servi le pagine, dalla console Google Cloud.

## 🎥 Setup streaming consigliato

- Smartphone come sorgente video (es. Pixel 9a)
- Connessione tramite router 5G/4G portatile per la banda in palazzetto
- App di streaming: Prism Live Studio
- Audio: microfono esterno dedicato

## 📝 Licenza

Distribuito con licenza MIT — vedi [LICENSE](LICENSE).

## 🙋 Autore

Progetto sviluppato e mantenuto da [@alessandroske-dev](https://github.com/alessandroske-dev) per lo streaming delle partite di volley locali.
