# Linee Guida e Istruzioni Operative per Agenti AI - Progetto Virtus Groane

Questo documento definisce il perimetro di autorizzazione, l'architettura tecnica, le convenzioni stilistiche e i requisiti obbligatori di ottimizzazione **SEO & GEO** per chiunque (in particolare agenti AI) effettui modifiche, aggiunte o manutenzioni al sito web istituzionale di **Virtus Groane ASD**.

---

## 1. Ambito di Autorizzazione e Policy Operativa

- **Pieno Accesso**: L'assistente AI ha piena facoltà di leggere, creare e modificare file, nonché eseguire comandi locali (PowerShell, Node.js, server locali) su tutti i file del repository `virtus-groane`.
- **Autonomia di Esecuzione**: Condurre le attività in autonomia dall'analisi al completamento finale, minimizzando le interazioni non necessarie. Richiedere input all'utente solo in caso di requisiti mancanti o scelte di business non deducibili.
- **Integrità Architetturale**: Mantenere l'architettura statica pura (HTML5/CSS3/JS vanilla) senza introdurre framework o dipendenze esterne non necessarie (niente React/Vue, Tailwind, Bootstrap, jQuery o bundler complessi).
- **Risposte Finali Chiare e Sintetiche**: Fornire riscontri concisi, evidenziando le azioni intraprese e includendo i link diretti `file:///` ai file esaminati o modificati.

---

## 2. Panoramica del Progetto: Cosa è Stato Fatto

Il sito attuale nasce dalla completa migrazione e riscrittura di un precedente sito realizzato su piattaforma Wix. L'obiettivo primario raggiunto è stato trasformare un sito lento e frammentato in un portale **statico ad altissime prestazioni**, accessibile, responsive e fortemente ottimizzato per i motori di ricerca e la geolocalizzazione locale.

### Sintesi degli interventi realizzati:
1. **Ristrutturazione dei Contenuti**: Suddivisione logica in sezioni verticali con cartelle dedicate (`/virtus/`, `/info-iscrizioni/`, `/abbigliamento/`, `/societa-ed-eventi/`, `/sostieni-virtus/`), oltre alla Home e alle pagine trasversali (Contatti, English, Privacy Policy, 404).
2. **Architettura Senza Framework**: Nessun costo di rendering client-side; codice HTML5 pulito e semantico servito all'istante, con caricamento asincrono/differito e CSS unificato (`style.css`).
3. **Database Dinamico per i Record Societari**: Implementazione in [societa-ed-eventi/record-societari.html](file:///c:/Emiliano/virtus-groane/societa-ed-eventi/record-societari.html) di un sistema di filtraggio interattivo e grafici storici (Chart.js via CDN), alimentato dall'array strutturato in [data/records/records-data.js](file:///c:/Emiliano/virtus-groane/data/records/records-data.js).
4. **Ottimizzazione Media**: Tutte le immagini sono servite nel formato di nuova generazione `.webp`, mantenendo fallback retrocompatibili (`.png`/`.jpg`), con dimensioni esplicite (`width`/`height`) e `loading="lazy"` per azzerare il Cumulative Layout Shift (CLS).
5. **Configurazione Hosting & Redirect**: File `_redirects` per la gestione automatica dei redirect 301 dal vecchio dominio Wix e per la protezione dei file riservati (blocco cartella `/virtus-non-pubblico/`, file `.xlsx`, `.csv`), unitamente a `_headers` con Content Security Policy (CSP), HSTS e policy di caching rigorose.

---

## 3. Design System & Coerenza Stilistica

Tutte le nuove pagine o le modifiche a quelle esistenti **devono seguire rigorosamente** i token e i pattern stabiliti in [style.css](file:///c:/Emiliano/virtus-groane/style.css):

### 3.1 Variabili CSS (Design Tokens)
```css
:root {
    --bg-primary: #0c0f12;        /* Sfondo principale (scuro/dark mode nativo) */
    --bg-secondary: #141922;      /* Sfondo card, header, sezioni secondarie */
    --bg-tertiary: #1b2230;       /* Sfondo box informativi, callout, hover */
    --color-blue: #1b589b;        /* Blu istituzionale Virtus */
    --color-green: #24b267;       /* Verde accento/azioni primarie/stato attivo */
    --color-blue-light: #2b7ad2;  /* Blu chiaro per accenti/link */
    --color-green-light: #2ecc71; /* Verde brillante per evidenziazioni */
    --text-primary: #ffffff;      /* Testo principale ad alto contrasto */
    --text-secondary: #a0aec0;    /* Testo secondario, sottotitoli, didascalie */
    --text-muted: #718096;        /* Testo disattivato o note a piè di pagina */
    --border-color: rgba(255, 255, 255, 0.08); /* Bordi discreti su fondo scuro */
    --font-title: 'Barlow Condensed', 'Arial Narrow', sans-serif; /* Titoli (bold/uppercase) */
    --font-body: 'Inter', sans-serif;                             /* Corpo testo leggibile */
    --max-width: 1200px;
    --header-height: 80px;
}
```

### 3.2 Tipografia & Regole di Stile
- **Titoli (`<h1>` - `<h6>`)**: Usano `--font-title`, pesi 600 o 700, trasformazione `text-transform: uppercase`, `letter-spacing: 0.05em`. Se un titolo non deve essere tutto maiuscolo, applicare la classe `.nocaps`.
- **Corpo del testo**: Usare `--font-body`, interlinea rilassata (`line-height: 1.6`), contrasto chiaro su scuro.
- **Colori sociali nel testo**: Giallo/arancione per richiami societari (`#ffd100`), verde `--color-green-light` per elementi salienti e successo, blu per bottoni secondari.

### 3.3 Componenti Standard Obbligatori in Ogni Pagina
1. **Accessibilità (Skip Link)**: Subito dopo `<body>`:
   ```html
   <a href="#main-content" class="skip-link" style="position: absolute; top: -9999px; left: -9999px;">Salta al contenuto principale</a>
   ```
2. **Header Fisso & Navigazione**:
   - Menu di navigazione responsive puro CSS (basato su `#menu-toggle` checkbox).
   - Nelle sottopagine in cartella, usare sempre i percorsi relativi verso la radice: `../index.html`, `../virtus.html`, `../logo.webp`, `../style.css?v=1.3`.
   - Sezione attiva evidenziata nel menu con `style="color: var(--color-green-light);"`.
3. **Page Hero Banner con Breadcrumb Visiva**:
   ```html
   <section id="main-content" class="page-hero">
       <div class="container">
           <h1><a href="../sezione-padre.html" class="parent-link">Sezione Padre</a> <span class="parent-separator">/</span> Titolo Pagina</h1>
           <p style="color: var(--text-secondary); margin-top: 0.5rem;">Sottotitolo descrittivo sintetico della pagina</p>
       </div>
   </section>
   ```
4. **Layout Contenuti Interni**:
   ```html
   <section class="internal-layout">
       <div class="container">
           <div class="article-content">
               <!-- Contenuto strutturato: h2, paragrafi, card, liste -->
           </div>
       </div>
   </section>
   ```
5. **Callout / Box Informativi**:
   Usare blocchi con sfondo `--bg-tertiary`, bordo `--border-color` e `border-radius: 8px` per note importanti, avvisi di sicurezza o istruzioni pratiche.
6. **Footer Condiviso**:
   Presente in tutte le pagine, suddiviso in: colonna istituzionale con Codice Fiscale (`04577740964`) e affiliazioni (FIDAL, FITRI, AICS, FIASP, CONI), link rapidi, orari/sedi operative e pulsanti social (Facebook, Instagram, Strava).
7. **Pulsante Flottante WhatsApp**:
   In fondo a ogni pagina, prima della chiusura di `</body>`:
   ```html
   <a href="https://wa.me/393406274022?text=Ciao%20Virtus%20Groane,%20vorrei%20informazioni..." class="whatsapp-float" target="_blank" rel="noopener noreferrer" aria-label="Contatta Virtus Groane su WhatsApp">
       <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" aria-hidden="true"><path d="..."/></svg>
       <span>Scrivici su WhatsApp</span>
   </a>
   ```

---

## 4. Requisiti Obbligatori SEO & GEO (Local Search)

Ogni nuova pagina o modifica a contenuti esistenti **deve integrare la suite completa di metadati SEO e GEO** già standardizzata nel progetto.

### 4.1 Meta Tag Base nel `<head>`
- **`<title>`**: Formula: `[Nome Pagina/Argomento] - [Keyword Contestuale] - Virtus Groane ASD` (lunghezza consigliata: 50-60 caratteri).
- **`<meta name="description">`**: Descrizione accattivante di 130-160 caratteri che includa sempre le keyword dell'argomento e i riferimenti geografici (*Senago, Solaro, Limbiate, Parco delle Groane, Nord-Ovest Milano*).
- **`<link rel="canonical">`**: URL canonico assoluto `https://www.virtusgroane.com/[percorso-pagina].html` (o `https://www.virtusgroane.com/` per la root).
- **Favicon**:
  ```html
  <link rel="icon" type="image/png" sizes="192x192" href="/favicon.png">
  <link rel="shortcut icon" href="/favicon.ico">
  ```

### 4.2 Open Graph Tags (Social Sharing & WhatsApp/Telegram Preview)
```html
<meta property="og:type" content="website">
<meta property="og:url" content="https://www.virtusgroane.com/[percorso-pagina]">
<meta property="og:title" content="[Titolo Ottimizzato] - Virtus Groane ASD">
<meta property="og:description" content="[Descrizione coerente con meta description]">
<meta property="og:image" content="https://www.virtusgroane.com/logo.png">
```

### 4.3 Geo Meta Tags (Geolocalizzazione Obbligatoria)
Per posizionare il club nelle ricerche locali su Google e Bing per l'area nord-ovest di Milano e Brianza, inserire **sempre**:
```html
<!-- Geo Meta Tags (Geolocalizzazione & Local Search) -->
<meta name="geo.region" content="IT-MI">
<meta name="geo.placename" content="Senago, Solaro, Limbiate, Parco delle Groane (Nord-Ovest Milano)">
<meta name="geo.position" content="45.570603;9.126529">
<meta name="ICBM" content="45.570603, 9.126529">
```
*(Se la pagina fa riferimento esclusivo a un impianto specifico, es. Solaro o Limbiate, indicare le coordinate puntuali di quell'impianto già censite nella home page).*

### 4.4 Dati Strutturati Schema.org (JSON-LD)

Ogni pagina **deve contenere** i dati strutturati pertinenti:

1. **BreadcrumbList (Obbligatorio su tutte le sottopagine)**:
   ```html
   <script type="application/ld+json">
   {
     "@context": "https://schema.org",
     "@type": "BreadcrumbList",
     "itemListElement": [
       {
         "@type": "ListItem",
         "position": 1,
         "name": "Home",
         "item": "https://www.virtusgroane.com/"
       },
       {
         "@type": "ListItem",
         "position": 2,
         "name": "Sezione Padre",
         "item": "https://www.virtusgroane.com/sezione-padre.html"
       },
       {
         "@type": "ListItem",
         "position": 3,
         "name": "Nome Pagina Corrente",
         "item": "https://www.virtusgroane.com/sezione-padre/nome-pagina.html"
       }
     ]
   }
   </script>
   ```

2. **Schema Specializzati di Pagina**:
   - **Home Page**: Include il blocco esaustivo `@type: "SportsClub"` con `foundingDate: "1978"`, `taxID: "04577740964"`, sedi geografiche `location` (Senago, Solaro, Limbiate), affiliazioni federali `memberOf` (FIDAL, FITRI, AICS, CONI), e `areaServed` estesa a tutti i comuni del bacino (Senago, Solaro, Limbiate, Cesate, Ceriano Laghetto, Garbagnate Milanese, Paderno Dugnano, Varedo, Bovisio Masciago, Cogliate).
   - **Eventi (`/societa-ed-eventi/`)**: Usare `@type: "SportsEvent"` o `@type: "Event"` indicando date, luoghi, organizzatore e modalità di partecipazione.
   - **Rassegne / Documenti**: Usare `@type: "CollectionPage"` o `@type: "AboutPage"` citando l'entità principale `mainEntity: { "@type": "SportsClub", ... }`.

### 4.5 Aggiornamento di `sitemap.xml` e `robots.txt`
- Quando viene **aggiunta o rinominata una pagina**, aggiornare immediatamente [sitemap.xml](file:///c:/Emiliano/virtus-groane/sitemap.xml):
  - Inserire l'elemento `<url>` con `<loc>`, `<lastmod>` (data ISO corrente YYYY-MM-DD), `<changefreq>` e `<priority>` proporzionata (1.0 Home, 0.8-0.9 sezioni primarie, 0.6-0.7 pagine interne).
- Rispettare [robots.txt](file:///c:/Emiliano/virtus-groane/robots.txt): le cartelle riservate (es. `/virtus-non-pubblico/`, `/data/`) e la pagina `404.html` devono rimanere escluse dal crawling.

---

## 5. Checklist per Ogni Intervento dell'Agente AI

Prima di considerare conclusa qualsiasi modifica o aggiunta al sito:
- [ ] Il markup rispetta la semantica HTML5 (`<main>`, `<article>`, `<header>`, `<footer>`, `<section>`).
- [ ] I percorsi relativi di fogli di stile, immagini e link sono corretti per la profondità della directory (`../` per sottopagine in cartella).
- [ ] Sono presenti i font ufficiali Google Fonts (`Barlow Condensed` e `Inter`) con `rel="preconnect"`.
- [ ] Sono presenti tutti i meta tag: `<title>`, `<meta name="description">`, canonical, Open Graph e **Geo Meta Tags**.
- [ ] È presente il blocco Schema.org JSON-LD con la `BreadcrumbList` corrispondente.
- [ ] Le nuove immagini sono fornite in formato `.webp` con attributi `loading="lazy"`, `width`, `height` e `alt` descrittivo.
- [ ] In caso di nuova pagina, è stato inserito il relativo link nei menu a tendina (`header`) e nel `footer` di tutte le pagine collegate.
- [ ] È stato aggiornato [sitemap.xml](file:///c:/Emiliano/virtus-groane/sitemap.xml) con il nuovo URL e la data odierna.
- [ ] In caso di percorsi eliminati o rinominati, è stata creata la corrispondente regola di redirect 301 in [_redirects](file:///c:/Emiliano/virtus-groane/_redirects).
