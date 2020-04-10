# Setup Raspebbry Pi4

Su linux, salvo casi particolari, si può procedere a scaricare da GitHub il codice
sorgente di [Faust](https://github.com/grame-cncm/faust) ed installarlo attraverso
i seguenti comandi eseguiti una riga alla volta.

```bash
git clone https://github.com/grame-cncm/faust.git
cd faust
git submodule update --init
make
sudo make install
```

Il comando finale, `sudo make install` chiama il programma `sudo` che abilita
l'esecuzione del comando successivo `make install` nella modalità **superuser**,
**s**-uper **u**-ser **do**. Il la modalità superuser necessita dell'inserimento
della password di sistema che verrà digitata dentro la finestra di terminale. È
importante notare che il terminale ovviamente non mostrerà i caratteri immessi,
quindi al termine dell'immissione della password premere `RETURN` come consueto.

Il comando `make` è diviso in due fasi, la seconda appena illustrata si limita ad
installare ciò che `make` precedentemente ha compilato e preparato per l'installazione.
Il processo di `make` da codice sorgente può essere piuttosto lungo, dipende dalla
potenza della macchina su cui si sta operando e dalla complessità del codice
sorgente che si sta compilando.

Se volete sapere quanti danni potete fare in modalità *superuser* non vi resta
che leggere il manuale digitando `man sudo`. `man` è il programma che apre la
pagina del manuale di ogni buon comando. Dentro al manuale si avanza
una riga per volta premendo `RETURN`, una pagina per volta premendo `SPACE`, si esce
automaticamente una volta raggiunta la fine oppure prematuramente premendo `Q`.
