# TD 1 — Introduction au HTML & CSS

> **Objectifs :** Créer une première page web, la styliser avec CSS et découvrir les outils du développeur web.

**Projet fil rouge :** Reproduire cette page de présentation Netflix.

![Résultat attendu](NEtflix.png)

> **Assets fournis :**
>
> - `netflix.svg` — Le logo Netflix
> - `bg.png` — L'image de fond (affiche Stranger Things)

---

## Exercice 1 — Mise en place de l'environnement

### 1.1 Navigateur par défaut : Firefox

Configurer Firefox comme navigateur par défaut sous Windows :

1. Sélectionnez **Démarrer > Paramètres > Applications > Applications par défaut**.
2. Recherchez **Firefox** dans la liste.
3. Cliquez sur **Définir par défaut**.

> **Pourquoi Firefox ?** Firefox intègre des outils de développement très puissants (inspecteur d'élément, console, débogueur réseau…) que nous utiliserons tout au long de la formation.

---

### 1.2 Visual Studio Code

1. Créez un répertoire `TD1` sur le bureau.
2. Ouvrez **Visual Studio Code** et ouvrez votre dossier `TD1` (`Fichier > Ouvrir le dossier`).
3. Installez l'extension [**Live Server**](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) — elle recharge automatiquement le navigateur à chaque sauvegarde.
4. Installez l'extension [**Prettier**](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) — elle formate automatiquement votre code.

> [!TIPS]
> **Raccourci utile :** `Ctrl + S` pour sauvegarder. Live Server détecte la sauvegarde et rafraîchit la page instantanément.

---

## Exercice 2 — Première page HTML

### 2.1 Structure des fichiers du projet

Organisez votre dossier `TD1` ainsi et copiez les assets fournis :

```plaintext
TD1/
├── index.html
├── css/
│   └ style.css
└── assets/
    ├ netflix.svg
    └ bg.png
```

### 2.2 Structure minimale avec Emmet

**Emmet** est un plugin intégré à VS Code qui génère du code HTML/CSS à partir de raccourcis.

Dans votre fichier `index.html` vide, tapez **`!`** puis appuyez sur **`Tab`** :

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body></body>
</html>
```

> **Explication des balises :**
>
> - `<!DOCTYPE html>` : déclare que le document est en HTML5.
> - `<html lang="en">` : balise racine de la page. Changez `en` en `fr` pour indiquer que la page est en français.
> - `<head>` : contient les métadonnées (non visibles par l'utilisateur).
> - `<meta charset="UTF-8">` : définit l'encodage de caractères (accents, emojis…).
> - `<body>` : contient tout le contenu visible de la page.

**À faire :** Modifiez l'attribut `lang` pour mettre `fr`, le `<title>` pour `Netflix — Stranger Things`, et ajoutez le lien vers le CSS :

```html
<!DOCTYPE html>
<html lang="fr">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Netflix — Stranger Things</title>
    <link rel="stylesheet" href="css/style.css" />
  </head>
  <body></body>
</html>
```

✅ **Vérification :** Ouvrez la page avec Live Server → page blanche, l'onglet doit afficher "Netflix — Stranger Things" et la console ne doit contenir aucune erreur.

### 2.3 Ajout de contenu

Dans le `<body>`, ajoutez les éléments suivants :

| Balise  | Rôle                                  | Exemple                                           |
| ------- | ------------------------------------- | ------------------------------------------------- |
| `<h1>`  | Titre de niveau 1 (le plus important) | `<h1>HELLO HTML</h1>`                             |
| `<p>`   | Paragraphe de texte                   | `<p>CSS is AWESOME</p>`                           |
| `<img>` | Image                                 | `<img src="..." alt="description" width="120" />` |

> **Attributs de `<img>` :**
>
> - `src` : chemin vers le fichier image (obligatoire)
> - `alt` : description textuelle de l'image (obligatoire pour l'accessibilité)
> - `width` : largeur en pixels — permet au navigateur de réserver l'espace avant que l'image soit chargée, évitant les "sauts" de mise en page

> **Hiérarchie des titres :** HTML propose 6 niveaux de titres (`<h1>` à `<h6>`). Il ne doit y avoir qu'un seul `<h1>` par page (le titre principal). Vous devez respecter la hiérarchie des titres : pas de h4 sans h3, pas de h3 sans h2, etc.

### 2.4 Application Netflix — Contenu du hero

Dans le `<body>`, ajoutez le `<header>` avec toutes ses classes sémantiques :

```html
<header class="hero">
  <!-- Logo Netflix -->
  <img
    class="hero-logo"
    src="./assets/netflix.svg"
    alt="Logo Netflix"
    width="120"
  />

  <!-- Titre de la série -->
  <h1 class="hero-title">Stranger Things</h1>

  <!-- Métadonnées -->
  <div class="hero-meta">
    2019 &nbsp;|&nbsp; DIRECTOR: Shawn Levy &nbsp;|&nbsp; seasons: 3 &nbsp;(5
    Episodes)
  </div>

  <!-- Description -->
  <p class="hero-description">
    In 1980s Indiana, a group of young friends witness supernatural forces and
    secret government exploits. As they search for answers, the children unravel
    a series of extraordinary mysteries.
  </p>

  <!-- Boutons d'action -->
  <div class="hero-actions">
    <button class="btn btn-primary">PLAY NOW</button>
    <button class="btn btn-outline">ALL EPISODES</button>
  </div>

  <!-- Footer du hero -->
  <p class="hero-footer">POPULAR THIS WEEK</p>
</header>
```

> **Pourquoi `class` et pas `id` ?**
> Les classes permettent de réutiliser les styles. Un `id` est unique sur la page et ne doit jamais servir pour le CSS — uniquement pour les ancres (`<a href="#section">`) et le JavaScript.

✅ **Vérification :** Rechargez la page — tout le texte brut s'affiche sans mise en forme.

### 2.5 Lancement avec Live Server

- Faites un **clic droit** sur votre fichier `index.html` dans l'explorateur VS Code.
- Sélectionnez **"Open with Live Server"**.
- Votre page s'ouvre dans Firefox.

### 2.6 Inspecteur d'élément

- Sur votre page ouverte dans Firefox, faites un **clic droit** sur un élément > **Inspecter l'élément**.
- Explorez le panneau **HTML** à gauche et le panneau **CSS** à droite.

> **À essayer :** Survolez les balises dans l'inspecteur — Firefox surligne l'élément correspondant dans la page.

---

## Exercice 3 — Mise en forme avec CSS

### 3.1 Création et liaison du fichier CSS

1. Créez un dossier `css/` dans votre répertoire `TD1`.
2. Dans ce dossier, créez un fichier `style.css`.
3. **Liez** le fichier CSS à votre HTML en ajoutant dans le `<head>` :

```html
<link rel="stylesheet" href="css/style.css" />
```

> **Principe de séparation des responsabilités :** le HTML structure le contenu, le CSS gère l'apparence. On ne les mélange pas.

### 3.2 Propriétés de base

Consultez [MDN Web Docs](https://developer.mozilla.org/fr/) pour chacune des propriétés suivantes et appliquez-les dans votre `style.css` :

| Propriété CSS                                                                        | Rôle                   |
| ------------------------------------------------------------------------------------ | ---------------------- |
| [`color`](https://developer.mozilla.org/fr/docs/Web/CSS/color)                       | Couleur du texte       |
| [`background-color`](https://developer.mozilla.org/fr/docs/Web/CSS/background-color) | Couleur d'arrière-plan |
| [`font-family`](https://developer.mozilla.org/fr/docs/Web/CSS/font-family)           | Police de caractères   |

**Exemple de règle CSS :**

```css
body {
  background-color: #f0f4f8;
  color: #333333;
  font-family: Arial, Helvetica, sans-serif;
}
```

> **Syntaxe d'une règle CSS :**
>
> ```
> sélecteur {
>   propriété: valeur;
> }
> ```
>
> Le **sélecteur** cible un ou plusieurs éléments HTML. La **propriété** est ce que l'on veut modifier. La **valeur** est ce qu'on lui attribue.

### 3.3 Application Netflix — Reset et styles de base

La **première chose** à écrire dans tout fichier CSS est le reset universel (couche **Generic**), qui supprime les marges et espaces par défaut des navigateurs :

```css
/* ============================================
   GENERIC — Micro Reset navigateur
   ============================================ */
* {
  /* Supprime les marges externes */
  margin: 0;
  /* Supprime les marges internes */
  padding: 0;
  /* Force le calcul de la taille d'un élément en incluant son padding et sa bordure */
  box-sizing: border-box;
}
```

> **`box-sizing: border-box`** : fait en sorte que le `padding` et la `border` soient inclus dans la largeur/hauteur d'un élément. Indispensable pour des mises en page prévisibles.

✅ **Vérification :** Les marges blanches autour de la page ont disparu.

Ajoutez ensuite les styles de base (couche **Elements**) :

```css
/* ============================================
   ELEMENTS — Styles des balises HTML de base
   ============================================ */
body {
  /* Police de caractère par défaut */
  font-family: sans-serif;
  /* Couleur du texte par défaut */
  color: white;
}
```

✅ **Vérification :** Tout le texte est maintenant en blanc.

- Appliquez une police **sans-serif** (ex : `Arial`, `Helvetica`, ou `sans-serif` en générique).

---

## Exercice 4 — Sélecteurs CSS : balises et classes

### 4.1 Le sélecteur de balise (déjà vu)

Cible tous les éléments d'un type donné, exemple : tous les `<p>` de la page.

```css
p {
  color: steelblue;
}
```

### 4.2 Le sélecteur de classe (`.`)

Une **classe** s'applique à un ou plusieurs éléments. Elle se déclare avec l'attribut `class` en HTML et se cible avec un `.` en CSS.

**HTML :**

```html
<p class="important">Ce texte est mis en avant.</p>
<p>Celui-ci est normal.</p>
<p class="important">Celui-là aussi est mis en avant.</p>
```

**CSS :**

```css
.important {
  color: crimson;
  font-weight: bold;
}
```

> **Avantage des classes :** une même classe peut être réutilisée sur autant d'éléments que nécessaire, quel que soit leur type de balise.

**À faire :**

1. Ajoutez une deuxième balise `<p>` dans votre page.
2. Créez une classe `highlight` et appliquez-la à l'un de vos paragraphes.
3. En CSS, donnez à `.highlight` : une `background-color` jaune (`#ffe066`) et du `padding` (ex : `5px 10px`).

### 4.3 Nommer ses classes avec du sens

Une bonne classe décrit **ce qu'est** l'élément, pas **comment il ressemble**.

| ❌ À éviter   | ✅ À préférer    | Pourquoi                             |
| ------------- | ---------------- | ------------------------------------ |
| `.rouge`      | `.alerte`        | La couleur peut changer, le rôle non |
| `.gros-texte` | `.titre-section` | Décrit la fonction, pas l'apparence  |
| `.div1`       | `.carte-produit` | Lisible et réutilisable              |

**À faire :**

1. Dans votre HTML, entourez votre `<h1>` et votre `<p>` dans une balise `<section>`.
2. Ajoutez les classes `page-title` sur le `<h1>` et `page-intro` sur le `<p>`.
3. En CSS, stylisez `.page-title` (taille, couleur, marge) et `.page-intro` (largeur, interligne).

### 4.4 Application Netflix — Composants CSS (couche Components)

Stylez maintenant chaque élément du hero avec ses classes sémantiques :

**Le bloc hero — image de fond plein écran :**

```css
/* ============================================
   COMPONENTS — Composants de l'interface
   ============================================ */

/* --- Hero (bloc principal) --- */
.hero {
  height: 100vh;
  padding: 3rem 5rem;

  background-image: url("../bg.png");
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}
```

> **`height: 100vh`** : `vh` = _viewport height_. `100vh` = 100 % de la hauteur de la fenêtre du navigateur.
> **`background-size: cover`** : l'image remplit tout le bloc sans se déformer.

✅ **Vérification :** L'image de fond Stranger Things s'affiche plein écran.

**Le logo, le titre et les métadonnées :**

```css
/* --- Logo --- */
.hero-logo {
  width: 120px;
}

/* --- Titre --- */
.hero-title {
  font-size: 4rem;
  font-weight: bold;
  margin: 8rem 0 1rem;
}

/* --- Métadonnées --- */
.hero-meta {
  font-size: 1rem;
  font-weight: 600;
  letter-spacing: 0.05em;
  margin-bottom: 1rem;
  opacity: 0.9;
}
```

> **`rem`** est une unité relative à la taille de police de base du navigateur (généralement `16px`). `4rem` = `64px`. Préférez `rem` aux pixels fixes.

**La description :**

```css
/* --- Description --- */
.hero-description {
  width: 40%;
  font-weight: 300;
  line-height: 1.6;
  opacity: 0.75;
  margin-bottom: 2.5rem;
}
```

> **`width: 40%`** : limite la largeur du paragraphe. Un texte sur toute la largeur serait difficile à lire sur fond d'image.

**Les boutons — multi-classes :**

```css
/* --- Zone de boutons --- */
.hero-actions {
  display: flex;
  gap: 1rem;
  margin-bottom: 3rem;
}

/* Styles communs à tous les boutons */
.btn {
  padding: 0.8rem 2.5rem;
  font-size: 0.85rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  cursor: pointer;
  border: 2px solid white;
}

/* Bouton rouge plein */
.btn-primary {
  background-color: #e50914;
  border-color: #e50914;
  color: white;
}

/* Bouton transparent avec bordure */
.btn-outline {
  background-color: transparent;
  color: white;
}
```

> **Multi-classes :** `class="btn btn-primary"` combine deux classes. `.btn` apporte les styles communs ; `.btn-primary` ajoute la couleur rouge.

✅ **Vérification :** Les boutons sont alignés horizontalement et possèdent des styles distincts selon leur rôle.

### 4.5 Récapitulatif des sélecteurs

| Sélecteur | Syntaxe HTML  | Syntaxe CSS | Utilisation                            |
| --------- | ------------- | ----------- | -------------------------------------- |
| Balise    | `<p>`         | `p { }`     | Cible **tous** les éléments `<p>`      |
| Classe    | `class="nom"` | `.nom { }`  | Cible plusieurs éléments réutilisables |

> **Bonne pratique :** Utilisez exclusivement des **classes** pour le style CSS. Les attributs `id` sont réservés aux ancres de navigation (`<a href="#section">`) et aux interactions JavaScript — **jamais** pour du style.

---

## Exercice 5 — Code complet & Bilan

### Code final — `index.html`

```html
<!DOCTYPE html>
<html lang="fr">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Netflix — Stranger Things</title>
    <link rel="stylesheet" href="css/style.css" />
  </head>
  <body>
    <header class="hero">
      <img class="hero-logo" src="netflix.svg" alt="Logo Netflix" />
      <h1 class="hero-title">Stranger Things</h1>
      <div class="hero-meta">
        2019 &nbsp;|&nbsp; DIRECTOR: Shawn Levy &nbsp;|&nbsp; seasons: 3
        &nbsp;(5 Episodes)
      </div>
      <p class="hero-description">
        In 1980s Indiana, a group of young friends witness supernatural forces
        and secret government exploits. As they search for answers, the children
        unravel a series of extraordinary mysteries.
      </p>
      <div class="hero-actions">
        <button class="btn btn-primary">PLAY NOW</button>
        <button class="btn btn-outline">ALL EPISODES</button>
      </div>
      <p class="hero-footer">POPULAR THIS WEEK</p>
    </header>
  </body>
</html>
```

### Code final — `css/style.css`

```css
/* GENERIC */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* ELEMENTS */
body {
  font-family: sans-serif;
  color: white;
}

/* COMPONENTS */
.hero {
  height: 100vh;
  padding: 3rem 5rem;
  background-image: url("../bg.png");
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}

.hero-logo {
  width: 120px;
}

.hero-title {
  font-size: 4rem;
  font-weight: bold;
  margin: 8rem 0 1rem;
}

.hero-meta {
  font-size: 1rem;
  font-weight: 600;
  letter-spacing: 0.05em;
  margin-bottom: 1rem;
  opacity: 0.9;
}

.hero-description {
  width: 40%;
  font-weight: 300;
  line-height: 1.6;
  opacity: 0.75;
  margin-bottom: 2.5rem;
}

.hero-actions {
  display: flex;
  gap: 1rem;
  margin-bottom: 3rem;
}

.btn {
  padding: 0.8rem 2.5rem;
  font-size: 0.85rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  cursor: pointer;
  border: 2px solid white;
}

.btn-primary {
  background-color: #e50914;
  border-color: #e50914;
  color: white;
}

.btn-outline {
  background-color: transparent;
  color: white;
}

.hero-footer {
  font-size: 0.8rem;
  font-weight: 800;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  opacity: 0.9;
}
```

### Checklist de rendu

Avant de rendre votre travail, vérifiez que votre page contient :

- [ ] Une structure HTML5 valide (`<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`)
- [ ] Un `<title>` pertinent dans le `<head>`
- [ ] Un `<h1>` unique avec une classe sémantique
- [ ] Au moins deux `<p>` dont un avec une classe `highlight`
- [ ] Une `<img>` avec les attributs `src` et `alt`
- [ ] Un fichier `style.css` lié avec `<link>`
- [ ] Des règles CSS utilisant des sélecteurs de **balise et de classe uniquement** (aucun `#id`)
- [ ] Une `font-family` sans-serif appliquée
- [ ] Image de fond plein écran avec `background-image` et `100vh`
- [ ] Boutons avec multi-classes (`.btn` + `.btn-primary` / `.btn-outline`)
- [ ] Unité `rem` utilisée pour les tailles de texte

---

## Liens utiles

- [MDN Web Docs](https://developer.mozilla.org/fr/) — La référence incontournable pour HTML et CSS
- [Web.dev](https://web.dev/learn/) — Cours complets par Google
- [Validateur HTML W3C](https://validator.w3.org/) — Vérifier que votre HTML est valide
- [CSS-Tricks](https://css-tricks.com/) — Astuces et guides CSS pratiques
- [MDN — background-image](https://developer.mozilla.org/fr/docs/Web/CSS/background-image)
- [MDN — Flexbox](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_flexible_box_layout)
