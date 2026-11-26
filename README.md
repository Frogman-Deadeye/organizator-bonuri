# Organizator bonuri fiscale

Aplicație web care folosește inteligența artificială pentru a organiza bonurile fiscale în vederea decontării.

**Aplicația online:** `https://frogman-deadeye.github.io/organizator-bonuri/` 

## Ce face

1. Încarci pozele bonurilor fiscale (JPG, PNG sau WEBP), oricâte deodată.
2. AI-ul citește de pe fiecare bon **data**, **magazinul**, **CUI-ul**, **numărul bonului** și **totalul**.
3. Fiecare bon este redenumit după dată, de exemplu `14-11-2026_Lidl_10,69lei.jpg`.
4. Bonurile sunt puse în foldere pe an și lună: `2026/11/`.
5. Se generează un **Excel centralizator** (`Centralizator_bonuri.xlsx`) cu două foi:
   - **Bonuri**: toate bonurile, cu dată, magazin, CUI, număr bon, total, nume fișier și folder;
   - **Total pe luni**: numărul de bonuri și suma cheltuită în fiecare lună.
6. Descarci totul ca arhivă ZIP, gata de trimis la decontare.

Bonurile citite cu încredere scăzută sunt marcate **„De verificat”** și pot fi corectate direct în tabel înainte de export.

## Cum se folosește

Deschide linkul aplicației în orice browser (calculator sau telefon). Nu e nevoie de cont sau de instalare.

Pentru o probă rapidă poți folosi poza de test din folderul `exemple/` (un bon **fictiv**, creat doar pentru testare).

## Cum funcționează partea de AI

Aplicația are două motoare de citire, la alegere:

| Motor | Cum funcționează | Cost | Confidențialitate |
| --- | --- | --- | --- |
| **OCR în browser** (implicit) | Poza este convertită alb-negru și cu contrast mărit, apoi modelul neuronal **Tesseract** (antrenat pentru limba română) extrage textul. Reguli automate găsesc data, rândul TOTAL, codul fiscal și numele magazinului. | Gratuit, fără cont | Pozele nu părăsesc dispozitivul |
| **Google Gemini** (opțional) | Poza este trimisă unui model AI multimodal, împreună cu un prompt structurat care cere răspuns în format JSON. | Cheie API gratuită din [Google AI Studio](https://aistudio.google.com/apikey) | Pozele sunt trimise la Google |

Promptul folosit pentru Gemini este afișat în aplicație, la secțiunea „Cum citește aplicația bonurile”.

## Tehnologii

- HTML, CSS și JavaScript, fără server; aplicația rulează în întregime în browser
- [Tesseract.js](https://github.com/naptha/tesseract.js) pentru OCR (recunoaștere optică a caracterelor)
- [SheetJS](https://sheetjs.com/) pentru generarea fișierului Excel
- [JSZip](https://stuk.github.io/jszip/) pentru arhiva ZIP
- Google Gemini API (opțional)

## Limitări

- Bonurile termice se decolorează în timp; pozele neclare, șifonate sau în lumină slabă se citesc mai greu.
- Motorul OCR gratuit este mai puțin precis decât Gemini, mai ales la numele magazinelor mici.
- Rezultatele trebuie verificate de om înainte de decontare, mai ales bonurile marcate „De verificat”.
- Pozele HEIC de pe iPhone trebuie salvate întâi ca JPG.

## Publicare pe GitHub Pages

1. Creează un repository public numit `organizator-bonuri`.
2. Încarcă fișierele `index.html`, `README.md` și folderul `exemple/`.
3. Mergi la **Settings → Pages**, alege **Deploy from a branch**, ramura `main`, folderul `/ (root)` și apasă **Save**.
4. După 1–2 minute aplicația este disponibilă la `https://frogman-deadeye.github.io/organizator-bonuri/`.

---

Proiect realizat pentru cursul „Competențe digitale – Utilizarea inteligenței artificiale”.
