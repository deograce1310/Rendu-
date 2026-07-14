# Guide débutant — Appliquer les textures LBP dans ArchiCAD + Enscape

## Étape 0 — Préparer les fichiers
1. Créez un dossier sur votre PC : `Documents\LBP_Textures`
2. Téléchargez-y le contenu du dossier `textures/` du dépôt (albedos + sous-dossier `PBR/`)
3. Ne renommez pas les fichiers : gardez les paires alignées (ex. `bois_noyer_horizontal.png` ↔ `PBR/bois_noyer_horizontal_normal.png`)

## Étape 1 — Créer une surface dans ArchiCAD
1. Menu **Options → Attributs élément → Surfaces…**
2. Choisissez une surface existante proche (ex. « Peinture ») → bouton **Dupliquer** → nommez-la `LBP_Damier` (une surface par texture : `LBP_Noyer_H`, `LBP_Creme`, etc.)
3. En haut du dialogue, passez le moteur sur **Cineware (CineRender)** pour voir tous les canaux
4. Canal **Couleur** : cochez « Texture » → **Charger l'image** → choisissez l'albedo (ex. `damier_bistrot_8K.png`)
5. Dans les réglages du **moteur interne**, réglez la taille de la texture :
   - Damier, noyer, papiers peints : **1800 × 1800 mm** (papiers peints/damier) ou **2000 × 2000 mm** (bois)
   - Peintures unies : **1500 × 1500 mm**
   - ⚠️ Toujours **largeur = hauteur**, sinon les motifs se déforment

## Étape 2 — Ajouter les cartes PBR (relief + matité)
Toujours dans la surface, moteur Cineware :
1. Canal **Relief (Bump)** : chargez `..._normal.png` (Enscape détecte automatiquement les normal maps, reconnaissables à leur couleur violette). Intensité : **15–20 %**
2. Canal **Réflectance** : ajoutez une couche → rugosité : chargez `..._roughness.png` si votre version accepte une image, sinon réglez la valeur à la main :
   - Bois verni : réflexion ~10 %, rugosité 40 %
   - Damier émaillé : réflexion ~15 %, rugosité 25 %
   - Peintures et papiers peints : réflexion 3–5 %, rugosité 80 %
3. **Même taille de texture** pour tous les canaux (celle de l'étape 1.5)

## Étape 3 — Appliquer la surface sur un mur
- **Méthode 1** : double-clic sur l'outil Mur → onglet **Modèle** → remplacez les surfaces (extérieure / intérieure) par votre `LBP_...`
- **Méthode 2 (rapide)** : sélectionnez le mur en 3D → Ctrl+T → Modèle → surface
- Pour un seul pan de mur, utilisez la **surcharge de surface** dans les réglages de l'élément

## Étape 4 — Caler la texture (crucial pour le damier et le mur M1)
1. Ouvrez la fenêtre 3D, sélectionnez le mur
2. Clic droit → **Aligner texture 3D → Définir origine**
3. Cliquez le **coin inférieur gauche du mur**
- Mur M1 avec cartouche menu : texture `mur_M1_damier_cartouche_HD.png` réglée **exactement à 4100 × 2800 mm** (elle EST le mur), origine coin bas-gauche obligatoire
- À refaire si vous modifiez le mur (Aligner texture 3D → Réinitialiser puis redéfinir)

## Étape 5 — La vitrophanie (logo sur vitre)
1. Créez une dalle fine (20 mm) de la taille de la vitre, collée contre elle
2. Surface dédiée `LBP_Vitrophanie` : texture `vitre_logo_200x100.png`, taille = taille de la vitre
3. Cochez **Canal alpha** dans les options de la texture : le fond transparent disparaît, seul le logo givré reste

## Étape 6 — Vérifier dans Enscape
1. Lancez Enscape (bouton ▶ dans la barre ArchiCAD) — la vue se met à jour en direct
2. Approchez-vous d'un mur en lumière rasante : vous devez voir le relief (joints du damier, veines du bois)
3. Si votre version d'Enscape a le **Material Editor** (icône sphère), vous pouvez y affiner : glissez la roughness map dans le canal *Roughness*, la normal dans *Normal*

## Étape 7 — Réglages de scène pour la boulangerie
- Spots intérieurs **3000 K** (blanc chaud) au-dessus du comptoir et du mur à pain
- Enscape → Visual Settings → **Exposure manuelle ~55–60 %**, White Balance ~3500 K
- Un rendu de nuit avec l'enseigne éclairée = l'image la plus vendeuse du dossier

## Erreurs fréquentes
| Symptôme | Cause | Remède |
|---|---|---|
| Motifs étirés | largeur ≠ hauteur de texture | remettre taille carrée |
| Le damier ne « tombe » pas juste | origine non définie | Étape 4 |
| Texture floue de près | image basse résolution | utiliser les versions 8K |
| Tout est gris dans Enscape | chemin de texture cassé | recharger l'image dans la surface |
| Trop brillant / plastique | rugosité trop basse | remonter à 40 % (bois) / 80 % (peinture) |
| Le logo vitre a un fond blanc | canal alpha non coché | Étape 5.3 |

## Correspondance fichiers → usage
| Fichier (textures/) | Où l'appliquer | Taille |
|---|---|---|
| `damier_bistrot_8K.png` | Mur vedette M1 (si sans cartouche) | 1800×1800 |
| `mur_M1_damier_cartouche_HD.png` | Mur M1 avec emplacement menu | 4100×2800 |
| `papier_peint_creme_8K.png` | Cloison M2 côté client | 1800×1800 |
| `papier_peint_bleu_nuit_8K.png` | Mur d'accent alternatif | 1800×1800 |
| `peinture_creme_artisan.png` | Murs M3/M4, plafond | 1500×1500 |
| `peinture_marine_profond.png` | Façade M5, cage d'escalier | 1500×1500 |
| `bois_noyer_horizontal.png` | Façades meuble bas | 2000×2000 |
| `bois_noyer_LBP.png` | Montants, côtés du mobilier | 2000×2000 |
| `bois_chene_rustique.png` | Plateaux, mange-debout | 1000×1000 |
| `enseigne_A_logo.png` | Bandeau façade 3,20×0,30 m | 3200×300 |
| `tableau_menu_contour_HD.png` | Menu-tableau (dalle 2 cm) | ~660×1160 |
| `vitre_logo_200x100.png` | Vitrophanie (alpha activé) | taille vitre |

Chaque albedo a ses cartes `_normal` / `_roughness` / `_height` dans `textures/PBR/` — même taille que l'albedo, toujours.
