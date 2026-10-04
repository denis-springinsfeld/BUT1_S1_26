# Mémo CSS · TP2 Les Avatars - Images

Ce mémo récapitule les principales propriétés CSS abordées lors du TP2, regroupées par thématique.

---

## 1. Centrage moderne avec `align-content`

La propriété `align-content` permet désormais de centrer verticalement du contenu sur des blocs standards sans avoir besoin d'activer Flexbox ou CSS Grid (Chrome 123, Firefox 125, Safari 17.4 minimum).

| Propriété               | Rôle & Utilisation                                                                                                            | Exemple dans le TP                                                                                                |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `align-content: center` | Centre **verticalement** le contenu dans un conteneur bloc (à condition que le conteneur ait une hauteur ou un `min-height`). | `.demo` : centrage vertical de l'avatar.<br>`.avatar__badge` : centrage vertical du texte/icône dans la pastille. |

> [!NOTE]
> **Et pour l'axe horizontal ?**
> `align-content` n'agit **que sur l'axe vertical** en block layout. Pour obtenir un centrage parfait dans les deux axes :
>
> - **Si l'enfant est un bloc à taille définie** (ex. `.avatar`, `.test-image`) : l'enfant doit avoir `margin: auto` (ou `margin-inline: auto`) pour se centrer horizontalement.
> - **Si le contenu est du texte ou un élément en ligne** (ex. dans `.avatar__badge`) : on ajoute `text-align: center` sur le conteneur.

```css
/* Cas 1 : Centrage d'un bloc (.avatar) dans un conteneur (.demo) */
.demo {
  min-height: 12rem;
  align-content: center; /* ↕️ Centrage VERTICAL via le parent */
}

.avatar {
  width: 8rem;
  margin: auto; /* ↔️ Centrage HORIZONTAL via l'enfant */
}

/* Cas 2 : Centrage de texte ou icône dans une pastille */
.avatar__badge {
  width: 2em;
  height: 2em;
  text-align: center; /* ↔️ Centrage HORIZONTAL du texte */
  align-content: center; /* ↕️ Centrage VERTICAL du texte */
}
```

---

## 2. Propriétés liées aux images et aux avatars

Ces propriétés permettent de contrôler les dimensions, le rognage, la forme et le style des avatars sans jamais déformer les photos.

### A. Dimensions et ratios

- **`display: block`** : Par défaut, une balise `<img>` est un élément `inline`, ce qui crée un espace résiduel indésirable de 3 à 4 px sous l'image (espace réservé aux jambages de texte comme "p" ou "j"). Le passer en `block` supprime cet espace.
- **`max-width: 100%` & `height: auto`** : Règle de base du responsive design. Empêche l'image de dépasser de son parent tout en conservant son ratio d'origine.
- **`aspect-ratio: 1`** : Impose un ratio carré (largeur = hauteur), à partir de la largeur définie. Il est **ignoré** si la largeur et la hauteur sont toutes deux définies.

### B. Cadrage et recadrage (`object-fit` & `object-position`)

- **`object-fit: cover`** : L'image remplit tout son conteneur en conservant ses proportions. Les parties en trop sont rognées (indispensable pour les avatars).
- **`object-fit: contain`** : L'image est entièrement visible dans le conteneur sans rognage, quitte à laisser des bandes vides.
- **`object-position: center`** : Définit le point d'ancrage du recadrage (ex. `center`, `top`, `bottom`, `left`, `right`).

### C. Formes, bordures et contours

- **`border-radius: 50%`** : Transforme un carré parfait en cercle parfait.
- **`border-radius: inherit`** : Fait hériter à l'élément enfant (l'image ou le pseudo-élément) le même rayon d'arrondi que son conteneur parent.
- **`box-shadow`** : Ajoute une ombre portée pour détacher l'avatar de l'arrière-plan. La couleur relative `hsl(from var(--ink) h s l / 0.5)` demande un navigateur récent (Chrome 119, Safari 16.4, Firefox 128) : on déclare avant une valeur de repli `rgb(...)`.
- **`border: 10px solid transparent`** combiné avec `background: linear-gradient(...) border-box` : Permet d'afficher un dégradé visible uniquement dans la zone de bordure. Le mot-clé `border-box` (valeur unique dans le raccourci) règle à la fois l'origine et la zone peinte : sans lui, le dégradé démarrerait au bord intérieur (`padding-box`) et se répéterait sous la bordure transparente (voir TP Arrière-plans).
- **`outline` & `outline-offset`** :
  - `outline` trace un contour sans modifier la taille de la boîte (ne décale pas les éléments voisins).
  - `outline-offset: -10px` : Une valeur négative repousse le contour vers l'intérieur de l'élément (effet de bague ou double bordure).

> [!TIP]
> **`border-radius: inherit` vs `overflow: hidden`**
>
> - `overflow: hidden` sur le conteneur rognait tout ce qui dépassait... y compris le badge (`.avatar__badge`) placé à cheval sur la bordure !
> - Appliquer `border-radius: inherit` directement sur l'image (`.avatar__img`) permet de rogner l'image en cercle tout en laissant le conteneur parent libre d'afficher un badge qui déborde.

### D. Positionnement du conteneur, de l'image et du badge

- **`.avatar` (`position: relative`)** : Crée un contexte de référence de positionnement pour ses enfants absolus.
- **`.avatar__img` (`position: absolute; inset: 0;`)** : Étire l'image sur l'intégralité du conteneur parent (`top: 0; right: 0; bottom: 0; left: 0;`).
- **`.avatar__badge` (`position: absolute; right: calc(14.6% - 1em); bottom: calc(14.6% - 1em);`)** : Place le badge sur le cercle à 45° (en bas à droite), quelle que soit la taille de l'avatar : 14,6 % = 50 % − 50 % × cos 45°, et `- 1em` recentre le badge (de largeur `2em`) sur ce point. `z-index: 1` le garde au-dessus du `::after`.

```css
/* Exemple complet : structure de base d'un avatar */
.avatar {
  position: relative;
  width: 8rem;
  aspect-ratio: 1;
  border-radius: 50%;
  box-shadow: 2px 4px 6px hsl(from var(--ink) h s l / 0.5);
}

.avatar__img {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  border-radius: inherit;
}
```

---

## 3. Superposition avec le pseudo-élément `::after`

Le pseudo-élément `::after` permet d'insérer un élément virtuel décoratif sans ajouter de balise dans le code HTML.

| Propriété                             | Rôle                                                                                                                     |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| **`content: ""`**                     | **Obligatoire**. Sans cette propriété (même avec une chaîne vide), le pseudo-élément n'est pas généré par le navigateur. |
| **`position: absolute` & `inset: 0`** | Positionne le pseudo-élément directement au-dessus du conteneur parent, couvrant exactement sa surface.                  |
| **`border-radius: inherit`**          | Épouse la forme du parent (qu'il soit rond ou carré).                                                                    |
| **`pointer-events: none`**            | Permet aux clics et survols de traverser le calque décoratif pour atteindre l'image ou le lien en-dessous.               |

```css
/* Exemple : calque de contour intérieur superposé */
.avatar--b-after::after {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  outline: 2px solid var(--paper);
  outline-offset: -10px;
  pointer-events: none;
}
```

> **Pourquoi utiliser `::after` plutôt qu'un `outline` direct ?**
> Lorsque l'image `<img>` est en position absolue, elle peut masquer ou chevaucher certains contours du parent. Placer l'effet sur le pseudo-élément `::after` garantit qu'il se dessine par-dessus l'image.
>
> Une `<img>` est un élément remplacé : elle ne peut pas porter de `::after`, d'où le passage par le conteneur `.avatar`.

---

## 4. Organisation et mise en page des listes

Dans l'exercice 09, une liste non ordonnée (`<ul>`) sert à présenter une galerie ou une collection d'avatars.

| Propriété                    | Sélecteur           | Rôle                                                                                                                               |
| ---------------------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **`list-style: none`**       | `.avatarList`       | Retire les puces automatiques de la liste.                                                                                         |
| **`padding: 0`**             | `.avatarList`       | Réinitialise l'indentation intérieure par défaut imposée par les navigateurs sur les `<ul>`.                                       |
| **`text-align: center`**     | `.avatarList`       | Centre horizontalement tous les éléments en ligne ou `inline-block` enfants.                                                       |
| **`display: inline-block`**  | `.avatarList__item` | Permet d'aligner les éléments de liste côte à côte tout en conservant la capacité de leur donner des marges, largeurs et hauteurs. |
| **`vertical-align: middle`** | `.avatarList__item` | Aligne verticalement les avatars entre eux sur une même ligne, même s'ils ont des tailles différentes.                             |
| **`margin: 1rem`**           | `.avatarList__item` | Crée un espacement régulier entre chaque avatar de la collection.                                                                  |

```css
/* Exemple : galerie d'avatars */
.avatarList {
  margin: 1.5rem 0 0;
  padding: 0;
  list-style: none;
  text-align: center;
}

.avatarList__item {
  display: inline-block;
  vertical-align: middle;
  margin: 1rem;
}
```

> [!TIP]
> **Accessibilité :** `list-style: none` fait perdre à la liste son rôle sous Safari/VoiceOver. On le rétablit avec `role="list"` sur le `<ul>`.

---

## 5. Utilisation d’un sprite SVG (`<symbol>` et `<use>`)

Dans l'exercice 08, une icône en forme d'étoile est insérée dans la pastille de badge grâce à la technique du **sprite SVG inline**. Cette méthode permet de centraliser et réutiliser des icônes vectorielles sans dupliquer leur tracé dans le DOM.

### A. Définition du sprite dans le HTML

Un conteneur `<svg>` invisible est placé en bas de page pour stocker les icônes sous forme de symboles :

```html
<!-- En bas de la page HTML : magasin d'icônes -->
<svg
  xmlns="http://www.w3.org/2000/svg"
  width="0"
  height="0"
  class="svg-sprite"
  aria-hidden="true"
>
  <symbol id="star" viewBox="0 0 32 32">
    <path
      d="M32 12.408l-11.056-1.607-4.944-10.018-4.944 10.018-11.056 1.607 8 7.798-1.889 11.011 9.889-5.199 9.889 5.199-1.889-11.011 8-7.798z"
      fill="currentColor"
    ></path>
  </symbol>
</svg>
```

| Élément / Attribut                                                                                    | Rôle                                                                                                                                                                          |
| ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `width="0" height="0"` + `.svg-sprite { position: absolute; width: 0; height: 0; overflow: hidden; }` | Empêche le conteneur du sprite d'occuper de l'espace visible dans la mise en page. Le CSS est indispensable : le reset `svg { height: auto }` écrase l'attribut `height="0"`. |
| `aria-hidden="true"`                                                                                  | Masque le sprite aux technologies d'assistance (lecteurs d'écran) car c'est un conteneur purement technique.                                                                  |
| `<symbol id="star">`                                                                                  | Déclare une icône réutilisable identifiée par son `id`.                                                                                                                       |
| `viewBox="0 0 32 32"`                                                                                 | Définit le repère cartésien interne du tracé pour qu'il soit parfaitement scalable à n'importe quelle taille sans perte de qualité.                                           |
| `fill="currentColor"`                                                                                 | **Astuce clé** : l'icône prend automatiquement la couleur du texte définie en CSS (`color`) sur son parent.                                                                   |

### B. Affichage et réutilisation dans un composant

Pour afficher l'icône, on utilise un `<svg>` léger qui référence le symbole via `<use href="#id">` :

```html
<!-- Dans l'exercice 08 : affichage dans le badge -->
<span class="avatar__badge" role="img" aria-label="Favori">
  <svg class="avatar__icon" aria-hidden="true">
    <use href="#star"></use>
  </svg>
</span>
```

### C. Règles CSS associées

```css
/* 1. Taille fluide basée sur le texte parent */
.avatar__icon {
  width: 1em; /* 1em = même taille que le texte du badge */
  height: 1em;
  margin: auto; /* Centrage dans le badge */
}

/* 2. Contrôle de la couleur */
.avatar__badge {
  color: #fff; /* L'étoile devient blanche grâce à fill="currentColor" */
}
```

> [!TIP]
> **Avantages de cette approche :**
>
> - **Performance & légèreté** : le tracé vectoriel (`<path>`) n'est écrit qu'une seule fois dans la page, même si l'icône est affichée 50 fois.
> - **Stylisation CSS dynamique** : la taille suit la `font-size` (`1em`) et la couleur suit `color` (`currentColor`), simplifiant les thèmes sombres/clairs et les survols.
> - **Accessibilité** : l'icône est décorative (`aria-hidden="true"`), tandis que le rôle textuel est porté proprement par le parent (`role="img"` + `aria-label="Favori"`).
