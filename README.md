# Storybook — Design System HUBWeb

Vetrina interattiva dei componenti del design system (`@ui`): permette di vedere, provare e riutilizzare i componenti senza avviare l'applicazione.

## Dove vederlo

Storybook è pubblicato su GitHub Pages:

**https://<utente-o-org>.github.io/hubweb-storybook/**

Si apre dal browser, senza installare nulla. È una vetrina di sola consultazione: modificare i controlli non tocca il codice reale.

## Com'è organizzato

I componenti sono raggruppati nella barra laterale per livello:

- **Atoms** — elementi base (button, chip, tag, input, ...)
- **Molecules** — composizioni (tabs, slider, accordion, select, ...)
- **Organisms** — blocchi complessi (data-table, stepper, dialog, ...)
- **Templates** — layout di pagina

Per ogni componente:

- le **stories** mostrano casi d'uso e varianti;
- il pannello **Controls** (in basso) permette di cambiare le proprietà al volo (severity, dimensioni, testi, ...) e vederne subito l'effetto;
- la scheda **Docs** riassume props ed esempi.

## Come pubblicare / aggiornare (per chi ha accesso)

Lo Storybook viene compilato in locale e caricato su GitHub Pages con un solo comando:

```bash
npm run deploy-storybook
```

Il comando compila lo Storybook (cartella `storybook-static/`) e ne carica **solo** il risultato sul branch `gh-pages` del repo dedicato: il codice sorgente resta su Azure DevOps e `main` non viene toccato. La build è locale, quindi riflette lo stato attuale dei file (anche modifiche non ancora committate).

### Prima configurazione (una volta sola)

1. Creare il repository GitHub `hubweb-storybook` (può restare vuoto).
2. Nello script `deploy-storybook` del `package.json`, sostituire `<utente-o-org>` con l'account/organizzazione reale.
3. Installare lo strumento di pubblicazione:
   ```bash
   npm i -D gh-pages
   ```
4. Lanciare una prima volta `npm run deploy-storybook`: crea da solo il branch `gh-pages` e vi carica lo Storybook.
5. Su GitHub: **Settings → Pages → Deploy from a branch → `gh-pages` / (root)**.

Da qui in poi la pubblicazione è automatica: a ogni `npm run deploy-storybook` il branch viene aggiornato e GitHub Pages si ricarica da solo, senza più toccare le impostazioni.

> Alla prima esecuzione GitHub chiede l'autenticazione: serve un token con permessi sui repository.

## Sviluppo in locale

Per lavorare sui componenti con ricarica automatica (senza pubblicare):

```bash
npm run storybook
```
