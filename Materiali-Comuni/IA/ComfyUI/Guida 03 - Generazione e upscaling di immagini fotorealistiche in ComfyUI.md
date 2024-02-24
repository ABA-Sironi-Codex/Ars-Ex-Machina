---
title: Guida 03 - Generazione e upscaling di immagini fotorealistiche in ComfyUI
data: Venerdì 23/02/2024
tags:
  - ComfyUI
  - IntelligenzaArtificiale
  - Dispense
---

```table-of-contents
title: 
style: nestedList # TOC style (nestedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
```

---

## Prima di cominciare

Questa guida è un supporto alla didattica frontale e non è strutturata per offrire un percorso completo *tout court*.

La guida assume che abbiate già installato ComfyUI o abbiate accesso ad una installazione in *cloud* e ne conosciate il funzionamento base.

Il *workflow* d'esempio è una variazione creata dal prof. Davide Riboli a partire da quello pubblicamente distribuito da Olivio Sarikas, attraverso il sito [OpenArt.ai](https://openart.ai/).

[Scarica il workflow](workflow.zip)

---

## Checkpoint, parametri e prompt

Per realizzare gli esempi acclusi è stata utilizzata la versione 5.1 di *RealisticVision*, ma su [Civitai](https://civitai.com/models/4201?modelVersionId=130090) è già disponibile la 6beta. Se siete particolarmente interessati alla creazione di immagini fotorealistiche, sperimentate con tutte le versioni disponibili.

Si raccomanda la lettura delle note di rilascio di *tutti* i modelli *RealisticVision* sulla [pagina ufficiale Hugging Face](https://huggingface.co/collections/SG161222/realistic-vision-sd15-656daddd8a37acfa3f30cf53), dove sono (quasi sempre) indicati anche i modelli VAE raccomandati.

Le note tecniche relative al modello 6beta riportano queste dimensioni ottimali:

- Face Portrait: 896x896  
- Portrait: 896x896, 768x1024  
- Half Body: 768x1024, 640x1152  
- Full Body: 896x896, 768x1024, 640x1152, 1024x768, 1152x640

Mentre per le versioni precedenti non sono indicate risoluzioni particolari e bisogna fare riferimento agli esempi pubblicati in Civitai o altrove.

### Prompt positivo

Lo schema di massima è:

```
RAW photo, *descrizione dettagliata del soggetto che volete ottenere*, 8k uhd, dslr, soft lighting, high quality, film grain, Fujifilm XT3
```

### Prompt negativo

La gestione dei *prompt* negativi per immagini che comportino la generazione di anatomie umane e/o animali può essere un problema e non è detto che funzioni sempre. Quelli che seguono sono due buoni *template* di massima che potrebbero comunque avere bisogno di aggiustamenti in funzione del risultato cercato:

```
(deformed iris, deformed pupils, semi-realistic, cgi, 3d, render, sketch, cartoon, drawing, anime), text, cropped, out of frame, worst quality, low quality, jpeg artifacts, ugly, duplicate, morbid, mutilated, extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, deformed, blurry, dehydrated, bad anatomy, bad proportions, extra limbs, cloned face, disfigured, gross proportions, malformed limbs, missing arms, missing legs, extra arms, extra legs, fused fingers, too many fingers, long neck, UnrealisticDream
```

```
(deformed iris, deformed pupils, semi-realistic, cgi, 3d, render, sketch, cartoon, drawing, anime, mutated hands and fingers:1.4), (deformed, distorted, disfigured:1.3), poorly drawn, bad anatomy, wrong anatomy, extra limb, missing limb, floating limbs, disconnected limbs, mutation, mutated, ugly, disgusting, amputation, UnrealisticDream 
```

In entrambi i casi, l'ultimo termine richiama un *embedding* di genere *fastnegative*. I migliori con cui lavorare, al momento, sono:

- [FastNegativeV2](https://civitai.com/models/71961?modelVersionId=94057) (*trigger in prompt*: `FastNegativeV2`)
- [BadDream](https://civitai.com/models/72437/baddream-unrealisticdream-negative-embeddings) (*trigger in prompt*: `BadDream`)
- [UnrealisticDream](https://civitai.com/models/72437?modelVersionId=77173) (*trigger in prompt*: `UnrealisticDream`)
- [Negative Hand](https://civitai.com/models/56519/negativehand-negative-embedding) (*trigger in prompt*: `negative_hand` oppure `negative_hand-neg`)

Si possono usare sia insieme che da soli e non esistono formule assolute e sempre valide. La sperimentazione personale è la sola strada aperta. Ricordate che, oltre a quelli citati, esistono decine di altri *negative embedding* specificatamente riferiti a particolari *checkpoint*.

### Altri parametri

Anche in questo caso riportiamo i consigliati, ma la sperimentazione personale potrebbe condurre a "ricette" molto diverse e altrettanto efficaci.

- Steps: 25
- Size: 640x960
- Sampler: DPM++ SDE Karras
- CFG scale: 7
- Denoising strength: 0.35

---

## Esempi di output

![[Bn_01.webp]] ![[Bn_02.webp]] ![[Bn_03.webp]]

![[Bn_04.webp]] ![[Bn_05.webp]] ![[Bn_06.webp]]

![[Clr_01.webp]] ![[Clr_02.webp]]![[Clr_03.webp]]

![[Clr_04.webp]] ![[Clr_05.webp]] ![[Clr_06.webp]]

![[Clr_07.webp]] ![[Clr_08.webp]]