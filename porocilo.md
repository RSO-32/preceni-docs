# Preceni 

Vid Smole, Vid Purgar

## Opis

Preceni je spletni sledilnik cen, namenjen spremljanju in beleženju nihanja cen izdelkov, ki so na voljo v spletnih trgovinah slovenskih trgovcev. Uporabnikom omogoča, da poiščejo določene izdelke in spremljajo spreminjanje cene skozi čas, hkrati pa jim omogoča tudi vpogled v zgodovino cene izdelka. Z uporabo Preceni lahko uporabnik naredi bolj informiran nakup, saj ima več informacij o ceni izdelka in ga tako trgovec ne more zavesti s trajnimi popusti in višanjem cen pred začetkom akcij.


## URL
- [https://preceni-ui.smole.org/](https://preceni-ui.smole.org/): Uporabniški vmesnik

- Naslov, na katerem so dostopne mikrostoritve: https://rso.smole.org - /data, /auth, /notify, /scrape

## Mikrostoritve
- `preceni-data` ([GitHub](https://github.com/RSO-32/preceni-data), [DockerHub](https://hub.docker.com/r/vidvidex/preceni-data)) - dostop do podatkov o izdelkih
  - prikaže trenutno ceno izdelka v različnih spletnih trgovinah
  - omogoča prikaz zgodovine cen izdelka
  - prikaže druge splošne podatke o izdelku (ime, opis, slike, ...)
  - napredno iskanje izdelkov glede na različne kriterije (trgovina, cena, kategorija, ...)
- `preceni-scrape` ([GitHub](https://github.com/RSO-32/preceni-scrape), [DockerHub](https://hub.docker.com/r/vidvidex/preceni-scrape)) - web scraper za pridobivanje podatkov o izdelkih iz spletnih trgovin
  - pridobivanje podatkov iz spletnih trgovin slovenskih trgovcev (Mercator, Tuš, Hofer, Špar, ...)
  - uporablja API, če ta obstaja ali pa web scraping, če API ni na voljo
- `preceni-notify` ([GitHub](https://github.com/RSO-32/preceni-notify), [DockerHub](https://hub.docker.com/r/vidvidex/preceni-notify)) - pošiljanje obvestil uporabnikom
  - uporabnike prek epošte ali drugih storitev obvesti, ko se cena izdelka spremeni (pade pod določeno mejo)
- `preceni-auth` ([GitHub](https://github.com/RSO-32/preceni-auth), [DockerHub](https://hub.docker.com/r/vidvidex/preceni-auth)) - avtentikacija uporabnikov
  - login, register
  - upravljanje računa
- `preceni-ui` ([GitHub](https://github.com/RSO-32/preceni-ui)) - preprost uporabniški vmesnik
  - pregled izdelkov
- `preceni-docs` ([GitHub](https://github.com/RSO-32/preceni-docs)) - dokumentacija

## Ogrodje
- Zaledne storitve so narejene z uporabo ogrodja Flask.
- Uporabniški vmesnik je narejen z uporabo Vue.js

## Razvojno okolje
  Storitve so bile razvite z uporabo VSCode, za pošiljanje zahtevkov pa sva uporabila Postman.

## Zunanji API
  <!--Kratek opis uporabe zunanjih API-jev v vaših rešitvah.-->
- `Mercator API` - pridobivanje podatkov(ime, cena, slike, ...) o izdelkih iz spletne trgovine Mercator
- `Barcode API` - dodajanje novih izdelkov in cen preko črtne kode

## Shema arhitekture
  <!--Shemo arhitekture in interakcij med mikrostoritvami. Označite tudi komunikacijske protokole med mikrostoritvami.-->
  ![arhitektura](arhitektura.png)


## Konfiguracija
  <!--Kratek opis uporabe različnih virov konfiguracije v vaših rešitvah (okoljske spremenljivke, konfiguracijska datoteka, skrivnosti).-->
- Okoljske spremenljivke: Za shranjevanje konfiguracije (npr. PYTHONUNBUFFERED)
- Skrivnosti: Za shranjevanje ključev (npr. RAPIDAPI_KEY)


## Kontrole zdravja in metrike
  <!--Seznam implementiranih kontrol zdravja in metrik.-->
Kontrole zdravja so implementirane na končnih točkah /health/live, metrike pa na končnih točkah /metrics.

- Kontrole zdravja:
  - `preceni-data`:
    - database
    - disk
    - test (za simuliranje bolne mikrostoritve)
  - `preceni-scrape`:  
    - disk
    - test (za simuliranje bolne mikrostoritve)
  - `preceni-notify`: 
    - database
    - disk
    - test (za simuliranje bolne mikrostoritve)
  - `preceni-auth`: 
    - database
    - disk
    - test (za simuliranje bolne mikrostoritve)

- Metrike:
  - `preceni-data`:
    - disk total 
    - disk used 
    - disk free
    - cpu percent 
    - ram percent 
  - `preceni-scrape`:  
    - disk total 
    - disk used 
    - disk free
    - cpu percent 
    - ram percent 
    - requests delay seconds 
    - mercator scraper on
  - `preceni-notify`: 
    - disk total 
    - disk used 
    - disk free
    - cpu percent 
    - ram percent 
  - `preceni-auth`:
    - disk total 
    - disk used 
    - disk free
    - cpu percent 
    - ram percent 

## Beleženje dnevnikov
  <!--Kratek opis centraliziranega beleženja dnevnikov v vaši aplikaciji.-->



## Izolacija in toleranca napak
  <!--Kratek opis demonstracije za izolacijo in toleranco napak, ki ste jo pripravili za vašo aplikacijo.-->