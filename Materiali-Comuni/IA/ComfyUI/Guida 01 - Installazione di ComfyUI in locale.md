---
title: Guida 01 - Installazione di ComfyUI in locale
data: Mercoledì 01/03/2024
tags:
  - ComfyUI
  - IntelligenzaArtificiale
  - Dispense
---

## Abstract

[ComfyUI](https://github.com/comfyanonymous/ComfyUI) è la più diffusa interfaccia *open source* per la generazione di immagini e video con modelli [StableDiffusion](https://stability.ai). In questa guida vediamo come installarla sotto Linux, Macintosh e Windows.

---

## Indice dei contenuti

```table-of-contents
title: 
style: nestedList # TOC style (nestedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
```

---

> [!Warning] Attenzione!
> - L'ultima data di aggiornamento di questo testo è *Martedì 20 feb. 2024*. Se consultate la guida a più di tre mesi di distanza, controllate sui siti ufficiali (vedi paragrafo "Siti di riferimento") che i passaggi e i comandi siano ancora corretti.

> [!tldr] Prerequisiti
> - La guida presuppone una certa familiarità coi comandi da terminale.

---

## Windows - Versione portatile

Sul *repository* ufficiale ComfyUI è disponibile una versione portatile che contiene tutto il  necessario per lavorare subito, senza dover installare nulla. Logicamente, questa è la versione consigliata per chi è alle primissime armi e non ha familiarità col *prompt* dei comandi.

Questa versione funziona anche con macchine sprovviste di GPU, sebbene questo renda il processo di generazione davvero lentissimo.  

- [Link diretto (avvia lo scaricamento della versione più aggiornata)](https://github.com/comfyanonymous/ComfyUI/releases/download/latest/ComfyUI_windows_portable_nvidia_cu121_or_cpu.7z);
- [Link alla pagina delle release](https://github.com/comfyanonymous/ComfyUI/releases).

Terminato il download, scompattate l'archivio .zip in una qualsiasi directory del computer. Al  termine della procedura di estrazione, sarà stata generata una cartella *ComfyUI_windows_portable* con vari file e cartelle al suo interno. 

Doppio clic sul file *run_nvidia_gpu.bat* se avete un computer dotato di GPU Nvidia ragionevolmente aggiornata oppure su *run_cpu.bat* se ne siete sprovvisti. 

Si aprirà un *prompt* di comando che a sua volta avvierà ComfyUI. Solo al primo avvio, lo script potrebbe avere bisogno di scaricare diversi gigabyte dalla rete. Al termine della procedura di avvio si aprirà una finestra nel vostro browser di default con ComfyUI pronto all'uso.

---

## Linux e Windows con GPU Nvidia - Installazione con GIT

Può apparire come la strada più difficoltosa, ma è quella giusta, proprio perché richiede attenzione ai particolari e familiarità con l'uso del terminale. Due cose con cui, chi si appresta a lavorare con le Intelligenze Artificiali deve prendere confidenza e prima o poi, bisogna pur cominciare...

Il primo comando clona il *repository* ufficiale. Perché funzioni, dovete avere installato [Git](https://git-scm.com/). Gli utenti Linux di solito ce l'hanno già o sanno comunque come fare. Gli utenti Windows possono [scaricarlo](https://git-scm.com/downloads) oppure lavorare con [Chocolatey](https://chocolatey.org/).

```bash
git clone https://github.com/comfyanonymous/ComfyUI
```

Ora entriamo nella *directory*:

```bash
cd ComfyUI
```

E cominciamo a installare il necessario. Lo *script* dovrà recuperare giga e giga di dati, quindi non abbiate fretta, non date fastidio al computer mentre lavora e assicuratevi di lanciarlo solo se avete una connessione stabile e veloce. Non toccate il terminale sino a quando la procedura non è finita.

Con GPU Nvidia, la prima cosa da fare è recuperare [PyTorch](https://pytorch.org/vision/stable/index.html). Consiglio di lavorare con la versione stabile.

```python
pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu121
```

Le *Nightly Release* sono per gli amanti del rischio. Probabilmente più veloci, ma certamente più instabili. Se vi piace l'azzardo, invece del comando precedente, date questo.

```python
pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu121
```

Se qualcosa non dovesse funzionare, potete disinstallare la *Nightly* con questo comando.

```python
pip uninstall torch
```

Al termine della installazione di PyTorch vanno installate tutte le dipendenze. Di nuovo, il download potrebbe essere piuttosto lungo.

```python
pip install -r requirements.txt
```

Il più è fatto e ora dovrebbe essere possibile lanciare ComfyUI.

```python
python main.py
```

---

## Linux con GPU AMD ROCm compatibili

Più o meno tutto come sopra, ma i comandi per PyTorch cambiano. Ecco la sequenza.

```bash
git clone https://github.com/comfyanonymous/ComfyUI && cd ComfyUI
```

```python
python -m pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/rocm5.7 -r requirements.txt
```

Oppure questo, per ROCm 6.0.

```python
python -m pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/rocm6.0 -r requirements.txt
```

Finito! Questo per l'avvio.

```python
python main.py
```

---

## Macintosh M1 e M2 - Installazione con GIT

Per prima cosa, controllate la compatibilità. Dovete avere un Mac M1 o M2 e la versione minima del sistema operativo deve essere MacOS 12.3. Se siete certi di avere le carte in regola, cominciamo installando [Homebrew](https://brew.sh/). 

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

> [!Warning] Attenzione!
> - Perché Homebrew funzioni correttamente deve essere aggiunto al PATH. Non è una operazione semplicissima, perché i passaggi si differenziano in funzione del fatto che usiate Bash o Zsh. La rete è piena di ottimi tutorial e guide in merito, ma si consigli in particolare la lettura di [questo articolo su Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-homebrew-on-macos) che spiega molto bene la questione Bash/Zsh, questa [discussione su StackOverFlow](https://stackoverflow.com/questions/35677031/adding-homebrew-to-path/76720643#76720643), dove sono fornite diverse soluzioni alternative e [anche questa](https://stackoverflow.com/questions/10343834/how-to-modify-path-for-homebrew).

Al termine della installazione è necessario controllare se ci sono parti del sistema che vanno aggiornate. Il comando è molto semplice.

```bash
brew doctor
```

Se la risposta è `Your system is ready to brew.` possiamo andare avanti. Altrimenti eseguite prima tutti gli aggiornamenti richiesti. Siamo pronti a installare tutti gli strumenti necessari (compreso Git) con:

```bash
brew install cmake protobuf rust python@3.10 git wget
```

Al termine di ogni procedura e con Git installato, possiamo clonare in locale il *repository* di ComfyUI.

```bash
git clone https://github.com/comfyanonymous/ComfyUI
```

Da questo momento, i passi sono quasi gli stessi della installazione base Linux/Win. Entriamo col terminale nella *directory* di ComfyUI. Il percorso dipende da dove avete clonato lo *script*.

```bash
cd IL-PERCORSO-ALLA-CARTELLA-DI/ComfyUI
```

Creiamo un *Virtual Environment* nella cartella con:

```python
python -m venv venv
```

Entriamo nel *Virtual Environment* e installiamo PyTorch.

```python
./venv/bin/pip install torch torchvision torchaudio
```

Terminiamo l'installazione aggiungendo le necessarie dipendenze.

```python
./venv/bin/pip install -r requirements.txt
```

Finito! Verificate che tutto funzioni, avviando ComfyUI con:

```python
./venv/bin/python main.py
```


## Macintosh, la via del Male

Per i computer Apple Macintosh non esiste una versione portatile, come per Windows, ma su diversi forum di settore si parla molto di [Pinokio](https://pinokio.computer/), un sistema costruito come un *browser* che permette di installare diverse interfacce per StableDiffusion, compresa ComfyUI.

Di solito questi "accrocchi" non sono mai una buona idea, ma se funziona...

---

## Aggiornamenti

Per tenere aggiornata qualsiasi installazione costruita con Git, indipendentemente dal sistema operativo, è sufficiente entrare nella cartella ComfyUI e lanciare il comando:

```bash
git pull
```

Per tenere aggiornata la versione Windows portatile, fate riferimento agli *script* che trovate nella cartella *update*.