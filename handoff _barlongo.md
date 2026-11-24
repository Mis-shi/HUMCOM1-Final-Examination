# HANDOFF.md 

Mishigel Barlongo 

github.com/username/HUMCOM1-Final-Examination 

username.github.io/HUMCOM1-Final-Examination/ 

# 1. Overview 

Product Description 

A 5-page static website. It provides advice for new hamster owners. It is coded in plain HTML and CSS and does not include a CSS framework. Basic JavaScript is used for the age calculator, background music and contact modal. 

Pages: 

Page | Summary 

--- | --- 

index.html | Hero section with a heading. Navigation links to main guides and fast hamster facts. 

about.html | Site aims; my details; my 4 pets and point of contact. 

hamstersbreeds.html | Breed comparison cards. 

foodguide.html | Lists of suitable and unsuitable food and feeding advice. 

habitatandcare.html | Optimal cage contents including bedding, wheel and cleaning. 

User need 

New hamster owners need to be able to answer "what do I feed it?" "what cage do I need?" and ‘what breed is right for me?’ in one click from the homepage. Each page concentrates on a single topic. As well as being succinct, this enables rapid skimming. 

# 2. Structure and Semantics 

Structure 

All pages share the same structure of: header (which includes a ‘Main navigation’ landmark nav); main section; and footer. Each page has one heading (h1). Sections of content are labelled with h2. Screen readers can therefore follow the heading hierarchy (from h1 to h2). 

# Why? 

Landmark tags (header, nav, main and footer) allow screen reader software to skip directly to the relevant part of a page. Plain divs would not provide such semantic structure. 

The aria-current="page" attribute is used to identify which nav link is currently selected. Again, this is also what causes the visual emphasis to occur (via the CSS code .main-nav a[aria-current="page"]). Thus the visual and screen reader experience will always remain aligned. 

The nav landmark is labelled ‘Main navigation’ with aria-label="Main navigation". 

Decorative graphics (emojis, hamsters and sparkles) include aria-hidden="true" as they do not convey any information. Without this screen readers would vocalise them. 

Images that contain information (such as those of my pets) have appropriately descriptive alt attributes. Purely decorative images have empty alt attributes. 

For the modal popup, role="dialog" and aria-labelledby are implemented. Each form input has a label defined with for. Native form validation (required and/or maxlength) is also employed, and this is done prior to script execution. 

Each page includes the html lang="en" and viewport meta tags. 

Known limitation 

Whilst the popup is constructed using the CSS :target pseudo-class (thus requiring no JavaScript), this means that it does not constitute a focusable area. Further, because it is hidden with display:none until targeted, it never becomes part of the tab sequence. So someone accessing it using their keyboard can tab directly from the popup back to the underlying page. As I did not implement a JavaScript solution to create a focusable area, I am being honest in noting this limitation. 

# 3. Colour and Labelling 

Structure 

All colour variables are grouped together in the style.css stylesheet. At the top of the file they are defined in :root. These are: --orange #E8A04D, --orange-dark #B5651D, --accent #A8527B, --cream #FFF6EA, --pink #F0B3B3, --brown #3A2415, --muted #6B5A4A, --green #7AA45A and --red #D9455A. Following this, separate comment headings organise the rest of the file. These relate to page colours; navigation; general layout; cards; buttons; page sections; footer; and animation. 

Colour Variables 

Variable | Colour | Use 

--- | --- | --- 

--orange | #E8A04D | Header 

--orange-dark | #B5651D | Footer 

--accent | #A8527B | Navigation links, statistics and my avatar graphic 

--cream | #FFF6EA | Page background and boxes 

--pink | #F0B3B3 | Card top border and stripe background 

--brown | #3A2415 | Body text and dark buttons 

--muted | #6B5A4A | Sub-text and .tag labels 

--green | #7AA45A | Suitable food 

--red | #D9455A | Unsuitable food 

Page Colours 

Each page adds its own --c and --bg variables to its main section. For instance .c-food{-c:#5E9A3F;--bg:#E2F0D8} and .c-habitat{--c:#3E86C6;--bg:#DCEBF8}. Sections (for example the cards, tags and borders) then access these with border-top-color:var(--c) and background:var(--bg). This means that applying a single class to a page’s main section can simultaneously alter all cards, tags and borders on that page. Modifying .c-habitat{--c:#3E86C6} in the DevTools will therefore affect all of that page’s cards (borders), tag badges, cage and wheel. 

# Labelling 

Colour variables are labelled with --role. Classes are predominantly descriptive and are also limited in scope (for example .main-nav, .breed-card, .pill-list, .cage, .modal-x, .hamster-track). There is also a small BEM-inspired element of scoping for parts of the navigation and cards (for example .sitenav__link--active, .card__title, .pet__photo). Ideally, one class is used for one styling instruction so as to ensure consistent, low-specificity styling. Individual components can then be styled independently without adversely affecting others. 

# Literal data 

Whilst most components access colour information from variables, there are instances where actual data is retained. This is deliberately so for: 

Page background colours (#FDE1E8, #EADBC8, #E2F0D8, #DCEBF8, #EEE6F8) – each page has a different one so that the 5 pages all appear differently. 

Header gradient end colours (#F2B068 and #E8A04D) and the colours for the sleep card and hero section (#FFF5F8, #FDEAEF, #FFF9FB, #F1E2FA) are unique to these components. 

Border and stroke width measurements (1px, 2px and 3px) are also literal. Radii for the cage illustration are .05em and .07em so that they scale with the illustration. 

# Breakpoints 

Although CSS does not permit variables to be included within @media queries, the two required layout breakpoints are again specified as literals. These are: 900px (from a multi-column to a vertical arrangement); and 560px (whereby the navigation text transforms into icons and grids become single column). Additionally, there is a landscape phone orientation query for screens with a max height of 500px. Rather than replicating the exact dimensions of devices, I identified these breakpoints by altering the window size and noting when the layout was no longer ideal. Three columns became too slim for card text at 900px. And the navigation pill buttons began to overflow at 560px. 

Responsive methods 

Font, padding and illustration sizing are all controlled using clamp(). For example .hero h1{fontsize:clamp(1.8rem,min(5.6vh,3.6vw),4rem)}. The cage illustration size is also clamped using -- s:clamp(40px,min(8.5vh,6vw),90px). Columns are created with fr units. Images are made to fit within their areas using max-width:100%; height:auto;. The navigation benefits from flex-wrap so that it can re-flow. 

Navigation text is styled responsively using solely CSS. 

Testing the 320-1920px range 

Chrome DevTools responsive viewports were utilised at 320, 375, 768, 1024, 1366 and 1920px. 

The viewport was then dragged from 320 to 1920, observing for the appearance of a horizontal scrollbar. 

At each viewport size, the console was used to execute document.documentElement.scrollWidth > innerWidth. This returned false at all sizes bar those where an ornamental absolutely-positioned sparkle was outside of its container. This is why overflow:hidden is applied to these containers. Finally, the live GitHub Pages version of the site was also tested, not just the localhost version. 

Problems and solutions uncovered 

Problem | Solution | Reason 

--- | --- | --- 

Form text field had no autocomplete attribute | Added autocomplete="name"/"email"/"off" to popup form | The console logged an error: “An element doesn't have an autocomplete attribute”. As Lighthouse identifies whether or not this rule is met, one form text field is responsible for dragging down the a11y score. 

# | | 

Page CLS affected by image and video loading | Set aspect-ratio on ornamental image containers and defined fixed-size images for the hero and avatar sections | Cumulative Layout Shift is one of 3 factors that influence the Performance score. 

# | | 

Navigation music button was purely iconographic | Added aria-label="Music on/off" | Navigation link and button text needs to be legible. 

# | | 

Ornamental emojis were vocalised by screen readers | Added aria-hidden="true" to each ornamental span, hamster and sparkle | These items do not hold information and were disrupting the reading sequence. 

# | | 

Selected navigation item was only highlighted visually | Both visual and screen reader emphasis are determined by aria-current="page" | Visual indication alone is inadequate. 

Manual checks were also performed to confirm that body text, .tag and navigation link colours conformed to good contrast ratios; that image alts were appropriate; and that navigation link and button text was legible. Form input labels were verified and the html lang attribute checked. Heading hierarchy was examined on all 5 pages. 

Ongoing constraints 

Background music can be distracting. However, it does not auto-play and there is a visual mute option which comes into effect following a user’s initial interaction with the site. 

The about page video does not account for the prefers-reduced-motion media query. Whilst the global media query does address CSS animation, it does not apply to the  element. This is indeed an issue and I am documenting it, even though I have not resolved it. 

The :target popup is not focusable and does not even enter the tab sequence until it is targeted. 

prefers-reduced-motion is acknowledged for all animated components on the site. These are: footer hamsters; cage scene; ornamental lines; sparkles and music button. The video is the one exception. 

As noted above, because variables cannot be accessed within @media queries, the 900px and 560px breakpoints are specified as literals. 

Git History 

1. feat: Develop 5-page HAMVEN product incorporating common header, nav and footer 

2. style: Introduce colour variables to :root and also --c and --bg for individual pages 

3. fix: Conceal footer hamster overflow to avoid horizontal scrollbar 

4. a11y: Implement aria-current on navigation; add aria-hidden to ornamental graphics; and attach labels to form inputs 

5. feat: Develop CSS-only popup using :target. Native form validation is also included. 

6. refactor: Convert fixed colour data to var(--token) for cards and buttons 

7. fix: Add autocomplete to popup form fields following Lighthouse a11y audit 



<!-- Start of picture text -->
8 Lighthouse Scoring Calculator<br>oe : = = TN<br><!-- End of picture text -->

Live server- <u><mark>https://mis-shi.github.io/HUMCOM1-Final-Examination/</mark></u> 

Repository- https://github.com/Mis-shi/HUMCOM1-Final-Examination.git 

