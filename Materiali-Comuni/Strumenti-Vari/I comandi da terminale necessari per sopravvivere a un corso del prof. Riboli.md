---
title: I comandi da terminale necessari per sopravvivere a un corso del prof. Riboli
data: Giovedì 22/02/2024
tags:
  - Dispense
  - Git
---

## Abstract

Questa veloce dispensa riepiloga i pochi comandi da terminale che è opportuno conoscere bene per seguire uno i corsi ABA Sironi tenuti dal prof. Riboli. 

---

## Indice

```table-of-contents
title: 
style: nestedList # TOC style (nestedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
```

---

### Cd

Significa *change directory* e permette di spostarsi tra le cartelle del computer. Se seguito da due punti fa risalire di un livello. Se scritto da solo, torna alla *directory* dell'utente.

```bash
cd ComfyUI //entra nella cartella ComfyUI

cd .. //risale di un livello rispetto a quello in cui ci si trova

cd //torna alla cartella utente
```

---

### Dir

Elenca i contenuti di una *directory*.

```bash
dir
```

---

### Git Clone

Il comando può essere lanciato solo dopo avere installato Git  e clona in locale un repository di cui si conosce l'URL. Nell'esempio qui sotto, il comando clona in locale il repository ufficiale di ComfyUI.

```bash
git clone https://github.com/comfyanonymous/ComfyUI
```

---

### Git Pull

Il comando può essere lanciato solo dall'interno della *directory* di un *repository* clonato e scarica dal repository originale tutti gli ultimi aggiornamenti. Ad esempio, se lanciato dalla copia in locale del repository di ComfyUI, aggiorna lo script all'ultima versione disponibile.

```bash
git pull
```

---

### Git Push

Il comando può essere lanciato solo verso un *repository* online su cui si posseggano i privilegi di scrittura e carica tutti gli ultimi aggiornamenti fatti in locale. Ad esempio, se lanciato dalla cartella di questo vault e solo dal computer del prof. Riboli, aggiorna la versione *online* delle dispense.

```bash
git push
```

---

### Homebrew (solo Mac)


I comandi base sono facili:

- `brew install nomepacchetto` 
- `brew remove nomepacchetto` 
 - `brew search nomepacchetto`
 
L'installazione e la gestione generale richiedono attenzione. Ecco alcuni fondamentali riferimenti sul web, da prima di mettersi al lavoro almeno fino a quando vi considererete *absolute beginner*...

- [Homebrew home page](https://brew.sh/) | contiene subito il comando di prima installazione.
- [Homebrew installation](https://docs.brew.sh/Installation) | informazioni dettagliate sulla procedura di installazione.
- [Homebrew commands](https://docs.brew.sh/Manpage#commands) | Tutti i comandi *brew*, dettagliatamente spiegati.
- [How to install and use homebrew on Mac](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-homebrew-on-macos) | Una guida Digital Ocean del 2021, molto ben fatta.

---

### Chocolatey (solo PC)

Valgono le medesime raccomandazioni per Brew. Una volta installato, i comandi base sono piuttosto semplici:

- `choco search  nomepacchetto`
- `choco install nomepacchetto`
- `choco uninstall nomepacchetto`

Il riferimento web per qualsiasi operazione più complessa e per le procedure di installazione è il sito ufficiale:

- [Chocolatey](https://chocolatey.org/)

---

### Bandit The Game (un modo divertente per diventare bravi)

[Bandit the Game](https://overthewire.org/wargames/bandit/) è un modo molto divertente per familiarizzare con l'uso del terminale.

Il primo comando per collegarsi è:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Se poi volete giocare sporco:

- [BtG Walktrough 01](https://home.adelphi.edu/~ni21347/cybersecgames/OverTheWire/Bandit/index.html)
- [BtG Walktrough 02](https://mayadevbe.me/posts/overthewire/bandit/overview/)

---
