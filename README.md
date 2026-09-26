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

## ⚙️ Come funziona

1. `control.html` scrive gli aggiornamenti (punteggio, set, sponsor, ticker) su un percorso di **Firebase Realtime Database**.
2. `overlay.html` è in ascolto su quello stesso percorso e si aggiorna automaticamente non appena arriva un cambiamento.
3. In Prism Live Studio (o OBS), `overlay.html` viene aggiunto come **browser source** in sovraimpressione al video della partita.

```
control.html  --(scrive)-->  Firebase Realtime Database  --(legge in real-time)-->  overlay.html --> Browser Source in Prism/OBS
```

## 🚀 Utilizzo

1. Configura un progetto Firebase con Realtime Database abilitato e imposta le **Security Rules** in modo appropriato (lettura pubblica se serve, scrittura ristretta).
2. Inserisci le credenziali del tuo progetto Firebase nella configurazione in `overlay.html` e `control.html`.
3. Se attivi [GitHub Pages](../../settings/pages) su questo repo, ottieni un URL pubblico direttamente utilizzabile come browser source, ad esempio:
   - Overlay: `https://alessandroske-dev.github.io/volleyball-overlay/overlay.html`
   - Controllo: `https://alessandroske-dev.github.io/volleyball-overlay/control.html`
4. Apri `control.html` da telefono/tablet a bordo campo e `overlay.html` come browser source nel software di streaming.

## 🎥 Setup streaming consigliato

- Smartphone come sorgente video (es. Pixel 9a)
- Connessione tramite router 5G/4G portatile per la banda in palazzetto
- App di streaming: Prism Live Studio
- Audio: microfono esterno dedicato

## 📝 Licenza

Distribuito con licenza MIT — vedi [LICENSE](LICENSE).

## 🙋 Autore

Progetto sviluppato e mantenuto da [@alessandroske-dev](https://github.com/alessandroske-dev) per lo streaming delle partite di volley locali.
