# Organizator bonuri fiscale

Aplicație web care folosește inteligența artificială pentru a organiza bonurile fiscale în vederea decontării.

## 👉 [Deschide aplicația](https://frogman-deadeye.github.io/organizator-bonuri/)

Link direct: https://frogman-deadeye.github.io/organizator-bonuri/

## Ce face

1. Încarci pozele bonurilor fiscale (JPG, PNG sau WEBP), oricâte deodată.
2. AI-ul citește de pe fiecare bon **data**, **magazinul**, **CUI-ul**, **numărul bonului** și **totalul**.
3. Fiecare bon este redenumit în formatul **`AAAA.LL.ZZ_Magazin`**, de exemplu `2026.11.24_Mega Image.jpg`.
4. Bonurile sunt puse în foldere pe an și lună, de exemplu `2026/11/`.
5. Se generează un **Excel centralizator** (`Centralizator_bonuri.xlsx`) cu două foi:
   - **Bonuri**: toate bonurile, cu dată, magazin, CUI, număr bon, total, nume fișier și folder;
   - **Total pe luni**: numărul de bonuri și suma cheltuită în fiecare lună.
6. Descarci totul ca arhivă ZIP, gata de trimis la decontare.

## Verificarea rezultatelor

| Stare | Ce înseamnă |
| --- | --- |
| **✓ Gata** | Datele au fost citite și confirmate automat. |
| **! De verificat** | Data sau totalul nu au putut fi confirmate; verifici pe poză, corectezi dacă e nevoie și apeși **Verificat ✓**. |
| **Imaginea nu pare a fi un bon fiscal** | Imaginea nu este inclusă în ZIP, în Excel și nici în totaluri. |

- Orice câmp (dată, magazin, total) se poate corecta direct în tabel.
- Click pe miniatura bonului (iconița cu lupă) deschide poza mărită.
- „Vezi textul citit” arată poza alături de textul extras, cu buton de copiere.

## Cum se folosește

Deschide [aplicația](https://frogman-deadeye.github.io/organizator-bonuri/) în orice browser, pe calculator sau pe telefon. Nu e nevoie de cont sau de instalare.

Pentru testare, în folderul [`exemple/`](exemple/) se găsesc poze cu bonuri reale (Dr.Max, Mega Image, Kaufland).

## Cum funcționează partea de AI

| Motor | Cum funcționează | Cost | Confidențialitate |
| --- | --- | --- | --- |
| **OCR în browser** (implicit) | Poza este convertită alb-negru cu prag adaptiv, apoi modelul neuronal **Tesseract** (limba română) extrage textul în două treceri. Reguli automate găsesc data (verificată și din codul ID UNIC), totalul (confirmat cu suma plătită), codul fiscal și numele magazinului. | Gratuit, fără cont | Pozele nu părăsesc dispozitivul |
| **Google Gemini** (opțional) | Poza este trimisă unui model AI multimodal, cu un prompt structurat (Rol – Context – Sarcină – Format) care cere răspuns în format JSON. | Cheie API gratuită din [Google AI Studio](https://aistudio.google.com/apikey) | Pozele sunt trimise la Google |

Promptul folosit pentru Gemini este afișat în aplicație, la secțiunea „Cum citește aplicația bonurile”.

## Rezultate test

Pe un lot de 10 bonuri:

| Etapa | Manual | Cu aplicația |
| --- | --- | --- |
| Scanare / poze cu telefonul | 5 min | 2–3 min |
| Identificarea datei, redenumirea și organizarea | 30 min | ≈ 50 s |
| Verificarea datelor | – | max. 5 min |
| Trecerea în Excel | 20 min | ≈ 15 s |
| **Total** | **55 min** | **≈ 9 min (−84%)** |

## Tehnologii

- HTML, CSS și JavaScript, fără server; aplicația rulează în întregime în browser
- [Tesseract.js](https://github.com/naptha/tesseract.js) – OCR (recunoaștere optică a caracterelor)
- [SheetJS](https://sheetjs.com/) – generarea fișierului Excel
- [JSZip](https://stuk.github.io/jszip/) – arhiva ZIP
- Google Gemini API (opțional)
- Găzduire gratuită pe GitHub Pages

## Limitări

- Bonurile termice se decolorează în timp; pozele neclare, șifonate sau în lumină slabă se citesc mai greu.
- Motorul OCR gratuit este mai puțin precis decât Gemini, mai ales la totalurile scrise cu font mare sau acoperite de scris de mână.
- Rezultatele trebuie verificate de om înainte de decontare, mai ales bonurile marcate „De verificat”.
- Pozele HEIC de pe iPhone trebuie salvate întâi ca JPG.

---

Proiect realizat de Ciotec Andrei pentru cursul „Competențe digitale – Utilizarea inteligenței artificiale”.
