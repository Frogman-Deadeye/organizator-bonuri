# Organizator bonuri fiscale

Aplicație web care folosește inteligența artificială pentru a organiza bonurile fiscale în vederea decontării.

**Aplicația online:** https://frogman-deadeye.github.io/organizator-bonuri/

## Ce face

1. Încarci pozele bonurilor fiscale (JPG, PNG sau WEBP), oricâte deodată.
2. AI-ul citește de pe fiecare bon data, magazinul, CUI-ul, numărul bonului și totalul.
3. Fiecare bon este redenumit după dată, de exemplu `14-11-2026_Lidl_10,69lei.jpg`.
4. Bonurile sunt puse în foldere pe an și lună: `2026/11-Noiembrie/`.
5. Se generează un Excel centralizator (`Centralizator_bonuri.xlsx`) cu două foi:
   - **Bonuri**: toate bonurile, cu dată, magazin, CUI, număr bon, total, nume fișier și folder;
   - **Total pe luni**: numărul de bonuri și suma cheltuită în fiecare lună.
6. Descarci totul ca arhivă ZIP, gata de trimis la decontare.

Bonurile citite cu încredere scăzută sunt marcate „De verificat” și pot fi corectate direct în tabel înainte de export.

## Cum se folosește

Deschide linkul aplicației în orice browser (calculator sau telefon). Nu e nevoie de cont sau de instalare.

## Cum funcționează partea de AI

| Motor | Cum funcționează | Cost | Confidențialitate |
| --- | --- | --- | --- |
| **OCR în browser** (implicit) | Poza este convertită alb-negru și cu contrast mărit, apoi modelul neuronal Tesseract (limba română) extrage textul. Reguli automate găsesc data, rândul TOTAL, codul fiscal și numele magazinului. | Gratuit, fără cont | Pozele nu părăsesc dispozitivul |
| **Google Gemini** (opțional) | Poza este trimisă unui model AI multimodal, cu un prompt structurat care cere răspuns în format JSON. | Cheie API gratuită din Google AI Studio | Pozele sunt trimise la Google |

## Tehnologii

- HTML, CSS și JavaScript, fără server; rulează în întregime în browser
- Tesseract.js (OCR), SheetJS (Excel), JSZip (arhivă ZIP)
- Google Gemini API (opțional)

## Limitări

- Bonurile termice se decolorează; pozele neclare sau șifonate se citesc mai greu.
- Motorul OCR gratuit este mai puțin precis decât Gemini, mai ales la magazinele mici.
- Rezultatele trebuie verificate de om înainte de decontare.
- Pozele HEIC de pe iPhone trebuie salvate întâi ca JPG.

---

Proiect realizat pentru cursul „Competențe digitale – Utilizarea inteligenței artificiale”.
