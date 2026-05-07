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

#### 1. Bug de navigation dans la galerie photo
La flèche « suivante » dans la visionneuse d'image renvoyait sur la même image. Corrigé : les flèches naviguent désormais correctement.

#### 2. Référencement Google
Ajout des balises essentielles (titre, description, image de partage Facebook/Twitter, langue française). La page est maintenant correctement comprise par Google et les réseaux sociaux.

#### 3. Structure de la page lisible par les lecteurs d'écran
La page utilisait des balises génériques (`div`) partout. Remplacées par des balises sémantiques (`header`, `main`, `nav`, `section`, `footer`) que les technologies d'assistance (lecteurs d'écran pour personnes malvoyantes) reconnaissent. Hiérarchie des titres (h1, h2, h3) corrigée. Libellés de formulaire associés à leurs champs.

#### 4. Contraste des couleurs
Le texte blanc sur fond olive ne respectait pas les normes d'accessibilité (WCAG AA). Passé en noir : ratio de contraste passé de 2,1:1 à 13,3:1, bien au-dessus du seuil requis (4,5:1).

#### 5. Dimensions des images
Les images n'avaient pas de dimensions déclarées dans le code, ce qui faisait sauter la mise en page pendant le chargement. Dimensions ajoutées : la page se stabilise immédiatement.

#### 6. Vitesse de chargement
- **Préchargement** de l'image principale du carousel (la première vue)
- **Chargement différé** des images plus bas dans la page (chargées seulement quand l'utilisateur défile)
- **Compression** des fichiers de style et de script (CSS et JavaScript réduits à l'essentiel)
- **Polices d'écriture** hébergées localement plutôt que chargées depuis Google (élimine 3 connexions réseau externes)
- **Bibliothèque Bootstrap** allégée : passée de 160 Ko à 10 Ko en supprimant le code inutilisé

#### 7. Présence Google enrichie
Ajout de données structurées (Schema.org) qui permettent à Google d'afficher la fiche entreprise de Nina Carducci dans ses résultats : adresse, tarifs, lien Instagram, type d'activité (photographe locale à Bordeaux).

#### 8. Favicon
Erreur 404 dans la console résolue.

---

### Phase 2 — Corrections UX et accessibilité (mai 2026)

#### 9. Flèches du carousel d'accueil illisibles
Les flèches « précédent / suivant » du grand carousel d'accueil étaient blanches sur fond clair → invisibles, signalées par WAVE. Remplacées par des **boutons ronds blancs avec une flèche noire** au centre, ombrés. Lisibles et élégantes.

#### 10. Visionneuse d'image (lightbox) repensée entièrement
Plusieurs problèmes corrigés en une fois :

- **Touche Échap (ESC) ne fermait pas la fenêtre** → corrigé
- **Cliquer en dehors de l'image ne fermait pas** → corrigé (clic sur le fond sombre ferme)
- **Flèches qui « sautaient » à l'ouverture** → corrigé (elles restent fixes aux bords de l'écran)
- **Image et flèches qui se décalaient à chaque changement de photo** → corrigé (la zone d'affichage est verrouillée à une taille stable)
- **Pas de bouton « Fermer »** → ajouté un bouton **×** en haut à droite

Au final, **4 façons de fermer** la fenêtre image : touche Échap, clic sur le fond noir, clic hors de l'image, bouton ×.

#### 11. Filtre des catégories de photos
Le menu « Tous / Concert / Entreprises / Mariages / Portrait » ne mettait pas en surbrillance la catégorie sélectionnée — elle restait toujours sur « Tous ». Corrigé : la catégorie active est désormais bien marquée en olive.

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
