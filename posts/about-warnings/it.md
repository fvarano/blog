---
title: "About Warnings"
date: "2026-02-16"
language: "it"
---

Un warning è un tipo di segnalazione che può arrivare da diversi strumenti: linter, compilatori, bundler, o altri tool di analisi del codice.

A differenza di un errore, non blocca il flusso di lavoro -- la build continua anche in presenza di warning -- ed è possibile arrivare a del codice "funzionante" anche ignorandolo.

**Questa caratteristica li rende facili da trascurare, ma può portare a conseguenze serie nel tempo.**

## Perché ignorare i warning è pericoloso

Quando ignoriamo sistematicamente i warning, accadono tre cose:

1. **Perdiamo comprensione**: saltiamo l'opportunità di capire un potenziale problema nel nostro codice
2. **Generiamo diffidenza**: il sistema di warning perde credibilità e utilità
3. **Creiamo rumore**: un muro di warning rende impossibile accorgersi quando ne nasce uno nuovo o quando uno viene risolto

## Come gestire i warning correttamente

### Comprendere prima di agire

Il primo passo è capire cosa ci sta dicendo il tool. Qual è la ragione dietro quel warning? Perché quella pratica è sconsigliata? A quali problemi può portare? Solo dopo aver compreso il contesto ha senso decidere come procedere.

Nella maggior parte dei casi, la soluzione migliore è seguire le indicazioni della documentazione del tool che ha emesso il warning.

### Se è un falso positivo

Prima di tutto: **ne siamo davvero sicuri?**

Se dopo un'analisi attenta confermiamo che si tratta di un falso positivo:

1. Disattivare il warning **localmente** sulla specifica porzione di codice (mai a livello di progetto)
2. Documentare con un commento la motivazione per cui è considerato un falso positivo in quel caso specifico
3. Se la stessa situazione si ripete in molti punti del codice con la stessa motivazione (sintomo di un problema sistemico), considerare la creazione di un componente o funzione atomica centralizzata che incapsuli il codice con il warning disattivato e la relativa documentazione

### Se è un problema sistemico

Quando un warning o errore è sistemico del progetto e non risolvibile a livello di codice applicativo, ancora una volta: **ne siamo davvero sicuri?**

Se la risposta è sì:

1. Valutare una soppressione a livello di build, ma **solo per i warning strettamente necessari**
2. Schedulare una rivalutazione periodica di questa decisione perché:
   - È probabile che la soppressione non sia più necessaria dopo un aggiornamento delle dipendenze interessate
   - Le dipendenze potrebbero essere obsolete e sostituibili con alternative moderne (es: Babel → [Oxc](https://oxc.rs), [esbuild](https://esbuild.github.io/)) o non più necessarie (es: Sass → [CSS nativo](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/Nesting_selector) ([baseline](https://caniuse.com/css-nesting)))

## Conclusione

Una build pulita è indice di un progetto sotto controllo. I warning, se ascoltati, possono aiutarci a intercettare problemi prima che diventino critici e a mantenere il codice più comprensibile nel tempo.
