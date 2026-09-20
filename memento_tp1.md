# Mémo HTML & CSS — Spécial TP Boutons

Ce mémento rassemble **uniquement les notions essentielles** abordées lors du TP (création de boutons, variables CSS, BEM, icônes) et le minimum requis pour structurer vos pages.

---

## 1. Structure HTML Minimale

Toute page web doit posséder cette structure de base (balises allégées HTML5) :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="utf-8">
  <title>Titre de l'onglet</title>
  <link rel="stylesheet" href="css/style.css"> <!-- Lien vers le fichier CSS -->
</head>
<body>
  <!-- Le contenu visible de la page va ici -->
</body>
</html>
```

### Balises de contenu utilisées dans le TP
*   `<a>` : **Lien hypertexte**. Permet de naviguer. Attribut `href` obligatoire.
    *   *URL absolue* : `href="https://mozilla.org"`
    *   *URL relative* : `href="page2.html"`
    *   *Ancre interne* : `href="#rubrique"` (pointe vers un élément avec `id="rubrique"`)
*   `<h1>` à `<h6>` : **Titres**. Permettent de hiérarchiser le contenu (du plus important `<h1>` au moins important).
*   `<p>` : **Paragraphe** de texte.
*   `<img>` : **Image**. Attributs `src` (chemin de l'image) et `alt` (texte alternatif pour l'accessibilité).
*   `<svg>` : **Image vectorielle**. Balise permettant d'inclure du dessin vectoriel (icônes) directement dans le code HTML (*inline*).

> **Accessibilité** : Utilisez toujours l'attribut `alt=""` vide sur une `<img>` si celle-ci est purement décorative. Sur un `<svg>` décoratif, utilisez l'attribut `aria-hidden="true"`.

---

## 2. Concepts CSS du TP

### Sélecteurs et Pseudo-classes
*   `*` : Sélecteur **universel** (cible tous les éléments).
*   `balise` : Cible tous les éléments d'un type (ex: `a { ... }`).
*   `.classe` : Cible les éléments ayant cet attribut classe (ex: `.btn { ... }`).
*   `:hover` : Pseudo-classe déclenchée quand l'élément est **survolé** par la souris.
*   `:active` : Pseudo-classe déclenchée quand l'élément est **cliqué**.
*   `:focus-visible` : Pseudo-classe déclenchée quand l'élément reçoit le focus au clavier (Tabulation).

### Les Unités de mesure
*   `px` : Pixel. Unité fixe.
*   `rem` : Relative à la taille de police de la racine (`<html>`). Préférable pour l'accessibilité.
*   `em` : Relative à la taille de police de l'élément lui-même. Idéal pour les `padding` des boutons ou la taille des icônes.
*   `ch` : Largeur du caractère "0" de la police actuelle. Pratique pour le `min-width` d'un bouton.

### La Convention BEM (Block Element Modifier)
Méthode de nommage des classes CSS pour créer des composants réutilisables :
*   **Bloc** : Le composant de base ` .btn `
*   **Élément** : Une partie du bloc ` .btn__icon ` (séparé par deux tirets du bas `__`)
*   **Modificateur** : Une variante du bloc ` .btn--danger ` (séparé par deux tirets `--`)

### Variables et Fonctions CSS
*   **Variables** (Custom Properties) : Permettent de stocker une valeur.
    *   *Déclaration globale* : `:root { --clr-primary: #1489ff; }`
    *   *Déclaration locale* : `.btn { --btn-bg: white; }`
    *   *Utilisation* : `color: var(--clr-primary);`
*   `calc()` : Fonction permettant d'effectuer des calculs mathématiques dynamiques *(ex: `calc(var(--shadow) / 2)` pour diviser une variable par deux)*.

---

## 3. Liste des Propriétés CSS utilisées (Classées par type)

Voici toutes les propriétés CSS dont vous avez eu besoin pour réaliser les exercices, classées par ordre logique de déclaration.

### 📐 Reset & Modèle de Boîte (Box Model)
Contrôle la taille et l'espacement physique des éléments.

*   `box-sizing` : Modifie le calcul de la taille. La valeur `border-box` inclut le padding et les bordures dans la largeur/hauteur.
*   `display` : Change le comportement d'affichage. `inline-block` permet à un lien (normalement *en-ligne*) de se comporter comme une *boîte* ayant une largeur et hauteur.
*   `width` / `height` : Largeur et hauteur fixes.
*   `min-width` / `min-height` : Largeur et hauteur minimales. *(ex: `min-height: 2.75rem` pour un bouton accessible)*.
*   `margin` : Marges externes (espace à l'extérieur de la bordure).
*   `padding` : Marges internes (espace entre le contenu et la bordure).

### 🔤 Typographie
Contrôle l'apparence du texte.

*   `@import` : Règle placée tout en haut du fichier CSS permettant d'importer une police distante *(ex: Google Fonts)*.
*   `font-family` : Police d'écriture *(ex: "Roboto", sans-serif)*.
*   `font-size` : Taille du texte.
*   `font-weight` : Graisse du texte *(ex: normal, bold, 500, 700)*.
*   `color` : Couleur du texte. La valeur `currentColor` hérite de la couleur du texte courant (très utile pour les SVG).
*   `text-align` : Alignement horizontal du texte *(ex: center)*.
*   `text-transform` : Transformation du texte *(ex: capitalize, uppercase)*.
*   `text-decoration` : Soulignement *(ex: none pour retirer le trait des liens)*.
*   `line-height` : Hauteur de ligne.
*   `vertical-align` : Alignement vertical pour les éléments *en-ligne* ou *inline-block* *(ex: middle pour centrer une icône)*.

### 🎨 Couleurs & Effets Visuels
Contrôle l'habillage de la boîte.

*   `background-color` : Couleur de fond.
*   `border` : Bordure (épaisseur, style, couleur). *(ex: `solid 3px black`)*.
*   `border-radius` : Arrondi des angles de la bordure.
*   `box-shadow` : Ombre portée de la boîte. *(ex: `8px 8px 0 gray`)*.
*   `outline` : Contour dessiné autour de l'élément (souvent utilisé pour le focus clavier).
*   `outline-offset` : Décale le contour `outline` vers l'extérieur.

### 🎬 Transitions & Transformations
Contrôle l'animation et la déformation.

*   `transition` : Permet d'animer le changement d'état d'une propriété (ex: lors d'un `:hover`). *Paramètres : propriété, durée, accélération*.
*   `transform` : Modifie la forme ou la position. Utilisé ici avec `scale(0.95)` pour réduire légèrement le bouton au clic (effet d'enfoncement).
