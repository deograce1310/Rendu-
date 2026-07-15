# Baguettes de pain — Objet bibliothèque ArchiCAD (.gsm)

Objet GDL décoratif : une ou plusieurs **baguettes de pain** posées côte à côte,
avec corps fuselé (surface de révolution) et **grignes** en biais sur le dessus.
Idéal pour habiller une boulangerie, une cuisine ou une table dans vos rendus.

> ⚠️ Le format `.gsm` est un format binaire propriétaire de GRAPHISOFT : ce
> dossier contient le **code source GDL** de l'objet et deux méthodes pour
> obtenir le `.gsm` (voir ci-dessous ou le README de `Table_Parametrique/`
> pour le pas-à-pas détaillé).

## Contenu du dossier

| Fichier | Rôle |
|---|---|
| `Baguette_Pain.xml` | Source complète au format XML de LP_XMLConverter (conversion automatique en `.gsm`) |
| `scripts/master.gdl` | Script maître (garde-fous, valeurs dérivées) |
| `scripts/3d.gdl` | Script 3D (corps fuselé + grignes + points chauds) |
| `scripts/2d.gdl` | Script 2D (vue de dessus projetée) |
| `scripts/vl.gdl` | Script paramètres (bornes des valeurs) |
| `scripts/ui.gdl` | Script interface (boîte de dialogue personnalisée) |

## Obtenir le fichier .gsm

**Méthode 1 — LP_XMLConverter** (livré avec ArchiCAD) :

```bat
:: Windows
cd "C:\Program Files\GRAPHISOFT\ARCHICAD 27"
LP_XMLConverter.exe x2l "chemin\vers\Baguette_Pain.xml" "chemin\vers\Baguette_Pain.gsm"
```

```bash
# macOS
cd "/Applications/GRAPHISOFT/ARCHICAD 27/ARCHICAD 27.app/Contents/MacOS"
./LP_XMLConverter x2l "/chemin/vers/Baguette_Pain.xml" "/chemin/vers/Baguette_Pain.gsm"
```

**Méthode 2 — Copier-coller** (100 % fiable) : *Fichier ▸ Bibliothèques et
Objets ▸ Nouvel Objet…*, créez les paramètres du tableau ci-dessous, collez
chaque fichier `scripts/*.gdl` dans l'onglet correspondant, puis
*Enregistrer sous…* → le `.gsm` est créé.

### Paramètres à créer

| Nom | Type | Valeur par défaut | Description |
|---|---|---|---|
| `longBaguette` | Longueur | 0,65 m | Longueur d'une baguette |
| `diamBaguette` | Longueur | 0,055 m | Diamètre (au centre) |
| `espacement` | Longueur | 0,09 m | Entraxe entre baguettes |
| `nbBaguettes` | Entier | 3 | Nombre de baguettes |
| `grignes` | Booléen | Oui | Afficher les grignes |
| `nbGrignes` | Entier | 5 | Nombre de grignes par baguette |
| `matPain` | Matériau | 1 | Matériau de la croûte |
| `matGrigne` | Matériau | 1 | Matériau des grignes (plus clair, la mie) |
| `stylo` | Stylo | 1 | Stylo du symbole 2D |

## Ce que fait l'objet

- **3D** : chaque baguette est une surface de révolution fuselée (pointes aux
  deux extrémités), posée au sol. Les baguettes sont légèrement pivotées en
  alternance (±2,5°) pour un rendu naturel. Les grignes sont de fines
  entailles en biais (30°) réparties sur le dessus.
- **2D** : vue de dessus générée automatiquement depuis le modèle 3D
  (`PROJECT2`), avec 5 points chauds.
- **Garde-fous** : proportions toujours cohérentes (diamètre limité au tiers
  de la longueur, espacement minimal égal au diamètre, etc.).
- **Astuce rendu** : affectez à `matPain` un matériau brun doré et à
  `matGrigne` un matériau beige clair pour évoquer la mie ouverte.

Testé pour la syntaxe GDL standard (ArchiCAD 21 et supérieur).
