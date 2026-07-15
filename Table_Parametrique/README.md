# Table paramétrique — Objet bibliothèque ArchiCAD (.gsm)

Objet GDL complet : une **table paramétrique** (plateau + 4 pieds) avec dimensions,
matériaux et interface de réglage personnalisée.

> ⚠️ **Pourquoi pas de fichier `.gsm` directement dans ce dépôt ?**
> Le format `.gsm` est un format **binaire propriétaire** de GRAPHISOFT : seul
> ArchiCAD (ou son outil officiel `LP_XMLConverter`) peut le générer. Ce dossier
> contient donc le **code source GDL** de l'objet, avec deux méthodes simples
> pour obtenir le `.gsm` en moins de 5 minutes.

## Contenu du dossier

| Fichier | Rôle |
|---|---|
| `Table_Parametrique.xml` | Source complète au format XML de LP_XMLConverter (conversion automatique en `.gsm`) |
| `scripts/master.gdl` | Script maître (valeurs dérivées, garde-fous) |
| `scripts/3d.gdl` | Script 3D (plateau + 4 pieds + points chauds) |
| `scripts/2d.gdl` | Script 2D (symbole en plan) |
| `scripts/vl.gdl` | Script paramètres (bornes des valeurs) |
| `scripts/ui.gdl` | Script interface (boîte de dialogue personnalisée) |

## Méthode 1 — Conversion automatique avec LP_XMLConverter (recommandée)

`LP_XMLConverter` est livré avec ArchiCAD.

**Windows :**
```bat
cd "C:\Program Files\GRAPHISOFT\ARCHICAD 27"
LP_XMLConverter.exe x2l "chemin\vers\Table_Parametrique.xml" "chemin\vers\Table_Parametrique.gsm"
```

**macOS :**
```bash
cd "/Applications/GRAPHISOFT/ARCHICAD 27/ARCHICAD 27.app/Contents/MacOS"
./LP_XMLConverter x2l "/chemin/vers/Table_Parametrique.xml" "/chemin/vers/Table_Parametrique.gsm"
```

Le fichier `Table_Parametrique.gsm` obtenu se charge ensuite dans ArchiCAD via
*Fichier ▸ Bibliothèques et Objets ▸ Gestionnaire de bibliothèques*.

> Si votre version d'ArchiCAD signale un avertissement de version de section,
> la conversion aboutit quand même dans la grande majorité des cas. Sinon,
> utilisez la méthode 2 (100 % fiable).

## Méthode 2 — Copier-coller dans l'éditeur GDL (100 % fiable)

1. Dans ArchiCAD : *Fichier ▸ Bibliothèques et Objets ▸ Nouvel Objet…*
2. Dans la fenêtre de l'éditeur, créez les **paramètres** ci-dessous (bouton *Nouveau paramètre*).
3. Collez le contenu de chaque fichier `scripts/*.gdl` dans l'onglet correspondant :
   - `master.gdl` → **Script Maître**
   - `3d.gdl` → **Script 3D**
   - `2d.gdl` → **Script 2D**
   - `vl.gdl` → **Script Paramètres**
   - `ui.gdl` → **Script Interface**
4. *Fichier ▸ Enregistrer sous…* → le fichier **`.gsm`** est créé dans votre bibliothèque incorporée ou à l'emplacement de votre choix.

### Paramètres à créer

| Nom | Type | Valeur par défaut | Description |
|---|---|---|---|
| `A` | Longueur | 1,40 m | Longueur de la table *(existe déjà)* |
| `B` | Longueur | 0,80 m | Largeur de la table *(existe déjà)* |
| `hauteurTable` | Longueur | 0,75 m | Hauteur totale |
| `epPlateau` | Longueur | 0,04 m | Épaisseur du plateau |
| `largPied` | Longueur | 0,06 m | Section (carrée) des pieds |
| `retraitPied` | Longueur | 0,05 m | Retrait des pieds depuis le bord |
| `matPlateau` | Matériau | 1 | Matériau du plateau |
| `matPieds` | Matériau | 1 | Matériau des pieds |
| `stylo` | Stylo | 1 | Stylo du symbole 2D |

## Ce que fait l'objet

- **3D** : plateau rectangulaire posé sur 4 pieds carrés, matériaux séparés
  pour le plateau et les pieds, 8 points chauds d'édition.
- **2D** : contour du plateau + pieds en trait caché, 5 points chauds
  (4 coins étirables + centre).
- **Garde-fous** : le script maître empêche les valeurs aberrantes
  (pieds qui se croisent, plateau plus épais que la table, etc.).
- **Interface** : page de réglage personnalisée « Table paramétrique »
  dans la boîte de dialogue de l'objet.

Testé pour la syntaxe GDL standard (ArchiCAD 21 et supérieur).
