# Mémo CSS · TP2 Les arrière-plans - background

Ce mémo récapitule les principales propriétés d’arrière-plan CSS abordées lors du TP2, dans l’ordre des exercices, avec leurs valeurs usuelles et les pièges fréquents.

---

## 1. Propriétés d’arrière-plan sous-jacentes

### `background-image`

Définit une ou plusieurs images ou dégradés d’arrière-plan. Les couches se séparent par des virgules ; la première déclarée est dessinée au-dessus des suivantes.

```css
/* Image seule */
background-image: url("photo.jpg");

/* Superposition d'un dégradé semi-transparent et d'une photo */
background-image:
  linear-gradient(rgb(0 0 0 / 30%), transparent), url("photo.jpg");
```

> [!NOTE]
> Une image d’arrière-plan n’a pas d’attribut `alt` : elle est invisible pour les lecteurs d’écran. Si elle est purement décorative, c’est suffisant. Si elle porte du sens, on l’indique sur l’élément avec `role="img"` et `aria-label` (comme dans l’exercice 01), ou on utilise une balise `<img>`.

---

### `background-size`

Définit les dimensions de l’image d’arrière-plan.

```css
background-size: cover; /* Couvre toute la zone (rognage possible) */
background-size: contain; /* Affiche toute l'image (bandes vides possibles) */
background-size: 120px 80px; /* Largeur puis Hauteur */
background-size: 50% auto; /* auto conserve le ratio d'origine */
```

- **`cover`** : Couvre l'intégralité du conteneur en conservant les proportions.
- **`contain`** : Ajuste l'image pour qu'elle tienne entièrement dans le conteneur. Avec `repeat` (par défaut), l'image se répète dans l'espace libre : ajouter `no-repeat` pour voir les bandes vides.
- **Deux valeurs** : `largeur hauteur` (ex. `100px auto`). Choisir des valeurs au même ratio que l'image pour ne pas la déformer.

---

### `background-repeat`

Définit si et comment l’image se répète pour remplir la zone.

```css
background-repeat: no-repeat; /* Pas de répétition */
background-repeat: repeat; /* Répétition X et Y (par défaut) */
background-repeat: repeat-x; /* Répétition horizontale uniquement */
background-repeat: repeat-y; /* Répétition verticale uniquement */
background-repeat: space; /* Répartit les motifs sans rognage */
background-repeat: round; /* Redimensionne les motifs pour un nombre entier */

/* Syntaxe à deux valeurs : horizontal puis vertical */
background-repeat: space repeat;
background-repeat: round no-repeat; /* équivaut à repeat-x avec round */
```

---

### `background-position`

Définit la position d’ancrage de l’image d’arrière-plan dans sa zone de référence.

```css
background-position: center;
background-position: right bottom;
background-position: 20% 70%;
background-position: 12px 24px;
```

> [!IMPORTANT]
> **Ordre des valeurs :** Lorsqu'on précise deux valeurs, la première indique l'axe **horizontal** (X) et la seconde l'axe **vertical** (Y).

---

### `background-attachment`

Définit le comportement de l’arrière-plan lors du défilement.

```css
background-attachment: scroll; /* Défile avec la page (valeur par défaut) */
background-attachment: fixed; /* Fixé par rapport à la fenêtre d'affichage (viewport) */
background-attachment: local; /* Défile avec le contenu interne de l'élément */
```

> [!TIP]
> **`local` vs `scroll` :** Sur un élément doté d'un défilement interne (`overflow: auto` ou `scroll`), `scroll` garde le fond fixe par rapport à la boîte globale, tandis que `local` fait défiler le fond avec le texte intérieur. Sans défilement interne, `local` se comporte comme `scroll`.

> [!WARNING]
> `fixed` est mal ou pas géré sur mobile (notamment iOS Safari) : ne pas compter dessus pour un effet indispensable.

---

### `background-origin`

Définit la boîte de référence pour le calcul du positionnement (`background-position`) et de la taille.

```css
background-origin: padding-box; /* Intérieur de la bordure (par défaut) */
background-origin: border-box; /* Inclut la bordure */
background-origin: content-box; /* Zone de contenu, à l'intérieur du padding */
```

---

### `background-clip`

Définit la zone sur laquelle l’arrière-plan (couleur et images) est effectivement **peint**.

```css
background-clip: border-box; /* Peint sous la bordure (par défaut) */
background-clip: padding-box; /* Peint jusqu'au bord intérieur de la bordure */
background-clip: content-box; /* Peint uniquement sous le contenu */
```

> [!NOTE]
> **Différence entre `origin` et `clip` :**
>
> - `background-origin` choisit où commence le repère du motif/photo.
> - `background-clip` découpe la peinture du fond (couleur + image).

---

### `background-color`

Définit la couleur peinte derrière toutes les images d’arrière-plan (couleur de secours).

```css
background-color: var(--primary);
background-color: #147d74;
background-color: transparent;
```

---

## 2. Le raccourci `background`

La propriété raccourcie permet d’associer plusieurs sous-propriétés en une seule ligne.

```css
/* Syntaxe usuelle : [couleur] [image] [position] / [taille] [répétition] [attachement] */
background: var(--primary) url("photo.jpg") center / cover no-repeat;

/* Plusieurs couches : la couleur n'apparaît que dans la dernière */
background:
  linear-gradient(rgb(0 0 0 / 30%), transparent),
  url("photo.jpg") center / cover var(--primary);
```

> [!WARNING]
> **Effet de réinitialisation automatique :**
> Déclarer la propriété raccourcie `background` réinitialise **toutes les sous-propriétés non spécifiées** à leurs valeurs par défaut.
>
> _Exemple :_ Si vous aviez défini `background-size: cover`, puis que vous écrivez ensuite `background: url("img.jpg");`, la taille repassera automatiquement à `auto` !

---

## 3. Tableau récapitulatif

| Propriété               | Valeur par défaut    | Description                                               |
| ----------------------- | -------------------- | --------------------------------------------------------- |
| `background-image`      | `none`               | Image(s) ou dégradé(s) d'arrière-plan                     |
| `background-size`       | `auto auto`          | Dimensions de l'image (`cover`, `contain`, px, %)         |
| `background-repeat`     | `repeat`             | Répétition du motif (`no-repeat`, `repeat-x`, `space`...) |
| `background-position`   | `0% 0%` (`top left`) | Position de l'image sur les axes X et Y                   |
| `background-attachment` | `scroll`             | Comportement au défilement (`fixed`, `local`)             |
| `background-origin`     | `padding-box`        | Boîte de référence pour l'ancrage de l'image              |
| `background-clip`       | `border-box`         | Zone d'extension de la peinture du fond                   |
| `background-color`      | `transparent`        | Couleur du fond (peinte sous les images)                  |
