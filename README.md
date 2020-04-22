# CGI kodutöö

### Projekti seadistamine (CGI-homework kaustas avage käsurida ja sisestage)
```
npm install
```

### Projekti käivitamine (CGI-homework kaustas avage käsurida ja sisestage)
```
npm run serve
```

## Projekti avanedes ...
Projekti avanedes näite Te vasakul andmete sisestusvälja. Kui vaadata ülevalt all, siis esimene sisestusrida palub Teid sisestada geograafilist laiust, teine rida aga geograafilist pikkust. Sisestada saab ainult reaalarve. Võimalus on ka valida mingit koordinaati kaardi pealt. Selleks peab vajutama kaardile soovitatud kohale. Sisetusread peavad automaatselt uuenema.

Nüüd kui tahate vaadata üht kindlat kuupäeva valitud koordinaatidel, siis valite kuupäevade osas ainult esimest sisestust ning vajutate sinist nuppu "OTSI". Kui aga tahate vaadata valitud andmeid kahe kuupäeva vahel, siis lisaks esimesele kuupäevaväljale, sisestate ka teise kuupäeva alumise sisestuskohta ning vajutate nuppu "OTSI". **NB!!! ÄRGE SISETAGE SUURT KUUPÄEVADE VAHEMIKKU, MUIDU API EI HAKKA VASTAMA!**

Kui andmed ei ole sisestatud, siis tulemust ei näidata.

## Projektist
Selleks kodutööks kuulutasin umbes 8 tundi. Iseenesest kodutöö ei olnud raske. Ehk selle põhimõte oli väga lihtne - luua UI, kus kasutaja saab sisestada andmeid, saata neid serverile, saada andmeid API'st ning näidata neid. Raskused tulid sisse tehnilises pooles. Esimeseks raskuseks oli kaardi seadistamine. Õnneks Teie poolt soovitatud https://leafletjs.com/ oli antud ülesande jaoks väga hea. Siiski dokumentatsiooni lugemine ja ülespanek võtis aega. Teine, minu arvates raskeim, probleem oli andmete kättesaamine. Mina kasutasin https://sunrise-sunset.org/api , kuhu saatsin *GET requeste*. Esialgu, kui kasutasin ainult üht kuupäeva, kõik töötas väga hästi. Kui aga tahtsin saada andmeid mitme kuupäeva kohta (üle 10), siis sain "NETWORK ERROR". Tuli välja, et antud API omab kindlat limiiti ning kui teha palju *requeste*, siis see ei hakka vastama. Kuid siiski väga väikese vahemiku jaoks see töötab enam-vähem normaalselt. Leidsin internetist sarnaseid API'sid, kuid need olid kas tasulised või siis omasid mingit prooviaega. Otsustasin, et jään esilagse plaani juurde ning teavitan Teid, et mitte sisestada suurt vahemikku. Viimaseks probleemiks oli minu jaoks y-teljel ajapanek. Kuna formaat HH:MM:SS ei ole matemaatiliselt kirjeldatav, siis otsustasin, et jagan aja eraldi tundideks, minutiteks ja sekunditeks. Jällegi, kuna API ei taha saada palju *requeste*, siis pidin valima ainult ühe. Valikuks osutusid minutid. Kui rääkida lihtsadest osadest, siis kõige lihtsam oligi rakenduse komponentide õigele kohale panek ja nende vahelise suhtlemise seadistamine. Samuti ka graafiku loomine oli väga lihtne. Selleks kasutasin juba valmis teeki ApexChart, mis lihtsalt nõudis õigeid andmeid.

Veel saan lisada juurde, et kasutasin võimsa Vue.js frontend frameworki, kuna see tundub minu jaoks kõige loogilisem ja kiirem veebiarenduses.
