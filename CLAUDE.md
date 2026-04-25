# Landingpage – Soutěž Langmeier & Co.

## Co je tento projekt

Jednoduchá landing page pro soutěž advokátní kanceláře Langmeier & Co.
Odkazovaná z newsletteru. Uživatel vyplní kvíz + kontaktní formulář a je zařazen do slosování o pobyt v resortu Mlýn Herlíkovice v Krkonoších.

## Soubory

```
soutez.html                  – jediný zdrojový soubor, vše inline (CSS + JS)
Logo/
  langmeier_logo_2024_281C.jpg  – logo kanceláře (bílé přes CSS filter)
Pictures/
  hlavní foto herlíkovice.jpeg  – hero pozadí (exteriér resortu)
  1ab.jpg                        – ložnice apartmánu
  3 doplnena.jpg                 – kuchyň + obývací pokoj
  8-7.jpg                        – wellness / jacuzzi
gdpr_zasady_final_v2.pdf       – GDPR dokument (odkaz v checkboxu + footer)
pravidla_souteze_final.pdf     – Pravidla soutěže (odkaz v checkboxu + footer)
```

## Architektura

- Čistý HTML/CSS/JS, žádné frameworky ani build kroky
- Mobile-first, responzivní
- Fonty: Playfair Display (nadpisy) + Inter (tělo) z Google Fonts

## Odesílání formuláře

**Primární: Web3Forms**
- Endpoint: `https://api.web3forms.com/submit`
- Access key: `e08f12e0-19b6-4bb5-888b-d80740ec7ba1` (hidden input ve formuláři)
- Příjemce `info@langmeier.cz` je nastaven v účtu Web3Forms (app.web3forms.com)
- Antispam: honeypot field (`name="botcheck"`) + implicitní ochrana Web3Forms
- Bez hCaptcha ani jiné viditelné captcha – záměrně kvůli konverzi

**Fallback: mailto**
- Aktivuje se pouze při chybě Web3Forms (výpadek sítě, chybný klíč)
- Otevře e-mailového klienta s předvyplněnými daty

## Tracking / analytika

Funkce `trackEvent(eventName, payload)` je připravena, ale tracking knihovny jsou zakomentovány.
Před spuštěním doplnit v `<head>`:
- Google Analytics 4: `G-XXXXXXXXXX`
- Meta Pixel: `YOUR_PIXEL_ID`
- LinkedIn Insight Tag: `YOUR_PARTNER_ID`

Implementované eventy:
- `quiz_start` – klik na „Začít kvíz"
- `quiz_answer_progress` – zodpovězení každé otázky (`{ question, answer }`)
- `quiz_submit` – úspěšné odeslání (`{ timestamp }`)
- `quiz_submit_error` – chyba odeslání (`{ message }`)

## Co záměrně není implementováno

- Žádný backend – vše řeší Web3Forms
- Žádná viditelná captcha
- Žádné cookies / consent banner (formulář sbírá jen soutěžní data se souhlasem)

## Nasazení

Stránka je statická – stačí nahrát celou složku na libovolný hosting.
Všechny cesty k obrázkům a PDF jsou relativní.

## Kontakt / příjemce soutěžních dat

info@langmeier.cz (nastaveno ve Web3Forms účtu)
