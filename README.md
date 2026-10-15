# Français à De Beuk – handleiding

Oefensite Frans voor de leerlingen van Secundaire School De Beuk (werkwoorden, indicatif présent).

De site bestaat uit twee delen:

| Deel | Waar | Wat |
|---|---|---|
| De website | GitHub Pages (gratis) | `index.html` voor de leerlingen, `resultats.html` voor de leerkracht, `config.js` met de instellingen |
| De opslag | Een Google Sheet met een script (`Code.gs`) | Bewaart resultaten, voortgang en de tests in de klas |

Er staan **geen leerlingengegevens op GitHub**. Alles wat leerlingen doen, komt alleen in jouw Google Sheet terecht.

---

## Deel 1 – De Google Sheet en het script (± 5 minuten)

1. Maak in Google Drive een nieuwe Google Sheet, bijvoorbeeld *Frans – resultaten*.
2. Kies **Extensies → Apps Script**.
3. Verwijder de voorbeeldcode in `Code.gs` en plak de volledige inhoud van het bestand **`Code.gs`**.
4. Vul bovenaan je eigen leerkrachtcode in bij `CODE_PROF` (bijvoorbeeld `'frans-beuk-7351'`). Met die code open je later de resultaten. Klik op het diskette-icoon om te bewaren.
5. Klik rechtsboven op **Implementeren → Nieuwe implementatie**.
   - Klik op het tandwiel naast *Type selecteren* en kies **Web-app**.
   - *Uitvoeren als*: **Ik**
   - *Wie heeft toegang*: **Iedereen**
   - Klik op **Implementeren** en geef de toestemming die Google vraagt (kies je account → *Geavanceerd* → *Ga naar … (onveilig)* → *Toestaan*; dat is normaal voor een eigen script).
6. Kopieer de **URL van de web-app**. Die eindigt op `/exec`. Je hebt ze nodig in deel 2.

> Waarom "Iedereen"? De site op GitHub moet het script kunnen bereiken. Het script geeft de resultaten alleen aan wie de leerkrachtcode kent.

## Deel 2 – De website op GitHub (± 10 minuten)

1. Maak een gratis account op [github.com](https://github.com) (of meld je aan).
2. Klik rechtsboven op **+ → New repository**.
   - *Repository name*: bijvoorbeeld `frans-de-beuk`
   - Kies **Public** (GitHub Pages is gratis voor openbare repositories; er staan geen persoonsgegevens in).
   - Klik op **Create repository**.
3. Klik op **uploading an existing file** (of *Add file → Upload files*). Sleep deze vier bestanden in het venster:
   `index.html`, `resultats.html`, `config.js`, `README.md`
   Klik onderaan op **Commit changes**.
4. Klik in de lijst op **`config.js`**, dan op het potlood (*Edit*). Plak de URL uit deel 1 tussen de aanhalingstekens bij `ENDPOINT`:
   ```js
   ENDPOINT: 'https://script.google.com/macros/s/.../exec',
   ```
   Klik op **Commit changes**.
5. Ga naar **Settings → Pages**. Kies bij *Source* **Deploy from a branch**, kies de branch **main** en de map **/ (root)**, en klik op **Save**.
6. Na één à twee minuten verschijnt bovenaan de pagina het adres van je site, bijvoorbeeld
   `https://jouwnaam.github.io/frans-de-beuk/`

**Links**
- Voor de leerlingen: `https://jouwnaam.github.io/frans-de-beuk/` – deel die link via Smartschool, Classroom of een QR-code.
- Voor jou: `https://jouwnaam.github.io/frans-de-beuk/resultats.html` – log in met je leerkrachtcode. Je kunt ook rechtstreeks in de Google Sheet kijken.

**Even testen**: open de leerlingenlink, meld je aan als testleerling en maak één oefening. Na enkele seconden staat er een rij in het tabblad *Résultats* van je Sheet, en onderaan de site staat "Résultats enregistrés".

## Deel 3 – Aanmelden met het Google-account van de school (aanbevolen, ± 10 minuten)

Zonder deze stap typen leerlingen hun naam en kiezen ze hun klas. Dat werkt, maar een leerling kan een andere naam intikken. Met deze stap melden ze zich aan met hun schoolaccount: de naam klopt altijd en de voortgang volgt hen naar elk toestel.

1. Ga naar [console.cloud.google.com](https://console.cloud.google.com) met je schoolaccount en maak een nieuw project (bijvoorbeeld *Frans De Beuk*).
2. Zoek **Google Auth Platform** (of *OAuth-toestemmingsscherm*) en klik op **Aan de slag**.
   - App-naam: *Français à De Beuk*, ondersteunings-e-mail: je eigen adres.
   - Doelgroep: **Intern** (alleen accounts van de school).
3. Ga naar **Clients → Client maken**.
   - Type: **Webapplicatie**
   - *Geautoriseerde JavaScript-oorsprongen*: `https://jouwnaam.github.io` (zonder `/frans-de-beuk` en zonder schuine streep op het einde)
   - Klik op **Maken** en kopieer de **Client-ID** (eindigt op `.apps.googleusercontent.com`).
4. Plak de Client-ID op twee plaatsen:
   - in `config.js` op GitHub bij `GOOGLE_CLIENT_ID`;
   - in `Code.gs` bij `GOOGLE_CLIENT_ID`. Vul daar ook `DOMAINE` in met het domein van de leerlingenaccounts (bijvoorbeeld `'leerling.svsl.be'`), zodat alleen schoolaccounts binnen kunnen.
5. Maak in Apps Script een nieuwe versie van de implementatie (zie deel 5). De eerste keer vraagt Google een extra toestemming, omdat het script de aanmelding moet controleren.

> Lukt stap 1 of 2 niet, dan heeft de ICT-beheerder van de school dit waarschijnlijk afgeschermd. Vraag hem om het project aan te maken of je de rechten te geven.

## Deel 4 – De test in de klas gebruiken

Elk leerpad heeft naast de *Test final* ook een **Test en classe**. Die staat standaard dicht.

1. Open `resultats.html`, log in met je code en klik op **Gérer les tests en classe**.
2. Vink bij het leerpad **Ouvert** aan. Vul eventueel een **code** in die je op het bord schrijft: wie thuis zit en de code niet kent, kan de toets niet starten. Kies of leerlingen na afloop de **correctie** mogen zien. Klik op **Enregistrer**.
3. De leerlingen zien de toets nu in hun leerpad (eventueel na het vernieuwen van de pagina). Ze krijgen **één poging**. De toets opent op volledig scherm. Kopiëren, plakken, rechtsklikken en afdrukken zijn geblokkeerd, en de theorie is niet beschikbaar.
4. Onder het leerpad zie je **live** (vernieuwt elke 15 seconden) wie begonnen is, wie de toets heeft ingediend, met welke score, en **elke keer dat een leerling de pagina verliet**: het uur, de manier (ander tabblad of andere app, ander venster, volledig scherm verlaten, toets voor een schermafdruk) en hoe lang. Een leerling die de toets opnieuw opende, krijgt een rode markering "2 débuts".
5. Zet de toets na de les weer dicht: vink **Ouvert** uit en klik op **Enregistrer**. Open je hem later opnieuw, dan is dat een nieuwe reeks en mag elke leerling hem opnieuw één keer maken.

Alle resultaten van de test in de klas staan ook in de Sheet (type `test-classe`; elke sortie staat apart als type `sortie`).

**Wat een website niet kan.** Een website mag niet zien naar welke site een leerling gaat; browsers laten dat om privacyredenen niet toe. De site ziet alleen dát de leerling de pagina verlaat, wanneer en hoelang. Een schermafdruk, Google Lens via de adresbalk of een foto met de gsm kan een website ook niet tegenhouden. Wil je dat echt afsluiten, dan kan dat alleen op toestellen die de school beheert, via de Google Admin-console (ICT-beheerder): daar kunnen schermafdrukken, Google Lens en AI-sites geblokkeerd worden en kan de browsergeschiedenis van beheerde Chromebooks bekeken worden.

## Deel 5 – Later iets aanpassen

- **Nieuwe versie van de site**: open op GitHub het bestand (`index.html` of `resultats.html`), klik op *Add file → Upload files*, sleep de nieuwe versie erin en klik op *Commit changes*. `config.js` laat je staan. De site is na een minuutje bijgewerkt.
- **Nieuwe versie van `Code.gs`**: plak de nieuwe code in Apps Script, vul `CODE_PROF`, `GOOGLE_CLIENT_ID` en `DOMAINE` opnieuw in, bewaar, en kies **Implementeren → Implementaties beheren → potlood → Versie: Nieuwe versie → Implementeren**. De URL blijft dezelfde, dus `config.js` hoeft niet te veranderen.

## Variante zonder GitHub

Je kunt de site ook rechtstreeks door Google laten tonen. Maak in Apps Script via **+ → HTML** een bestand met de naam `index` en plak daarin de inhoud van `variante-zonder-github/index.html`. Kies bij de implementatie *Wie heeft toegang*: **Iedereen binnen [het domein van de school]**. De URL van de web-app is dan meteen de link voor de leerlingen; de school-aanmelding werkt vanzelf, zonder deel 3. De resultaten bekijk je via de link *Espace professeur* onderaan het aanmeldscherm.
