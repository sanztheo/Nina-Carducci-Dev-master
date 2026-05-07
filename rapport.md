# Rapport d'optimisation — Site Nina Carducci

Site audité avec deux outils standards :
- **Lighthouse** (Google) : note de 0 à 100 sur 4 axes — performance, accessibilité, bonnes pratiques, référencement (SEO)
- **WAVE** : détecteur d'erreurs d'accessibilité (contrastes, structure, libellés)

---

## Résultats globaux

| Critère | Avant | Après | Évolution |
|---|---|---|---|
| Performance (vitesse) | 67 / 100 | **99 / 100** | +32 points |
| Accessibilité | 87 / 100 | **100 / 100** | +13 points |
| Bonnes pratiques | 96 / 100 | **100 / 100** | +4 points |
| Référencement (SEO) | 100 / 100 | **100 / 100** | Inchangé |
| Erreurs WAVE | 4 | **0** | Résolues |
| Erreurs de contraste | 3 | **0** | Résolues |
| Alertes WAVE | 7 | **0** | Résolues |
| Temps d'affichage de la page | 6,6 s | **2,0 s** | 3× plus rapide |

---

## Ce qui a été corrigé

### Phase 1 — SEO, accessibilité, performance (avril 2026)

#### 1. Bug de navigation dans la galerie photo — `c816bfb`
La flèche « suivante » dans la visionneuse d'image renvoyait sur la même image. Corrigé : les flèches naviguent désormais correctement.

#### 2. Référencement Google — `38f67db`
Ajout des balises essentielles (titre, description, image de partage Facebook/Twitter, langue française). La page est maintenant correctement comprise par Google et les réseaux sociaux.

#### 3. Structure de la page lisible par les lecteurs d'écran — `4af25c9`
La page utilisait des balises génériques (`div`) partout. Remplacées par des balises sémantiques (`header`, `main`, `nav`, `section`, `footer`) que les technologies d'assistance (lecteurs d'écran pour personnes malvoyantes) reconnaissent. Hiérarchie des titres (h1, h2, h3) corrigée. Libellés de formulaire associés à leurs champs.

#### 4. Contraste des couleurs — `f28829c`
Le texte blanc sur fond olive ne respectait pas les normes d'accessibilité (WCAG AA). Passé en noir : ratio de contraste passé de 2,1:1 à 13,3:1, bien au-dessus du seuil requis (4,5:1).

#### 5. Dimensions des images — `905d34c`
Les images n'avaient pas de dimensions déclarées dans le code, ce qui faisait sauter la mise en page pendant le chargement. Dimensions ajoutées : la page se stabilise immédiatement.

#### 6. Vitesse de chargement
- **Préchargement** de l'image principale du carousel + **chargement différé** des images plus bas + favicon (erreur 404 résolue) — `f51f2e0`
- **Compression** des fichiers CSS et JavaScript — `1f4f4a3`
- **Polices** hébergées localement (Inter + Spectral) + **Bootstrap** allégé de 160 Ko à 10 Ko — `a2da4d1`

#### 7. Présence Google enrichie — `433ce39`
Ajout de données structurées (Schema.org) qui permettent à Google d'afficher la fiche entreprise de Nina Carducci dans ses résultats : adresse, tarifs, lien Instagram, type d'activité (photographe locale à Bordeaux).

---

### Phase 2 — Corrections UX et accessibilité (mai 2026)

#### 8. Flèches du carousel d'accueil illisibles — `5bf6dc4`
Les flèches « précédent / suivant » du grand carousel d'accueil étaient blanches sur fond clair → invisibles, signalées par WAVE. Remplacées par des **boutons ronds blancs avec une flèche noire** au centre, ombrés. Lisibles et élégantes.

#### 9. Visionneuse d'image (lightbox) repensée entièrement — `dc6b2b2`
Plusieurs problèmes corrigés en une fois :

- **Touche Échap (ESC) ne fermait pas la fenêtre** → corrigé
- **Cliquer en dehors de l'image ne fermait pas** → corrigé (clic sur le fond sombre ferme)
- **Flèches qui « sautaient » à l'ouverture** → corrigé (elles restent fixes aux bords de l'écran)
- **Image et flèches qui se décalaient à chaque changement de photo** → corrigé (la zone d'affichage est verrouillée à une taille stable)
- **Pas de bouton « Fermer »** → ajouté un bouton **×** en haut à droite

Au final, **4 façons de fermer** la fenêtre image : touche Échap, clic sur le fond noir, clic hors de l'image, bouton ×.

#### 10. Filtre des catégories de photos — `0ccbae3`
Le menu « Tous / Concert / Entreprises / Mariages / Portrait » ne mettait pas en surbrillance la catégorie sélectionnée — elle restait toujours sur « Tous ». Corrigé : la catégorie active est désormais bien marquée en olive.

#### 11. Sources non-minifiées en développement — `e0e79cb`
Bascule des fichiers CSS/JS vers leurs versions lisibles pour faciliter la maintenance. La compression sera relancée avant déploiement en production.

---

## Synthèse des bénéfices

| Bénéfice | Impact concret |
|---|---|
| Site **3× plus rapide** | Visiteurs ne quittent pas la page avant chargement |
| **100/100 accessibilité** | Conforme aux standards légaux (WCAG AA), accessible aux personnes en situation de handicap |
| **Fiche entreprise Google enrichie** | Visibilité accrue dans les résultats de recherche |
| **Visionneuse photo fluide et fermable** | Expérience utilisateur naturelle et sans frustration |
| **Carousel d'accueil lisible** | Navigation visible quel que soit l'arrière-plan |

---

## Limite restante

La bibliothèque jQuery (~59 Ko) ne peut pas être retirée : elle est requise par la galerie photo (mauGallery). Une réécriture complète sans jQuery serait possible mais hors périmètre de l'optimisation actuelle.
