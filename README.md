# Virtus Groane ASD - Sito Web Ufficiale

Repository del sito web istituzionale di **Virtus Groane ASD** ([virtusgroane.com](https://www.virtusgroane.com)).  
Sito statico ad alte prestazioni, accessibile e responsive, sviluppato in HTML5 semantico, CSS3 e JavaScript vanilla per garantire massima velocità di caricamento, facilità di manutenzione e ottima indicizzazione sui motori di ricerca.

---

## 📁 Struttura del Progetto

```
virtus-groane/
├── index.html                      # Home page con sezioni principali e corsi
├── virtus.html                     # Portale "Chi Siamo" / Società
├── virtus/                         # Sottosezioni societarie
│   ├── organigramma.html           # Consiglio direttivo e cariche
│   ├── allenatori.html             # Staff tecnico e qualifiche
│   ├── safeguarding.html           # Politiche e responsabile tutela minori/soci
│   ├── tesseramento.html           # Enti affiliati (FIDAL, FITRI, AICS, FIASP)
│   ├── statuto-sociale.html        # Statuto costitutivo ufficiale
│   ├── associarsi.html             # Vantaggi e modalità per associarsi
│   ├── regolamenti.html            # Norme di accesso alle piste e impianti
│   └── collaborazioni.html         # Accordi e sinergie con altre società
├── info-iscrizioni.html            # Portale corsi e iscrizioni
├── info-iscrizioni/                # Pagine di dettaglio per disciplina e logistica
│   ├── atletica-leggera.html       # Dalle categorie giovanili agli Assoluti e Master
│   ├── triathlon.html              # Settore multisport
│   ├── running-school.html         # Corso per podisti amatori e neofiti
│   ├── mamme-che-sport.html        # Fitness e tonificazione all'aperto
│   ├── nordic-walking.html         # Camminata nordica con istruttori SINW
│   ├── visita-medica.html          # Certificati medici (agonistici e non)
│   ├── convenzioni.html            # Centri medici, fisioterapici e palestre
│   ├── golee.html                  # Guida all'app gestionale e pagamenti
│   └── dove-ci-alleniamo.html      # Centri sportivi di Senago, Solaro e Limbiate
├── abbigliamento.html              # Presentazione linea tecnica e merchandising
├── abbigliamento/
│   ├── catalogo.html               # Catalogo online prodotti
│   ├── ordini.html                 # Moduli d'ordine per tipologia di capo
│   └── fornitori.html              # Partner tecnici ufficiali (Bioracer, Bitre)
├── societa-ed-eventi.html          # Portale eventi e manifestazioni
├── societa-ed-eventi/
│   ├── record-societari.html       # Albo d'oro con filtri dinamici per disciplina/categoria
│   ├── gara-sociale.html           # Campionato interno societario con algoritmo a compensazione
│   ├── 24x1-ora.html               # Partecipazione alla staffetta su pista
│   ├── estate-correndo.html        # Circuito podistico estivo (tappa Senago)
│   ├── fametta-run.html            # Corsa non competitiva nel Parco delle Groane
│   ├── 10k-delle-groane.html       # Manifestazione podistica competitiva e non
│   ├── prova-l-atletica.html       # Open day e prove gratuite per neofiti
│   └── dicono-di-noi.html          # Rassegna stampa e articoli di giornale
├── sostieni-virtus.html            # Come sostenere l'associazione
├── sostieni-virtus/
│   ├── donazioni.html              # Erogazioni liberali e ringraziamento donatori
│   ├── 5x1000.html                 # Destinazione del 5x1000 nella dichiarazione dei redditi
│   ├── giocoatletica-2025.html     # Sponsor manifestazioni giovanili
│   ├── estate-correndo-2026.html   # Sponsor circuito estivo
│   ├── tutti-in-campo.html         # Iniziativa promozionale supermercati
│   └── amici-dello-sport.html      # Campagna Esselunga "Amici di Scuola e dello Sport"
├── contatti.html                   # Canali ufficiali, segreteria e recapiti referenti
├── english.html                    # Pagina di presentazione per contatti internazionali
├── privacy-policy.html             # Informativa sul trattamento dei dati personali
├── 404.html                        # Pagina di errore personalizzata
│
├── style.css                       # Foglio di stile principale unificato e responsive
├── data/                           # Dati strutturati (es. record societari JS/JSON)
├── docs/                           # Documenti e moduli PDF ufficiali (statuto, regolamento, ecc.)
├── images/                         # Asset grafici, loghi, foto ottimizzate in formato WebP e PNG
├── virtus-non-pubblico/            # File sorgenti di lavoro, storico atleti e tabelle di supporto
│
├── _headers                        # Direttive caching e sicurezza HTTP per hosting statico
├── _redirects                      # Regole di redirect e routing Netlify
├── robots.txt                      # Istruzioni per i crawler dei motori di ricerca
└── sitemap.xml                     # Mappa XML per l'indicizzazione SEO
```

---

## 🎨 Linee Guida e Stile

- **Colori Sociali**:
  - Giallo Virtus: `#ffd100` / Giallo caldo accento: `#f0b800`
  - Blu Virtus: `#0f2a4a` / Blu scuro sfondo: `#081a2e`
  - Neutri: Testo scuro `#1c2530`, sfondi `#ffffff` e `#f8f9fa`, bordi `#e2e8f0`
- **Tipografia**:
  - Titoli: `Barlow Condensed`, sans-serif (pesi 600, 700)
  - Corpo testo: `Inter`, sans-serif (pesi 400, 500, 600)
- **Immagini**:
  - Ottimizzazione in formato moderno `.webp` con fallback `.png` o `.jpg`
  - Attributi `loading="lazy"`, `width` e `height` per evitare layout shift
- **SEO & Social Sharing**:
  - Meta tag Open Graph (`og:title`, `og:image`, `og:description`, `og:url`)
  - Geo Meta Tags per geolocalizzazione (Senago, Solaro, Limbiate, Parco delle Groane)
  - Dati strutturati Schema.org (`BreadcrumbList`, `SportsClub`)

---

## 🚀 Sviluppo Locale e Deploy

### Anteprima Locale
Poiché il sito è composto da file statici, non richiede build o compilazione. Per testare correttamente i percorsi assoluti (`/style.css`, `/images/...`), è consigliato avviare un server HTTP locale dalla radice del progetto:

```powershell
# Opzione 1: Node.js (npx serve)
npx serve .

# Opzione 2: Python 3
python -m http.server 8080
```
Aprire il browser su `http://localhost:3000` (o `http://localhost:8080`).

### Hosting e Pubblicazione
Il sito è configurato per il deployment su piattaforme di hosting statico (es. Netlify):
- `_redirects` gestisce il routing statico, la pagina 404 e l'eventuale reindirizzamento degli URL.
- `_headers` definisce le policy di caching (asset statici con cache estesa, HTML a validazione rapida) e le intestazioni di sicurezza (X-Content-Type-Options, X-Frame-Options, Referrer-Policy).

---

## 🛠️ Manutenzione e Aggiornamento Contenuti

1. **Record Societari**:
   I dati dell'Albo d'Oro sono gestiti in [data/records/records-data.js](file:///c:/Emiliano/virtus-groane/data/records/records-data.js) e caricati dinamicamente dalla pagina [societa-ed-eventi/record-societari.html](file:///c:/Emiliano/virtus-groane/societa-ed-eventi/record-societari.html). Per inserire o correggere un primato, aggiornare l'array dei record nel file JavaScript.
2. **Documenti Istituzionali**:
   I file PDF scaricabili (Statuto, Regolamento, informative) risiedono nella cartella [docs/](file:///c:/Emiliano/virtus-groane/docs/).
3. **Moduli d'Iscrizione e Link Esterni**:
   I link a Golee, ai moduli Google (ordini abbigliamento, segnalazione record) e alle iscrizioni gare (ENDU) sono inseriti direttamente nei rispettivi file HTML tematici.
