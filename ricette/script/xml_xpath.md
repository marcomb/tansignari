# Estrarre dati da un file XML con Google sheet (XPATH)

* autore: [gbvitrano](https://twitter.com/gbvitrano)
* issue: [#50](https://github.com/opendatasicilia/tansignari/issues/50) fornitore ricetta _[Andrea Borruso](https://twitter.com/aborruso?lang=it)_

**Ricetta beta version**

---

**Caso d'uso:** il file di tematizzazione di un layer (in [QGIS](https://qgis.org/it/site/)) è un file [XML](https://it.wikipedia.org/wiki/XML), alcune volte è necessario reperire i codici colore (in [rgba](https://it.wikipedia.org/wiki/RGBA)) direttamente dal file di tematizzazione: questa ricetta estrae i codici colori utilizzati e crea una tabella, in [CSV](https://it.wikipedia.org/wiki/Comma-separated_values), pronta per essere utilizzata in QGIS e messa in join con il layer in esame. (dalla [ricetta](https://tansignari.readthedocs.io/it/latest/ricette/script/Estrarre_dati_da_file_XML.html#utility-xmlstarlet-con-linguaggio-xpath) di [@Totò Fiandaca](https://twitter.com/totofiandaca?lang=it))

Il file [sheet](https://docs.google.com/spreadsheets/d/1tjXYrhP2nggPxML3Vay2Ycab7ikACQ95scRHLjo_GYc/edit#gid=0) iniziale per l'importazione del file [tema.xml](https://gist.githubusercontent.com/aborruso/5452bbecbacfce8ac61b5cc8165ac0d4/raw/0b0243ac25361726fd1a112e8bdea7920d1d487b/tema.xml) e le relative query XPATH è scritto da [Andrea Borruso](https://twitter.com/aborruso?lang=it)

![](/img/xpath/xml_00.jpg)

File xml da cui estrarre i dati [tema.xml](http://gbvitrano.it/clip/umap/tema.xml)

![](/img/xpath/sheet_01.jpg)

![](/img/xpath/xml_01.jpg)

![](/img/xpath/sheet_02.jpg)

![](/img/xpath/xml_02.jpg)

![](/img/xpath/sheet_03.jpg)

![](/img/xpath/xml_03.jpg)

![](/img/xpath/sheet_04.jpg)

alla fine si fa il JOIN con VLOOKUP (cit. [Andrea Borruso](https://twitter.com/aborruso?lang=it))

## Utility yq
Studiando il comando utilizzato per estrarre i dati con l'utility **[yq](https://stedolan.github.io/jq/)**, ci rendiamo conto che anche se scritta ovviamente in modo diverso, la query è sempre la stessa, il file *tema.xml* si trova il locale e la finstra *bash* è aperta direttamente nella cartella del file *tema.xml*

```
<tema.xml xq -r '.qgis["renderer-v2"].symbols.symbol[]|[.["@name"],.layer.prop[1]["@v"]]|@csv' >./idColori.csv
```
```
<tema.xml xq -r '.qgis["renderer-v2"].categories.category[]|[.["@symbol"],.["@value"]]|@csv' >./idRegioni.csv
```


