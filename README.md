# Catalogo — Archivio di Deposito · Soprintendenza del Mare

Sito statico per sfogliare **a faccette** e **su mappa** il catalogo delle buste
dell'**Archivio di Deposito** della Soprintendenza del Mare (Sicilia).

🔗 **Sito**: https://aborruso.github.io/sop_mare_w/

## Contenuto

- `index.html` — l'applicazione (nessun backend)
- `catalogo_data.js` — i dati del catalogo (schede + località riconciliate)

## Funzioni

- **Mappa**: un pallino per località (colore = tipo di luogo), con sotto gli
  **esagoni H3** che rappresentano l'**intensità** (numero di schede per cella);
  slider di risoluzione H3 e legenda.
- **Faccette** (Provincia, Tipo di luogo, Sezione, Serie, Decennio) e ricerca full
  text, con **conteggi che si aggiornano** al filtro applicato.
- **Click su una card** → pannello di lettura della scheda (markdown → HTML).
- **Click su un pallino** → filtra il catalogo alle sole schede che citano quel luogo.

## Dati e provenienza

Le schede sono estratte da file `.doc` con una pipeline Python **idempotente**
(LibreOffice per la conversione + stdlib per il parsing), poi le località sono
**riconciliate** a due livelli: comune **ISTAT** (via `opensituas`) e toponimo
**GeoNames** (dump IT offline + web service per le feature marine). Il file
`catalogo_data.js` è rigenerato dallo script `genera_catalogo.py` della pipeline.

Librerie caricate da CDN (MapLibre GL, Tailwind, h3-js, marked); tile della mappa da
**CARTO** / **OpenStreetMap**.

## Sviluppo locale

Il browser blocca il caricamento dei dati da `file://`, quindi va servito via HTTP:

```bash
python -m http.server 8777    # poi apri http://localhost:8777/
```
