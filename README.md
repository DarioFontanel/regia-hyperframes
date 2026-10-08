# regia-hyperframes

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude_Code-skill-d97757)](https://docs.anthropic.com/en/docs/claude-code)
[![HyperFrames](https://img.shields.io/badge/HyperFrames-brief-111111)](https://github.com/heygen-com/hyperframes)

**regia-hyperframes** è una skill per Claude Code che ti permette di decidere la regia di un video prima che [HyperFrames](https://github.com/heygen-com/hyperframes) lo costruisca: messaggio, pubblico, look, movimento, suono e scene. Ogni domanda arriva con opzioni tra cui scegliere e un consiglio motivato, e le decisioni confermate vengono consegnate a HyperFrames come brief già chiuso.

---

## Le cinque fasi

```
materiali ──▶ 9 blocchi di domande ──▶ controllo d'insieme ──▶ foglio di regia ──▶ BRIEF.md + frame.md ──▶ HyperFrames
                      ▲                                              │
                      └──────────── una correzione riapre ───────────┘
```

**1. Apertura** — la skill legge ciò che hai già fornito e cerca i materiali nella cartella di lavoro: loghi, screenshot, dati, un `frame.md` o un `design.md`. Una decisione a cui i materiali rispondono già viene mostrata come chiusa.

**2. Un giro per blocco** — nove blocchi in ordine, ciascuno con le proprie domande. Rispondi a un blocco alla volta; opzioni e consigli di ogni blocco discendono dalle decisioni dei blocchi precedenti.

**3. Controllo d'insieme** — le decisioni vengono rilette tutte insieme per individuare le incompatibilità che nessuna mostrava singolarmente, ad esempio venti secondi di durata con sei scene e voce narrante.

**4. Foglio di regia** — un riepilogo unico di tutte le decisioni, divise tra quelle prese da te e quelle delegate alla skill. Una correzione riapre il foglio, che viene ripresentato fino alla tua conferma.

**5. Consegna** — il foglio confermato diventa un progetto HyperFrames con `BRIEF.md` e `frame.md`. Con questi due file HyperFrames costruisce il video senza porre altre domande di brief.

---

## Formato delle domande

Ogni decisione viene presentata in tre parti: una domanda che chiede una cosa sola, da due a quattro opzioni con un valore concreto ciascuna, e il consiglio della skill con il motivo.

```
## Blocco 6 di 9 · Motion

**6.1 · Ritmo**
Che passo deve avere il movimento del video?

- **A · Calmo** — 72 BPM, un evento ogni battito: ogni schermata resta il tempo di essere letta con agio.
- **B · Deciso** — 96 BPM, un evento ogni battito: il video avanza senza pause e resta leggibile.
- **C · Serrato** — 120 BPM, un evento ogni battito: energia alta, adatta a testi molto brevi.

**Consiglio: B.** Il video dura 30 secondi e spiega un concetto a chi non lo conosce (decisioni 2.1 e 2.4).

---
Come rispondere: numero e lettera (`6.1 A`), un valore tuo, oppure `fai tu` per affidarmi le domande che salti.
```

**Lettera** — scegli una delle opzioni: `6.1 A`.
**Valore tuo** — scrivi una risposta diversa dalle opzioni. Se è generica ("qualcosa di elegante"), la skill la traduce in un valore concreto e ti chiede conferma.
**`fai tu`** — deleghi la decisione: vale il consiglio. Puoi delegare una domanda, un blocco intero o tutto il video.

---

## I nove blocchi

**1 · Idea** — il messaggio in una frase, la domanda a cui il video risponde, la convinzione diffusa che ribalta e i fatti che restano fuori.
**2 · Pubblico e formato** — chi guarda, cosa sa fare dopo il video, dove viene pubblicato, formato, durata e lingua.
**3 · Materiali** — brand, screenshot e dati con la loro fonte, riferimenti visivi.
**4 · Storia** — arco narrativo, immagine di apertura, caso reale, svolta e chiusura.
**5 · Look** — tre direzioni visive a confronto in una pagina HTML, con palette, caratteri e immagine di apertura composti con il messaggio del video.
**6 · Motion** — ritmo, entrate e arresti, passaggi tra scene, movimenti di camera.
**7 · Voce e suono** — voce narrante, testo a schermo, musica, effetti sonori, sottotitoli.
**8 · Scene** — la lista completa delle scene, scritta dalla skill a partire dai blocchi precedenti, da confermare o correggere.
**9 · Lavorazione** — revisione dello storyboard prima della costruzione e grado di autonomia di HyperFrames.

---

## File prodotti

**`regia/<slug>/direzioni.html`** — le tre direzioni visive del blocco 5, con la direzione scelta e il motivo annotati: resta come registro della decisione.
**`videos/<slug>/BRIEF.md`** — intento, materiali, voce e suono, arco narrativo e lista delle scene, nel formato che HyperFrames legge come brief.
**`videos/<slug>/frame.md`** — colori, caratteri, spaziature e regole di movimento della direzione scelta, con i valori esatti.

Al termine la skill mostra i percorsi dei due file e il comando di avvio: `/hyperframes esegui il brief in videos/<slug>`.

---

## Prerequisiti

**Claude Code** — la skill si richiama con uno slash command.

**Node.js** — necessario per la CLI `npx hyperframes`, con cui la skill crea il progetto.

**Skill di HyperFrames** — la skill legge il formato di `BRIEF.md` e `frame.md` dalle skill `hyperframes` e `hyperframes-creative` installate. Per installare il set base:

```bash
npx hyperframes skills update
```

Il workflow `general-video`, usato per la costruzione, viene installato dalla skill durante la consegna.

---

## Installazione

1. Clona la repo — `git clone https://github.com/DarioFontanel/regia-hyperframes.git`
2. Copia la skill nella cartella delle skill utente di Claude Code:

```bash
# macOS / Linux
cp -r regia-hyperframes/skills/* ~/.claude/skills/

# Windows (PowerShell)
Copy-Item -Recurse regia-hyperframes\skills\* $env:USERPROFILE\.claude\skills\
```

Verifica: in Claude Code digita `/regia-hyperframes` — la skill compare tra quelle disponibili.

Per aggiornare: `git pull` e ripeti la copia.

---

## Utilizzo

Avvia la skill indicando l'argomento del video:

```
/regia-hyperframes un video di 30 secondi che spiega come funziona un agente AI
```

La skill si attiva solo con lo slash command. Se hai già materiali di brand, indicane il percorso nel messaggio: i valori che contengono vincolano le opzioni del blocco 5.

---

Designed by **[Dario Fontanel, PhD](https://dariofontanel.com/)**

*Aiuto PMI italiane ad integrare l'intelligenza artificiale per automatizzare i lavori ripetitivi, abbattere i costi e guadagnare tempo per crescere.*

[![Sito](https://img.shields.io/badge/Sito-dariofontanel.com-4285F4?style=flat&logo=googlechrome&logoColor=white)](https://dariofontanel.com/)
[![YouTube](https://img.shields.io/badge/YouTube-FF0000?style=flat&logo=youtube&logoColor=white)](https://www.youtube.com/@dariofontanel)
[![Instagram](https://img.shields.io/badge/Instagram-E4405F?style=flat&logo=instagram&logoColor=white)](https://www.instagram.com/dariofontanel.ai/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI%2BPHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0yMC40NDcgMjAuNDUyaC0zLjU1NHYtNS41NjljMC0xLjMyOC0uMDI3LTMuMDM3LTEuODUyLTMuMDM3LTEuODUzIDAtMi4xMzYgMS40NDUtMi4xMzYgMi45Mzl2NS42NjdIOS4zNTFWOWgzLjQxNHYxLjU2MWguMDQ2Yy40NzctLjkgMS42MzctMS44NSAzLjM3LTEuODUgMy42MDEgMCA0LjI2NyAyLjM3IDQuMjY3IDUuNDU1djYuMjg2ek01LjMzNyA3LjQzM2MtMS4xNDQgMC0yLjA2My0uOTI2LTIuMDYzLTIuMDY1IDAtMS4xMzguOTItMi4wNjMgMi4wNjMtMi4wNjMgMS4xNCAwIDIuMDY0LjkyNSAyLjA2NCAyLjA2MyAwIDEuMTM5LS45MjUgMi4wNjUtMi4wNjQgMi4wNjV6bTEuNzgyIDEzLjAxOUgzLjU1NVY5aDMuNTY0djExLjQ1MnpNMjIuMjI1IDBIMS43NzFDLjc5MiAwIDAgLjc3NCAwIDEuNzI5djIwLjU0MkMwIDIzLjIyNy43OTIgMjQgMS43NzEgMjRoMjAuNDUxQzIzLjIgMjQgMjQgMjMuMjI3IDI0IDIyLjI3MVYxLjcyOUMyNCAuNzc0IDIzLjIgMCAyMi4yMjUgMHoiLz48L3N2Zz4%3D)](https://www.linkedin.com/in/dario-fontanel/)
[![TikTok](https://img.shields.io/badge/TikTok-000000?style=flat&logo=tiktok&logoColor=white)](https://www.tiktok.com/@dario.fontanel)
[![AI Academy](https://img.shields.io/badge/AI_Academy-E7514F?style=flat&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI%2BPHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAzIDEgOWwxMSA2IDktNC45MVYxN2gyVjlMMTIgM3pNNSAxMy4xOFYxN2MwIDEuNjYgMy4xMyAzIDcgM3M3LTEuMzQgNy0zdi0zLjgybC03IDMuODItNy0zLjgyeiIvPjwvc3ZnPg%3D%3D)](https://www.skool.com/ai-academy-2306)

Licenza [MIT](./LICENSE).
