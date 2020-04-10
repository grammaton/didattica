# Setup MacOS

Questa guida ha lo scopo di preparare il proprio ambiente informatico installando
passo passo i software consigliati per lo **studio** delle _tecnologie musicali_,
la _musica elettronica_ e la _computer music_.

Tutti gli articoli presenti nelle pagine di questo sito fanno riferimento
all'utilizzo di [free-software](https://en.wikipedia.org/wiki/Free_software) e
[open-source](https://en.wikipedia.org/wiki/Open_source).

> **Support:** Data la possibilità di eventuali problematiche nell'installazione
di software su macchine specifiche, qualsiasi segnalazione e contributo alla
presente guida sarà di enorme utilità.

## Lista dei software consigliati

La presente guida illustra, preferibilmente e dove possibile, l'utilizzo del
sistema operativo e delle applicazioni attraverso il **Terminale**.

[Qui una buona guida introduttiva all'utilizzo del computer mediante **Terminale** \(ENG\)](https://www.learnenough.com/command-line-tutorial/basics).

* Editor di testo: [**Atom**](http://atom.io)
* Stesura testi ed impaginazione: [**LaTeX**](http://www.tug.org/mactex/index.html)
* Scrittura musicale ed impaginazione partiture: [**LilyPond**](http://lilypond.org/introduction.html)
* DSP \(_Digital Signal Processing_\): [**Faust**](http://faust.grame.fr)
* Analisi dei segnali: [**Octave**](https://www.gnu.org/software/octave/)
* Computer Music: [**CSound**](https://csound.com), [**SuperCollider**](https://supercollider.github.io), [**PureData**](http://puredata.info)
* DAW: [**Reaper**](https://www.reaper.fm)

## Background Operativo

Prima di procedere all'installazione di software aggiuntivi, il sistema operativo
MacOS ha bisogno di essere equipaggiato con sistemi che lo rendano pronto o
facilmente preparabile ad accettare sistemi di sviluppo open-source.

Il primo passo è controllare che ci siano installati sulla macchina i
`command line tools` attraverso il terminale:

```bash
xcode-select --install
```

Nel caso questi siano già presenti nel sistema otterremo in risposta il seguente
errore: `xcode-select: error: command line tools are already installed, use
"Software Update" to install updates` il che significa semplicemente che se si
mantiene aggiornata la macchina con gli strumenti offerti normalmente dal
sistema operativo, anche i `command line tools` si aggiornano di conseguenza.
Se altrimenti non risultassero presenti la procedura proseguirebbe con il
download dei tools e la successiva schermata di installazione.

Al termine dell'installazione dei `command line tools` si può procedere
all'installazione di [**Homebrew**](https://brew.sh), un sistema di gestione di
pacchetti aggiuntivi al sistema operativo. La cosa non deve spaventare, il sistema
MacOS è basato su tecnologia [**UNIX**](https://en.wikipedia.org/wiki/Unix),
che come accade per [**Linux**](https://en.wikipedia.org/wiki/Linux), può
scendere ad un livello di capillarità molto elevato, se si conoscono i luoghi e
gli oggetti che si stanno posizionando. [**Homebrew**](https://brew.sh) fa quello
che deve fare per offrirci i pacchetti di cui abbiamo bisogno in maniera piuttosto
pulita ed educata.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

Il software risponde dichiarando che andrà ad installare pacchetti in alcune
posizioni specifiche, si preme **RETURN** e passa la paura.

Con il passare degli anni, questioni legate alla sicurezza informatica, alla
tipologia di utilizzatore medio, il sistema operativo Mac è diventato discretamente
più rigido e bloccato, al punto da rendere operazioni di sviluppo software più
articolate che in passato. Di seguito una serie di script che personalizzano
il sistema operativo che io considero necessari per un utilizzo informatico serio.

attiva ed abilita l'opzione _ovunque_ per le applicazioni scaricate, nelle preferenze
di sistema
```bash
sudo spctl --master-disable
```

disattiva il pannello “Are you sure you want to open this application?” che appare
ogni volta che si apre un'applicazione scaricata da web.

```bash
defaults write com.apple.LaunchServices LSQuarantine -bool false
```

disattiva il maiuscolo automatico, funzione molto scomoda nella programmazione testuale.

```bash
defaults write NSGlobalDomain NSAutomaticCapitalizationEnabled -bool false
```

## Atom

Atom può essere scaricato direttamente dalla pagina ufficiale [atom.io](https://atom.io). Come dichiarato dagli sviluppatori, è un potente e versatile editor di testo, _hackable_. Il che significa tante cose, la più importante è che non è solo un editor di testo. Diventa altre cose, agendo nei posti giusti.

La sua struttura è a pacchetti i quali si possono aggiungere e togliere con estrema semplicità. Ci sono due modi per farlo, il primo è attraverso l'interfaccia grafica, entrando nei `settings` e poi in `install`, il secondo attraverso riga di comando digitando `apm install` e poi il nome del pacchetto che si vuole installare.

Ci sono buone ragioni per usare il comando da terminale, il primo è che se sapete già cosa volete, è un po' come fare la lista della spesa, uno dopo l'altro inserite i pacchetti che volete aggiungere

Il pacchetto `counter` aggiunge un contatore di caratteri, parole e righe in fondo alla schermata di Atom, `language-faust` aggiunge semplicemente il riconoscimento del codice testuale di Faust.

### LaTeX \(MacTeX\)

La distribuzione per Mac OS di LaTeX è scaricabile da [qui](http://www.tug.org/mactex/index.html). L'installazione è completa di editor **TeXShop** ed altre utilità che verranno approfondite in seguito.

Si può aggiungere un po' di LaTeX dentro Atom per il nostro piacere di avere lo stesso ambiente di scrittura per tutti i nostri linguaggi testuali preferiti.

Atom è già predisposto per riconoscere il linguaggio `.tex` ma se si vuole aggiungere la possibilità di compilare documenti LaTeX direttamente da Atom, con funzioni di automazione come per esempio la compilazione al salvataggio del file, basta aggiungere il pacchetto `atom-latex`

### Faust

Per l'installazione di [**Faust**](http://faust.grame.fr) sono necessari i seguenti pacchetti

* [cmake](https://cmake.org)
* [pkgconfig](https://www.freedesktop.org/wiki/Software/pkg-config/)
* [qt](https://www.qt.io)
* [libsndfile](http://www.mega-nerd.com/libsndfile/)

che andremo ad installare con Homebrew

La libreria `qt` va collegata a mano, per farlo è necessario chiedere a Homebrew di farlo

Ottenuti i pacchetti necessari, si può procedere a scaricare da GitHub il codice sorgente di [Faust](https://github.com/grame-cncm/faust) ed installarlo attraverso i seguenti comandi eseguiti una riga alla volta.

Il comando finale, `sudo make install` chiama il programma `sudo` che abilita l'esecuzione del comando successivo `make install` nella modalità **superuser**, **s**-uper **u**-ser **do**. Il la modalità superuser necessita dell'inserimento della password di sistema che verrà digitata dentro la finestra di terminale. È importante notare che il terminale ovviamente non mostrerà i caratteri immessi, quindi al termine dell'immissione della password premere `RETURN` come consueto.

Il comando `make` è diviso in due fasi, la seconda appena illustrata si limita ad installare ciò che `make` precedentemente ha compilato e preparato per l'installazione. Il processo di `make` da codice sorgente può essere piuttosto lungo, dipende dalla potenza della macchina su cui si sta operando e dalla complessità del codice sorgente che si sta compilando.

Se volete sapere quanti danni potete fare in modalità _superuser_ non vi resta che leggere il manuale digitando `man sudo`. `man` è il programma che apre la pagina del manuale di ogni buon comando. Dentro al manuale si avanza una riga per volta premendo `RETURN`, una pagina per volta premendo `SPACE`, si esce automaticamente una volta raggiunta la fine oppure prematuramente premendo `Q`.

### Csound

Lo scopo di questa guida è portarvi ad utilizzare Atom come [IDE](https://en.wikipedia.org/wiki/Integrated_development_environment) per Csound in modo da avere un ambiente integrato per diversi scopi.

Homebrew al termine di alcune installazioni suggerisce come comportarsi nel caso si vogliano collegare tra loro pacchetti o programmi specifici. È il caso di Csound, per il quale Homebrew stampa:

Ci sono diversi modi automaci in terminale per aggiungere una stringa in coda ad un file, ma per gli scopi di questa prima guida introduttiva andremo ad aggiungere manualmente il puntamento suggerito nel file indicato

in Atom aggiungere le seguente riga, salvare e chiudere.

Per il passo successivo, è necessario avere **XCode** completo ed installato sulla propria macchina. Per installarlo è sufficiente lanciare il download attraverso l'[App Store](https://apps.apple.com/it/app/xcode/id497799835?l=en&mt=12).

Dopo aver installato Xcode può essere necessario impostare la giusta versione dei `command line tools` all'interno delle preferenze di Xcode. Per farlo è necessario lanciare XCode, aprire le preferenze con `cmd + ,` ed entrare nel pannello _Locations_

![xcode locations](https://raw.githubusercontent.com/grammaton/didattica/gh-pages/_img/xcodelocations.png)

Selezionata la giusta versione dei `command line tools` si può procedere all'installazione dell'[API](https://en.wikipedia.org/wiki/Application_programming_interface) csound attraverso node:

Ora si possono installare i pacchetti di Csound per Atom.

```text
apm install language-csound linter-csound ide-csound
```

I pacchetti [Atom](http://atom.io) relativi a Csound così come il legame tra node.js e csound-api sono sviluppati da [Nate Whetsell](https://github.com/nwhetsell).

[Qui una breve guida con un esempio di utilizzo di Csound all'interno di Atom](https://grammaton.github.io/didattica/esempio/csound).
