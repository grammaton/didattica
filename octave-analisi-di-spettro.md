---
description: Costruirsi uno script per l'analisi di spettro di un file audio
---

# Octave - Analisi di Spettro

Lo scopo di questa piccola guida è quello di capire come utilizzare Octave per ottenere dei grafici di analisi del contenuto spettrale di un file audio.

```text
f = figure('visible','off');
[fname, fpath, fltidx] = uigetfile()
file = strcat(fpath,fname);
info = audioinfo (file)
fs = input ("Select Sample Rate: ")
ared = audioread(file);
b = ared(:, [1]);
wsize = input ("Select the Window Size: ")
[h, w] = freqz (b, 1, wsize, fs);
freqz_plot(w, h)
[filepath,name,ext] = fileparts(file);
wsizestr = num2str(wsize);
outname = strcat(name, '_', wsizestr, '.eps')
print(outname, "-deps") %-color
```



