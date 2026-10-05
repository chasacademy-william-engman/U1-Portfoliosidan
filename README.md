# U1-Portfoliosidan

- Github sidan: https://chasacademy-william-engman.github.io/U1-Portfoliosidan/

- **Från skiss till kod.** Hur gick du tillväga? Var det något i skissen som var svårt att översätta till HTML och CSS, och hur löste du det?

Jag började med mobillayouten enligt mobile first och anpassade den sedan till desktop med @media. Det svåra var att mobilbilderna i Figma var skärmdumpar, så jag kunde inte läsa av exakta mått som på desktop. Jag löste det genom att uppskatta storlekar utifrån andra element. Till exempel såg jag att bilden på index.html tog halva sidbredden eftersom den var i linje med den centrerade LinkedIn-ikonen. Dark mode var också svårt, eftersom skissen inte visade hur det skulle slås på. Lösningen blev prefers-color-scheme, som jag tar upp under AI-verktyg.

- **Semantik.** Vilka HTML-element valde du för sidans olika delar, och varför just de? Var landade du i ett `div` för att inget bättre fanns?

Alla sidor har en **header** med en **nav**. Nav gör att skärmläsare kan hoppa direkt till menyn, och länkarna ligger i en **ul** så att det läses upp som en lista med fem val som inte behöver vara i ordning. De sociala ikonerna har aria-label, eftersom en ikon utan text annars saknar namn. Mobilmenyn byggde jag med **details** och **summary**, eftersom de skapar en fällbar meny utan JavaScript och fungerar med tangentbord.
Innehållet ligger i **main**, så att man kan hoppa förbi menyn direkt till det viktiga. **Section** använder jag för delar med egen rubrik, som "Work Experience", eftersom rubriken då beskriver vad delen innehåller. Varje anställning och utbildning är en **article** eftersom de kan läsas fristående. Datumen ligger i **time** med datetime="2026-03" så att de blir maskinläsbara, men "Present" är inget giltigt datum och står som vanlig text. **Address** markerar kontaktuppgifterna som just kontaktuppgifter. Alla sidor utom index.html har en **footer** enligt skissen, vilket jag lade till.´

**Div** använder jag bara för layout, som .container och Grid- och Flexbox-strukturer. Där finns inget innehåll att beskriva, och en div säger ingenting till skärmläsare.

- **Layout.** Var använde du Flexbox, var använde du Grid, och vad avgjorde valet? Hur gjorde du sidan responsiv, och varför lade du brytpunkterna där du gjorde?

Jag använde **Flexbox** när innehållet bara behövde placeras i en riktning, exempelvis navigationen som går från kolumn på mobil till rad på desktop. Även sidan är Flexbox där body har min-height: 100vh och .container har flex: 1, så att footern hamnar längst ner. I projektkorten placerar margin-block: auto länkarna längst ner. **Grid** använde jag när innehållet behövdes i både rader och kolumner. Teknikikonerna använder repeat(4, minmax(0, 100px)), vilket ger lika stora rutor som bryts till nya rader. I .career ligger titel och "Full Time" i två kolumner medan hr sträcker sig över hela raden med grid-column: 1 / -1. Sidan är mobile first, så grunden gäller för mobil och @media (min-width: 1270px) skriver över dem för desktop. Brytpunkten 1270px valde jag eftersom h1 och bilden på index.html då fick plats bredvid varandra, samtidigt som navigeringen inte krockade med logotypen. Alltså utifrån Stephen hays: "Expand until it looks like shit. Time for a breakpoint!"

- **Tillgänglighet.** Vad har du gjort för att sidan ska gå att använda för fler? Hur testade du det, och vad visade testet? Vad återstår?

Jag testade med W3C:s validator, WAVE plugin i Chrome och genom att navigera med tangentbord, där fokuserade element fick tydliga linjer. WAVE hittade kontrastproblem med "Full Time", så jag använde en mörkare textfärg än i Figma. Validatorn hittade strukturfel, som att "present" låg i time och att jag hade en rubrik i address. Dessa åtgärdade jag. Validatorn gav också fel på nästlad CSS som fungerar, troligen för att den inte fullt ut stödjer modern CSS. Det som återstår är att länkarna till GitHub, Twitter och LinkedIn pekar på #. Dessutom är "Full Time" en button, eftersom Figma angav en knappfärg. Den borde vara en span, eftersom den inte har någon knappfunktion men ändå går att tabba till.

- **Användbarhet.** Vilka UX- eller UI-principer känner du igen i Pawans design? Är det något du hade gjort annorlunda, och varför?

En tydlig princip i Pawans design är konsekvens. Alla sidor har samma header och navigation, så användaren lär sig navigeringen en gång. Logotypen uppe till vänster leder hem, precis som på de flesta webbplatser. Hierarkin syns genom rubrikernas storlek och gradienten som lyfter fram namnet. Dark mode anpassas efter användarens systeminställning. Jag valde separata sidor även på mobil eftersom menyn då fungerade likadant på alla skärmar. Jag hade också visat samma kontaktinformation på desktop som på mobil, och markerat vilken sida användaren är på i navigationen så att det blir lättare att veta var man är.

- **Styrkor och brister.** Vad blev bra, och vad skulle du bygga om med mer tid?

Jag är nöjd med att färgerna ligger som variabler i :root, vilket gjorde dark mode enkelt. Jag är också nöjd med hur jag kombinerade Grid och Flexbox, till exempel att samma nav ul går från kolumn till rad med en enkel CSS-ändring. Med mer tid skulle jag lägga till en brytpunkt för surfplattor och minska den dubblerade HTML:en. Header och meny finns på varje sida och i separata versioner för mobil och desktop, där mycket döljs med display: none.

- **AI-verktyg.** Om du använt dem: till vad, och vad ändrade du i det som genererades?

Jag använde AI för förklaringar och lösningsförslag på min nivå. AI föreslog details och summary för mobilmenyn, så jag slapp JavaScript och den gav förslag på prefers-color-scheme för dark mode. Eftersom färgerna redan låg i :root behövde jag bara skriva över dem. AI föreslog även filter: invert(1) för svarta ikoner som gjorde dem vita i dark mode. Senare gjorde jag om de sociala ikonerna till SVG-element och använde fill, men behöll invert på teknikikonerna eftersom de laddas som img och CSS inte kommer åt deras fill. AI förklarade också gradienttext: background-clip: text klipper bakgrunden efter bokstäverna och color: transparent låter gradienten synas. Själv lade jag gradienterna som variabler i :root så att de återanvänds på alla sidor. AI gav också förslag på line-clamp, som kapar projektbeskrivningarna till två rader på mobil och fem på desktop i project card och jag lade själv till min-height: calc(1.5em \* 2) så att korten blir lika höga.
När jag fastnade använde jag AI för felsökning. Projektkorten fick olika bredder med Flexbox, och AI föreslog Grid. Jag valde Grid runt korten eftersom repeat(3, 1fr) ger lika breda kolumner, och Flexbox inuti eftersom innehållet bara går uppifrån och ner. I mobilheadern hamnade menyn bredvid logotypen. AI föreslog att lägga dem i samma grid-row med details över hela bredden via grid-column: 1 / -1, så att hamburgerikonen står på logotypens rad medan menyn får hela bredden under.
