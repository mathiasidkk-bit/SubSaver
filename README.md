# 💸 SubSaver – Stop med at betale for meget

> Alle dine abonnementer ét sted. Se hvad du betaler, bliv mindet om kommende betalinger, og find billigere alternativer.

## Problemet
De fleste har 5-15 abonnementer (streaming, musik, fitness, software, aviser, cloud m.m.). Mange bruges sjældent, priserne stiger stille og roligt, og ingen har det fulde overblik over de samlede udgifter.

## Løsningen
SubSaver samler alle brugerens abonnementer og viser, hvor pengene går hen – og hvor der kan spares.

## Kernefunktioner (MVP)
- [x] **Samlet overblik** – tilføj abonnementer manuelt fra en katalogliste (Netflix, Viaplay, Disney+, Spotify m.fl.)
- [x] **Månedlige og årlige udgifter** – alle betalingsintervaller omregnes automatisk
- [x] **Kommende betalinger** – sorteret efter næste trækningsdato
- [x] **Billigere alternativer** – forslag inden for samme kategori
- [x] **Tilbud** – fx "3 måneder gratis på Viaplay" (sponsoreret/affiliate, tydeligt markeret)
- [x] **Familie** – forældre styrer børns abonnementer, sætter budgetter og godkender anmodninger (se "Familiefunktion")
- [ ] **Push-/mail-påmindelser** 1-3 dage før betaling og før gratisperioder udløber
- [ ] **"Bruger du det?"-tjek** – markér abonnementer, du sjældent bruger, og se potentiel besparelse
- [ ] **Prisstigningsalarm** – besked når en tjeneste hæver prisen
- [ ] **Opsigelses-guide** – direkte link/trin til at opsige hver tjeneste

## Ekstra idéer (efter MVP)
- Automatisk opdagelse af abonnementer via Open Banking (kontoudtog, kun med brugerens samtykke)
- Del-abonnement-forslag (familie-/deleplaner) med besparelse
- "Rotér i stedet for at beholde": forslag om at pause en streamingtjeneste og skifte måned for måned
- Årlig sparerapport ("Du sparede 1.240 kr. i år")
- Familieplaner: automatisk forslag om at slå flere enkeltabonnementer sammen

## Familiefunktion
- **Profiler:** Voksne og børn i samme husstand. Hver person har sine egne abonnementer og et valgfrit månedligt budget.
- **Overblik for forældre:** Samlet husstandsudgift, udgift pr. person og advarsel, hvis et barn går over sit budget.
- **Godkendelse:** Børn kan ikke selv oprette abonnementer, men sender en anmodning, som en forælder godkender eller afviser. Forælderen advarres, hvis godkendelsen sprænger budgettet.
- **Delte abonnementer:** Marker et abonnement som "Hele familien", så det ikke tæller dobbelt.
- **Spar-tip:** Appen foreslår ét familieabonnement, hvis flere i familien betaler for den samme tjeneste hver for sig.
- **Børnevenligt:** Børneprofiler ser kun deres egne abonnementer og får aldrig vist annoncer eller sponsorerede tilbud.
- **Prototype vs. rigtig app:** Prototypen har et "Se som"-valg til at teste børnevisningen og er ikke sikker. I den rigtige app styres roller af separate konti (Supabase Auth + Row Level Security), og forældre inviterer børn.
- **Børn og persondata:** Der gælder særlige regler for børns persondata og samtykke (i Danmark 13 år). Tjek gældende regler, og få forældresamtykke på plads, før appen bruges af børn.

## Indtjening
| Kilde | Beskrivelse |
|---|---|
| **Premium** (fx 29 kr./md.) | Ubegrænsede påmindelser, prisalarmer, bankforbindelse, flere familieprofiler, sparerapport |
| **Affiliate/provision** | Provision når brugere tegner abonnement via vores anbefalinger/tilbud |
| **Partneraftaler** | Eksklusive tilbud (fx gratis prøvemåneder) mod betaling pr. tilmelding |

**Vigtigt:** Anbefalinger skal være ærlige. Sponsorerede tilbud markeres tydeligt som "Annonce/Tilbud", og alternativer rangeres efter brugerens besparelse – ikke kun efter hvem der betaler mest. Det er både påkrævet (markedsføringsloven) og det, der opbygger tillid.

## Målgruppe
Privatpersoner og familier i Danmark (start), derefter Norden. Især 20-45-årige med flere streaming-/app-abonnementer.

## Konkurrence og differentiering
Eksisterende apps (fx Rocket Money, Bobby, Subby) er mest internationale. SubSaver differentierer sig ved:
1. Fokus på **danske tjenester og danske priser** (Viaplay, TV 2 Play, DR m.fl.)
2. **Aktive besparelsesforslag** frem for blot en liste
3. Dansk sprog, MitID/Open Banking på sigt

## Teknologi (forslag)
| Lag | Valg |
|---|---|
| Mobilapp | React Native (Expo) – iOS + Android |
| Backend | Supabase (Postgres, Auth, Row Level Security) |
| Notifikationer | Expo Push + e-mail (Resend) |
| Priskatalog | JSON/DB over tjenester, planer og priser (vedligeholdes manuelt, senere automatisk) |
| Bankdata (senere) | Open Banking-udbyder, fx Enable Banking eller Tink |
| Analytics | PostHog (privacy-venlig) |

## Datastruktur (kort)
- `services` – katalog: navn, kategori, logo, affiliate-link
- `plans` – pris, interval, kommentar, sidst verificeret
- `households` / `household_members` – husstand, medlemmer, rolle (voksen/barn), månedligt budget
- `subscription_requests` – børns anmodninger med status (afventer/godkendt/afvist)
- `user_subscriptions` – bruger, ejer (person eller hele familien), service/plan, pris, interval, næste betalingsdato, sidst brugt, gratisperiode slutter
- `offers` – tilbud, gyldighed, sponsoreret ja/nej
- `reminders` – udsendte/planlagte påmindelser

## Persondata og GDPR
- Gem kun det nødvendige; abonnementsdata er personlige oplysninger.
- Samtykke til bankdata, mulighed for at slette al data med ét klik.
- Row Level Security: brugere kan kun se egne data.
- Privatlivspolitik og cookie-/samtykkehåndtering før lancering.

## Køreplan
1. **Uge 1-2:** Prototype (findes i `index.html`), test med 10 brugere
2. **Uge 3-6:** Expo-app med login, katalog, overblik, påmindelser
3. **Uge 7-8:** Tilbud + affiliate-links + sporing af klik
4. **Uge 9-10:** Premium (RevenueCat), beta-lancering i Danmark
5. **Senere:** Open Banking, prisalarmer, husstandsdeling

## Succeskriterier
- 1.000 aktive brugere inden for 3 måneder efter lancering
- Gns. 3+ abonnementer pr. bruger
- 5 % konvertering til Premium
- Gns. besparelse pr. bruger: 150 kr./år

## Kør prototypen
Åbn `index.html` i en browser – ingen installation nødvendig. Data gemmes lokalt i din browser.

> ⚠️ Priserne i prototypen er **eksempler** og skal verificeres mod tjenesternes officielle priser, før de vises til rigtige brugere.

## Bidrag
Se `docs/CONTRIBUTING.md`.

## Licens
Endnu ikke valgt (tilføj fx MIT, hvis projektet gøres open source).
