# Consegna a HyperFrames

Il foglio di regia confermato diventa due file nella radice di un progetto HyperFrames: `BRIEF.md` e `frame.md`. HyperFrames li riconosce da solo — con un `BRIEF.md` presente esegue senza fare domande di brief, e legge `frame.md` come verità di brand.

La forma dei due file la definisce HyperFrames. Leggila dalle skill installate prima di scrivere:

- `hyperframes` → `references/brief-format.md`: chiavi del frontmatter e sezioni di `BRIEF.md`.
- `hyperframes-creative` → `references/design-spec.md`, più un `frame-presets/<nome>/FRAME.md` aperto come esempio di struttura: frontmatter di token, corpo in prosa.

## 1. Progetto

Scegli uno slug kebab-case dal messaggio. Installa il workflow con `npx hyperframes skills update general-video`, poi crea il progetto col comando di init che quella skill riporta al § 2. L'init viene prima di ogni file: rifiuta una cartella non vuota.

Il workflow è `general-video` perché costruisce dal brief e legge `frame.md` così com'è.

## 2. `BRIEF.md`

Frontmatter: `workflow: general-video`, `flow` e `storyboard` dal blocco 9, `message` dal blocco 1, `destination`, `aspect`, `language`, `audience`, `length` dal blocco 2.

| Sezione             | Contiene                                                                                                    |
| ------------------- | ----------------------------------------------------------------------------------------------------------- |
| `## Intent`         | Blocchi 1 e 2 in prosa: domanda, aggancio, chi guarda e cosa crede, cosa sa fare dopo. Le parole dell'utente dove contano. |
| `## Assets`         | Blocco 3, una riga per file: `percorso — cos'è, dove serve`.                                                |
| `## Customizations` | Blocco 7: voce, musica, effetti, sottotitoli, ognuno con abbastanza dettaglio per essere eseguito.          |
| `## Notes`          | Arco del blocco 4; la lista scene del blocco 8 per intero, sotto `### Scene`; tagli, nomi, effetti fuori; l'elenco delle decisioni *delegate*. |

Apri `### Scene` con questa riga: scene, ordine, durate e consegne sono confermate, lo storyboard le sviluppa.

## 3. `frame.md`

Nome sempre minuscolo. Il frontmatter porta i valori esatti della direzione vincente del blocco 5: `colors` (ruolo → hex), `typography` (ruolo → famiglia, peso, misura), `spacing`, e in `components` la cornice se c'è. Il corpo in prosa:

- `## Overview`: il look in tre righe e l'idea che serve.
- `## Composition Rules`, con `### Do` e `### Don't`: cosa si disegna, cosa resta fuori.
- `## Motion`: il blocco 6 scritto come regole coi suoi numeri — griglia di tempo, frame di entrata, tipo di arresto, quiete, passaggi tra scene, camera.

## 4. Verifica

Scorri il foglio di regia decisione per decisione: ognuna compare in uno dei due file con lo stesso valore. Ogni hex e ogni carattere di `frame.md` coincide con la direzione segnata in `direzioni.html`.

## 5. Lancio

Mostra i percorsi dei due file e la riga di lancio:

```
/hyperframes esegui il brief in videos/<slug>
```

Se l'utente dice di partire, invoca tu la skill `hyperframes` su quel progetto.
