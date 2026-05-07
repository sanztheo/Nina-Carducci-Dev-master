e03509b1033bb60df16a8cd1d28e5fde0704995e - Light house "84,67,96,73" Total : 84
92e092f2a92d7c7b4cd78e72864a6b97c7c424ce  - Light House "89,78,100,82" Total : 89

---

## Optimisation SEO, Accessibilité & Performance - 2026-04-09

### Baseline après renommage images SEO + fix JS + meta tags
38f67db - Lighthouse "67,87,96,100" (Perf,Access,BP,SEO)
WAVE : 4 Errors, 3 Contrast Errors, 7 Alerts, AIM Score 6.8/10
- Erreurs WAVE : 3 labels formulaire manquants, 1 titre non informatif (corrigé), 3 contrastes faibles, 3 labels orphelins, 1 pas de landmarks, 3 sauts de niveaux de titres
- Lighthouse fails : color-contrast, heading-order, label, landmark-one-main, unsized-images

### Fix 1 - Semantic HTML (landmarks, heading hierarchy, form labels)
4af25c9 - Lighthouse "73,96,96,100" (Perf,Access,BP,SEO)
- div → header, main, section, footer, nav (landmarks WAVE)
- h3 titres → h2, h1 citations → p, h6 intro → p (hiérarchie correcte h1>h2>h3)
- Ajout for="" sur les 3 labels du formulaire (fix WAVE orphaned/missing labels)
- Accessibilité : 87 → 96 (+9), heading-order OK, label OK, landmark-one-main OK
- Reste : color-contrast (blanc sur #BEB45A), unsized-images

### Fix 2 - Contraste couleurs (WAVE contrast errors)
f28829c - Lighthouse "77,100,96,100" (Perf,Access,BP,SEO)
- .nav-pills .nav-link.active : color #fff → #000 sur fond #BEB45A
- Ratio contraste : 2.12:1 → 13.3:1 (seuil WCAG AA = 4.5:1)
- Accessibilité : 96 → 100 (+4), color-contrast OK
- WAVE : 0 Errors, 0 Contrast Errors
- Reste : unsized-images, errors-in-console (favicon 404)

### Fix 3 - Dimensions images explicites + height:auto
905d34c - Lighthouse "70,100,96,100" (Perf,Access,BP,SEO)
- Ajout width/height sur slider (1440x666), nina (560x558), camera (560x559), instagram (40x40)
- Ajout height:auto en CSS sur .carousel-item img, .picture img, .social-link img
- Fix </div> orphelin → </section> pour fermer gallery
- unsized-images : 50 → 100, image-aspect-ratio : 0 → 100, image-size-responsive : 0 → 100
- Best Practices : 88 → 96 (+8)
- Reste : errors-in-console (favicon 404), performance (LCP, FCP lents)

### Fix 4 - Preload LCP, lazy load, favicon, fetchpriority
f51f2e0 - Lighthouse "77,100,100,100" (Perf,Access,BP,SEO)
- Preload première image slider (LCP element) via <link rel="preload">
- fetchpriority="high" sur image LCP, loading="lazy" sur images below-the-fold
- Favicon vide pour supprimer erreur 404 console
- LCP : 6.6s → 5.0s, FCP : 2.7s
- Best Practices : 96 → 100, errors-in-console OK
- Reste : performance LCP encore à 5.0s (CSS render-blocking, fonts Google)

### Fix 5 - Minification CSS et JS
1f4f4a3 - Lighthouse "74,100,100,100" (Perf,Access,BP,SEO)
- bootstrap.css 201K → 160K, style.css 5K → 4K (clean-css)
- bootstrap.bundle.js 81K → 76K, maugallery.js 7K → 5K (terser)
- Référencement des fichiers .min dans index.html
- unminified-css : 0 → 100, unminified-javascript : 0 → 100
- LCP : 5.0s → 4.7s
- Reste : unused-css (Bootstrap ~153 KiB inutilisé), unused-js (jQuery ~59 KiB)

### Fix 6 - Schema.org LocalBusiness (données structurées)
433ce39 - Lighthouse "81,100,100,100" (Perf,Access,BP,SEO)
- Ajout JSON-LD Schema.org LocalBusiness (nom, adresse, tarifs, Instagram)
- Permet rich snippets Google (Knowledge Panel, résultats enrichis)
- LCP : 4.4s, FCP : 2.6s, TBT : 0ms, CLS : 0.001

---

### Résumé final

| Métrique | Baseline (38f67db) | Final (433ce39) | Gain |
|---|---|---|---|
| Performance | 67 | 81 | +14 |
| Accessibilité | 87 | 100 | +13 |
| Best Practices | 96 | 100 | +4 |
| SEO | 100 | 100 | = |
| WAVE Errors | 4 | 0 | -4 |
| WAVE Contrast | 3 | 0 | -3 |
| WAVE Alerts | 7 | 0 | -7 |
| LCP | 6.6s | 4.4s | -2.2s |

#### Corrections apportées
1. **Bug JS** - Navigation lightbox prev/next cassée (index au lieu de index±1)
2. **Meta SEO** - title, description, Open Graph, lang="fr", charset en premier
3. **HTML sémantique** - header/main/nav/section/footer, hiérarchie h1>h2>h3, labels form
4. **Contraste** - Texte blanc sur #BEB45A → noir (ratio 2.12:1 → 13.3:1)
5. **Images** - width/height explicites + height:auto CSS (CLS, aspect-ratio)
6. **Performance** - Preload LCP, fetchpriority, loading=lazy, defer scripts
7. **Minification** - CSS et JS minifiés (bootstrap, style, maugallery, scripts)
8. **Schema.org** - Données structurées LocalBusiness pour rich snippets

### Fix 7 - PurgeCSS Bootstrap + Self-host Google Fonts
a2da4d1 - Lighthouse "99,100,100,100" (Perf,Access,BP,SEO)
- PurgeCSS supprime les règles Bootstrap inutilisées : 160 KiB → 9.9 KiB
- Self-host fonts Inter + Spectral en local (élimine 3 requêtes DNS externes)
- Suppression preconnect googleapis + stylesheet externe
- LCP : 4.4s → 2.0s, FCP : 2.6s → 0.9s, SI : 2.6s → 1.0s
- Performance : 81 → 99 (+18)

---

### Résumé final (mis à jour)

| Métrique | Baseline (38f67db) | Final (a2da4d1) | Gain |
|---|---|---|---|
| Performance | 67 | 99 | **+32** |
| Accessibilité | 87 | 100 | **+13** |
| Best Practices | 96 | 100 | **+4** |
| SEO | 100 | 100 | = |
| WAVE Errors | 4 | 0 | -4 |
| WAVE Contrast | 3 | 0 | -3 |
| WAVE Alerts | 7 | 0 | -7 |
| LCP | 6.6s | 2.0s | **-4.6s** |
| FCP | - | 0.9s | - |
| TBT | - | 0ms | - |
| CLS | - | 0.001 | - |

#### Corrections apportées
1. **Bug JS** - Navigation lightbox prev/next cassée (index au lieu de index±1)
2. **Meta SEO** - title, description, Open Graph, lang="fr", charset en premier
3. **HTML sémantique** - header/main/nav/section/footer, hiérarchie h1>h2>h3, labels form
4. **Contraste** - Texte blanc sur #BEB45A → noir (ratio 2.12:1 → 13.3:1)
5. **Images** - width/height explicites + height:auto CSS (CLS, aspect-ratio)
6. **Performance** - Preload LCP, fetchpriority, loading=lazy, defer scripts
7. **Minification** - CSS et JS minifiés (bootstrap, style, maugallery, scripts)
8. **Schema.org** - Données structurées LocalBusiness pour rich snippets
9. **PurgeCSS** - Bootstrap purgé de 160 KiB à 9.9 KiB
10. **Fonts** - Google Fonts self-hosted en local (élimine latence réseau)

#### Limite restante
- unused-js : jQuery (~59 KiB) - nécessaire pour mauGallery, ne peut être retiré

---

## Correctifs UX & A11y - 2026-05-07

### Fix 8 - Contraste flèches carousel hero (WAVE)
5bf6dc4 - Pastille blanche 56px + chevron noir SVG (fill `%23111`)
- Override Bootstrap `.carousel-control-prev/next` : `border-radius:50%`, `background:#fff`, `opacity:1`
- Icônes SVG inline : data URI avec `fill='%23111'` (au lieu de `%23fff` Bootstrap)
- Hover : `scale(1.06)` + ombre renforcée
- Responsive < 600px : taille réduite à 44px
- WAVE : 1 contraste résolu sur les contrôles carousel

### Fix 9 - Reconstruction lightbox galerie
dc6b2b2 - UX modal complète, bugs structurels résolus
**Problèmes identifiés** :
1. `$(el).modal("toggle")` (jQuery interface BS5) instable → ESC + clic backdrop ne fermaient pas
2. Modal-dialog `width:auto` se redimensionnait par image → image et flèches sautaient à chaque navigation
3. Flèches enfants de `.modal-dialog` (qui reçoit `transform` Bootstrap pendant fade-in) → containing block créé par `transform` capturait les `position:fixed` (spec CSS) → flèches collées au dialog pendant l'animation, snap viewport après
4. Bootstrap ajoute `padding-right:17px` sur body à l'ouverture (compensation scrollbar) → viewport élargit → flèches `right:24px` shifaient
5. Inline styles dans markup JS empêchaient overrides CSS propres

**Corrections** :
- API native `bootstrap.Modal.getOrCreateInstance(el).show()` (au lieu jQuery interface)
- `.modal-dialog` verrouillé à `92vw × 90vh` fixe → image et UI stables peu importe ratio image
- `.mg-prev`, `.mg-next`, `.mg-close` hissés direct enfants `.modal` → aucun ancêtre transform → `position:fixed` ancré viewport dès frame 1
- `html { scrollbar-gutter: stable }` + `body.modal-open { padding-right: 0 !important }` → neutralise shift viewport
- Listener click custom sur modal : ferme si target ≠ image / flèche / close
- Bouton fermer `×` ajouté en haut à droite (`data-bs-dismiss="modal"`)
- Backdrop opacity 0.85 (lisibilité)
- Markup nettoyé : `<button>` sémantique au lieu `<div>`, plus d'inline styles
- 4 moyens de fermer : ESC, clic backdrop, clic hors image, bouton ×

### Fix 10 - Filtre galerie : état actif perdu
0ccbae3 - Classe `active` non réappliquée
- `filterByTag` retirait `active active-tag` mais ne réajoutait que `active-tag`
- CSS `.nav-pills .nav-link.active{background:#BEB45A}` jamais touché → fond olive bloqué sur "Tous"
- Fix : `addClass("active active-tag")` pour symétrie avec `removeClass`

### Fix 11 - Sources non-minifiées en dev
e0e79cb - `index.html` référence `style.css`, `maugallery.js`, `scripts.js`
- Lecture/debug en dev impossible sur fichiers minifiés
- Chaîne minification à relancer avant déploiement prod

#### Synthèse correctifs UX
| Bug | Cause racine | Correctif |
|---|---|---|
| Contraste flèches hero | SVG fill blanc sur fond clair | Pastille blanche + chevron noir |
| Modal ne se ferme pas (ESC/backdrop) | `.modal("toggle")` jQuery BS5 unreliable | API native `bootstrap.Modal` |
| Flèches teleport à l'ouverture | `transform` sur ancêtre crée containing block fixed | Flèches hissées hors `.modal-dialog` |
| Image et flèches sautent à navigation | `modal-dialog` width:auto | Box verrouillée 92vw × 90vh |
| Shift viewport à l'ouverture modal | Bootstrap `padding-right` body | `scrollbar-gutter:stable` + override |
| Filtre tags : pas de fond actif | `addClass` asymétrique avec `removeClass` | Re-ajout `active` |
| Pas de bouton fermer visible | Manque dans markup originel | Bouton × fixed top-right |
