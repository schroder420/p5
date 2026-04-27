# Kode Design Guide

**HTML / CSS / JavaScript – Project Standard**

Denne guide ligger øverst i repoet og bruges som fælles standard for, hvordan projektets kode skrives, struktureres og reviewes.

Formålet er ikke at gøre koden mere kompliceret, men at sikre at den er nem at læse, nem at rette og nem at arbejde videre på.

## 1. Core Principles

- Konsistens går foran personlig præference
- Læsbarhed går foran smart kode
- Eksisterende patterns skal følges
- Samme problem skal løses på samme måde
- Kode skal kunne forstås uden mundtlig forklaring

## 2. Formatting

Tabs bruges til indryk i HTML, CSS og JavaScript.

Der skal være tom linje mellem logiske kodeblokke, så koden er lettere at scanne.

JavaScript skal altid bruge `{}` ved `if`, loops og funktioner.

**Godt:**

```js
if (isValid) {
    doSomething();
}
```

**Dårligt:**

```js
if (isValid) doSomething();
```

## 3. File Structure

Standard struktur:

```text
/assets
/css
/js
index.html
CODE_GUIDE.md
```

Regler:

- Filnavne skrives med `kebab-case`
- Ingen mapper med navne som `misc`, `stuff`, `test` eller `new`
- CSS placeres i `/css`
- JavaScript placeres i `/js`
- Billeder, ikoner og video placeres i `/assets`
- Filer skal have et tydeligt ansvar

**Godt:**

```text
/css/style.css
/js/clock.js
/assets/images/logo.webp
```

**Dårligt:**

```text
/css/newstyle.css
/js/stuff.js
/assets/misc/image1.png
```

## 4. HTML

HTML skal bruges til struktur og indhold. Styling hører til i CSS, og funktionalitet hører til i JavaScript.

### Semantic HTML

Brug semantiske tags, når det giver mening.

```html
<header></header>
<main></main>
<section></section>
<footer></footer>
```

Regler:

- Brug kun én `<h1>` pr. side
- Brug overskrifter i korrekt rækkefølge
- HTML skal være korrekt nested
- Elementer skal lukkes korrekt
- JavaScript skrives ikke inline i HTML

**God struktur:**

```html
<main>
    <section class="project-section">
        <h2>Mine projekter</h2>
    </section>
</main>
```

**Dårlig struktur:**

```html
<div>
    <div>
        <div>Mine projekter</div>
    </div>
</div>
```

### Buttons og links

`<button>` bruges til handlinger.  
`<a>` bruges til navigation.

**Godt:**

```html
<button type="button">Åbn menu</button>
<a href="#side-om-mig">Om mig</a>
```

**Dårligt:**

```html
<div onclick="openMenu()">Åbn menu</div>
```

### Forms og inputs

Alle inputs skal have en label.  
`label` og `input` kobles med `for` og `id`.

```html
<label for="email">Email</label>
<input id="email" name="email" type="email">
```

### Images

Billeder skal have `alt`.

```html
<img src="logo.webp" alt="Logo for portfolio">
```

Hvis billedet kun er dekorativt, kan alt-teksten være tom.

```html
<img src="decoration.webp" alt="">
```

## 5. CSS

CSS skal være struktureret, læsbart og konsekvent. Der er ikke én fast rækkefølge for properties, men relaterede properties skal samles logisk.

### Naming

CSS-klasser skrives med `kebab-case`.

**Godt:**

```css
.hero-section {}
.project-card {}
.gallery-item {}
```

**Dårligt:**

```css
.box {}
.bigBox {}
.red-text {}
.thing {}
```

Regler:

- Navne skal beskrive funktion eller rolle
- Undgå generiske navne som `.box`, `.thing`, `.stuff` og `.container2`
- Undgå navne der kun beskriver udseende, fx `.red-text`
- Ens komponenter skal navngives ens

## 6. BEM-light

Projektet bruger en simpel BEM-inspireret navngivning.

Format:

```text
block
block-element
block--modifier
```

Eksempel:

```css
.card {}
.card-title {}
.card--highlighted {}
```

Betydning:

- `block` er selve komponenten
- `block-element` er en del af komponenten
- `block--modifier` er en variation af komponenten

Eksempel i HTML:

```html
<article class="project-card project-card--featured">
    <h2 class="project-card-title">Portfolio</h2>
    <p class="project-card-text">Et kodet portfolio-projekt.</p>
</article>
```

BEM-light bruges for at gøre navne tydelige uden at gøre syntax unødvendigt tung.

## 7. Component + Effect Classes

Komponentklasser og effektklasser må kombineres.

```html
<div class="project-card glass-box"></div>
```

Regel:

- Komponentklassen beskriver elementets rolle
- Effektklassen beskriver visuel styling

Eksempel:

```html
<a class="content-box glass-box" href="#side-kodning">
    <span class="content-box-title">Kodning</span>
</a>
```

Her er `content-box` komponenten, mens `glass-box` er en genbrugelig visuel effekt.

Effektklasser må ikke overtage komponentens struktur. De bør primært styre visuelle ting som baggrund, border, shadow, blur eller radius.

## 8. CSS Structure

CSS skrives i logiske blokke. Der er ikke krav om en bestemt property-rækkefølge, men koden skal være konsekvent og nem at scanne.

**Godt:**

```css
.card {
    display: flex;
    gap: 16px;

    padding: 24px;

    background: white;
    border-radius: 12px;
}
```

**Dårligt:**

```css
.card {
    background: white;
    display: flex;
    border-radius: 12px;
    gap: 16px;
    padding: 24px;
}
```

Regler:

- Relaterede properties samles
- Ens komponenter struktureres ens
- Undgå unødvendig dyb selector-nesting
- Undgå `!important`, medmindre der er en klar grund

**Dårligt:**

```css
.page .wrapper .card .title {
    color: white;
}
```

**Bedre:**

```css
.card-title {
    color: white;
}
```

## 9. JavaScript

JavaScript skal bruges til funktionalitet, events og dynamisk adfærd. JavaScript skal ikke ligge inline i HTML.

### Basic structure

```js
const form = document.querySelector("#form");

form.addEventListener("submit", handleSubmit);

function handleSubmit(event) {
    event.preventDefault();
}
```

Regler:

- Brug `camelCase` til variabler og funktioner
- Brug `const` som default
- Brug `let` når værdien ændrer sig
- Brug aldrig `var`
- Én funktion skal have ét ansvar
- Funktioner skal være korte og tydelige
- JavaScript placeres i separate filer i `/js`
- Inline scripts i HTML undgås

### Naming in JavaScript

**Dårligt:**

```js
let x;
let data;
let thing;
```

**Godt:**

```js
const userEmail;
const formElement;
const submitButton;
```

Navne skal gøre det tydeligt, hvad variablen bruges til.

### Event listeners

Events tilføjes i JavaScript, ikke direkte i HTML.

**Dårligt:**

```html
<button onclick="openMenu()">Menu</button>
```

**Godt:**

```html
<button id="menuButton" type="button">Menu</button>
```

```js
const menuButton = document.querySelector("#menuButton");

menuButton.addEventListener("click", openMenu);
```

## 10. Components

Gentagne elementer behandles som komponenter.

Hvis samme struktur bruges flere steder, skal naming og markup være ens.

```html
<a class="content-box glass-box" href="#side-kodning">
    <div class="content-box-inner">
        <span class="content-box-title">Kodning</span>
        <span class="content-box-subtitle">Mine kodeprojekter</span>
    </div>
</a>
```

Regler:

- Ens komponenter skal have ens struktur
- Genbrug struktur før du kopierer og ændrer tilfældigt
- Komponentnavne skal være tydelige
- Komponenter må gerne kombineres med effektklasser

## 11. Performance

Performance handler om at undgå unødvendig belastning, især ved billeder, video og JavaScript.

### Images

```html
<img src="project.webp" alt="Projektbillede" loading="lazy" decoding="async">
```

Regler:

- Brug `loading="lazy"` på billeder, der ikke er kritiske ved første load
- Brug `decoding="async"` hvor det giver mening
- Brug optimerede billedformater som `.webp`
- Undgå unødvendigt store billeder

### Video

```html
<video autoplay muted loop playsinline preload="none">
    <source src="background.webm" type="video/webm">
</video>
```

Regler:

- Brug `preload="none"` på tunge videoer, hvor videoen ikke skal loades med det samme
- Brug fallback-billede ved vigtige visuelle videoer
- Undgå at afspille tunge videoer unødvendigt på mobile enheder

### JavaScript performance

Regler:

- Gem DOM queries i variabler
- Undgå at querye samme element igen og igen
- Brug CSS til visuelle effekter, når JavaScript ikke er nødvendigt

**Dårligt:**

```js
document.querySelector("#menu").classList.add("is-open");
document.querySelector("#menu").style.opacity = "1";
```

**Bedre:**

```js
const menu = document.querySelector("#menu");

menu.classList.add("is-open");
```

## 12. Accessibility

Accessibility betyder, at siden skal kunne bruges af så mange som muligt.

Regler:

- Brug semantic HTML
- Brug labels på inputs
- Brug meningsfuld alt-tekst på billeder
- Interaktive elementer skal kunne bruges med mus og keyboard
- Designvalg må ikke gøre siden unødvendigt svær at bruge
- Farver og kontrast skal være læsbare

Viewport standard:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Hvis viewport ændres af designmæssige årsager, skal det være et bevidst valg og ikke en standardløsning.

## 13. Do / Don’t

### HTML

**Dårligt:**

```html
<div onclick="submitForm()">Send</div>
```

**Godt:**

```html
<button id="submitButton" type="submit">Send</button>
```

### CSS

**Dårligt:**

```css
.big-box {}
```

**Godt:**

```css
.hero-section {}
```

### JavaScript

**Dårligt:**

```js
let x = document.querySelector(".x");
```

**Godt:**

```js
const submitButton = document.querySelector("#submitButton");
```

## 14. Review Rules

Review bruges for at sikre, at koden følger projektets standard og kan overtages af andre.

### Før commit

Tjek:

- Følger koden naming-reglerne?
- Matcher strukturen resten af projektet?
- Er der ubrugt kode?
- Er HTML korrekt struktureret?
- Er JavaScript opdelt i klare funktioner?
- Er CSS opdelt i logiske sektioner?
- Er der inline JavaScript, som bør flyttes?

### Ved review

Spørg:

- Kan koden forstås uden forklaring?
- Er der genbrug fremfor unødvendig kopiering?
- Er HTML, CSS og JavaScript adskilt?
- Følger løsningen eksisterende patterns?
- Er der noget, der bør refactores?

### Kode bør afvises hvis

- Navngivningen er uklar
- Strukturen er rodet
- Der er inline JavaScript uden tydelig grund
- Der er quick fixes uden kommentar
- Koden bryder eksisterende patterns
- Koden er svær at læse uden forklaring

## 15. Final Rule

> Hvis koden ikke er let at læse, skal den refactores.
