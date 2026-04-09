e03509b1033bb60df16a8cd1d28e5fde0704995e - Light house "84,67,96,73" Total : 84
92e092f2a92d7c7b4cd78e72864a6b97c7c424ce  - Light House "89,78,100,82" Total : 89

---

## Optimisation SEO, Accessibilité & Performance — 2026-04-09

### Baseline après renommage images SEO + fix JS + meta tags
38f67db - Lighthouse "67,87,96,100" (Perf,Access,BP,SEO)
WAVE : 4 Errors, 3 Contrast Errors, 7 Alerts, AIM Score 6.8/10
- Erreurs WAVE : 3 labels formulaire manquants, 1 titre non informatif (corrigé), 3 contrastes faibles, 3 labels orphelins, 1 pas de landmarks, 3 sauts de niveaux de titres
- Lighthouse fails : color-contrast, heading-order, label, landmark-one-main, unsized-images

### Fix 1 — Semantic HTML (landmarks, heading hierarchy, form labels)
4af25c9 - Lighthouse "73,96,96,100" (Perf,Access,BP,SEO)
- div → header, main, section, footer, nav (landmarks WAVE)
- h3 titres → h2, h1 citations → p, h6 intro → p (hiérarchie correcte h1>h2>h3)
- Ajout for="" sur les 3 labels du formulaire (fix WAVE orphaned/missing labels)
- Accessibilité : 87 → 96 (+9), heading-order OK, label OK, landmark-one-main OK
- Reste : color-contrast (blanc sur #BEB45A), unsized-images

### Fix 2 — Contraste couleurs (WAVE contrast errors)
f28829c - Lighthouse "77,100,96,100" (Perf,Access,BP,SEO)
- .nav-pills .nav-link.active : color #fff → #000 sur fond #BEB45A
- Ratio contraste : 2.12:1 → 13.3:1 (seuil WCAG AA = 4.5:1)
- Accessibilité : 96 → 100 (+4), color-contrast OK
- WAVE : 0 Errors, 0 Contrast Errors
- Reste : unsized-images, errors-in-console (favicon 404)
