# TP1 : L'élément `<a>` comme bouton

## Objectifs

À la fin de ce TP, vous saurez :

- créer des liens hypertextes (absolus, relatifs, ancres internes) avec la balise `<a>` ;
- styliser un lien pour en faire un **bouton accessible** (états, focus clavier, taille de cible tactile) ;
- factoriser vos styles avec les **propriétés personnalisées CSS** ;
- décliner un composant avec la convention **BEM** ;
- intégrer des **icônes SVG** (via `<img>` et en inline).

---

## Exercice 1 : Basic Button — Mise en place HTML

L'élément HTML `<a>` (pour **ancre**, _anchor_ en anglais), avec son attribut `href`, crée un **lien hypertexte** vers des pages web, des fichiers, des adresses e-mail, des emplacements se trouvant dans la même page, ou tout ce qu'une URL peut adresser.

[Documentation MDN : l'élément `<a>`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/a)

➡️ Ouvrir le fichier `exo1_btn_basic_HTML/index.html`.

➡️ Ajouter dans le `<body>` une balise `<a>` avec un attribut `href` vide et le texte de lien « Basic ».

> [!NOTE]
>
> ```html
> <a href="">Basic</a>
> ```
>
> Un `href` vide pointe vers la page courante : cliquer dessus recharge la page.

### `<a>` ou `<button>` ?

Il existe aussi une balise `<button>` pour créer des boutons. Nous la verrons plus tard ; pour l'instant, nous utilisons `<a>`. Pour bien les différencier :

| Balise         | Rôle                                               | Exemples                                                      |
| -------------- | -------------------------------------------------- | ------------------------------------------------------------- |
| `<a href="…">` | **Naviguer** : aller quelque part                  | une page, une section, un fichier, un e-mail                  |
| `<button>`     | **Agir** : déclencher un comportement dans la page | envoyer un formulaire, ouvrir un menu, exécuter du JavaScript |

> [!TIP]
> Un lien qui ressemble à un bouton reste un lien. On lui donne une apparence de bouton quand son rôle est de **mener quelque part** (« S'inscrire », « En savoir plus »). Le choix de la balise dépend du **comportement**, pas de l'apparence.

### Liens hypertextes absolus et relatifs

Il existe trois façons d'écrire l'adresse d'un lien hypertexte :

| Type                                    | Principe                                         | Exemples                                                                                                                   |
| --------------------------------------- | ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| **URL absolue**                         | Adresse complète : protocole + domaine + chemin  | `https://developer.mozilla.org/fr/`                                                                                        |
| **Relatif à la racine** (chemin absolu) | Part de la **racine du site** (commence par `/`) | `/page2.html` (dossier racine) <br> `/pages/page2.html` (sous-dossier)                                                     |
| **Relatif au fichier courant**          | Chemin calculé **à partir du fichier courant**   | `page2.html` ou `./page2.html` (même dossier) <br> `../index.html` (dossier parent) <br> `pages/page2.html` (sous-dossier) |

> [!IMPORTANT]
> Pour les TP, nous utiliserons **uniquement des liens relatifs** pour naviguer entre les pages du projet.
> Un lien relatif à la racine (`/page2.html`) se casse dès que le site n'est pas hébergé à la racine : ouverture directe du fichier depuis le disque, ou publication dans un sous-dossier. Les liens vers des sites externes, eux, utilisent bien sûr des URL absolues.

> [!NOTE]
> `./page2.html` est une écriture explicite de `page2.html` : le `./` indique que le fichier se trouve dans le **même dossier** que la page courante.

#### ◼︎ Créer un lien vers une URL absolue

➡️ Ajouter une **URL absolue** à l'attribut `href` de votre ancre pour créer un lien vers la page de Mozilla.

#### ◼︎ Créer des liens vers des URL relatives

➡️ Ajouter un fichier `page2.html` à votre répertoire de travail.
Ajouter une **URL relative** à l'attribut `href` d'une seconde ancre pour créer un lien vers `page2.html`.

➡️ Dans `page2.html`, ajouter un lien relatif de retour vers `index.html`.

#### ◼︎ Créer un lien vers un élément de la même page

➡️ Ajouter un paragraphe `<p>` après votre ancre. Utiliser **Emmet** pour créer du texte de substitution : `p>lorem1000` puis `Tab`.

➡️ Ajouter ensuite un titre avec l'identifiant `rubrique-down`, puis un second paragraphe de texte de substitution.

➡️ Ajouter l'URL `#rubrique-down` à l'attribut `href` de votre ancre.

> [!NOTE]
> L'identifiant `id=rubrique-down` sert à relier l'ancre à cet élément. Un `id` doit être **unique** dans la page.
>
> ```html
> <!-- Rubrique à relier -->
> <h2 id="rubrique-down">Section plus bas</h2>
> ```
>
> Le texte de substitution rend la page assez longue pour qu'on **voie** la page défiler jusqu'à la rubrique. Le second paragraphe, placé après le titre, permet à celui-ci de remonter tout en haut de la fenêtre.

➡️ Ajouter en bas de page un lien « Retour en haut » (`href="#"`).

---

## Exercice 2 : Basic Button — Styles CSS

➡️ Ouvrir le fichier `exo2_3_btn_basic_Styles/index.html`.

➡️ Ajouter dans le `<body>` une balise `<a>` avec un attribut `href="#"`, le texte de lien « Basic » et un attribut de **classe `btn`**.

➡️ Ouvrir le fichier `exo2_btn_basic_Styles/css/style.css`.
Nous allons maintenant styliser notre bouton en CSS.

> [!NOTE]
> En CSS, les commentaires s'écrivent `/* … */`.

### Conventions d'écriture CSS

> [!IMPORTANT]
> **Ordre des blocs dans un fichier CSS**
>
> Du plus général au plus spécifique :
>
> 1. **Import des polices** (Google Fonts) : `@import` doit figurer en tout début de fichier
> 2. **Variables CSS** (_custom properties_) : déclarées dans `:root`
> 3. **Reset CSS** : neutralisation des styles par défaut du navigateur
> 4. **Styles de base** : éléments HTML génériques (`body`, `h1`, `a`, etc.)
> 5. **Composants** : styles propres à chaque élément de l'interface

> [!IMPORTANT]
> **Ordre des propriétés dans une règle**
>
> Les propriétés vont des plus structurantes (impact sur la mise en page) aux plus décoratives :
>
> 0. **Variables locales du composant** : déclarées en tête de la règle
> 1. **Positionnement** : `position`, `top`, `right`, `bottom`, `left`, `z-index`
> 2. **Display et Box Model** : `display`, `width`, `height`, `margin`, `padding`, `border`
> 3. **Typographie** : `font-*`, `line-height`, `text-align`, `color`
> 4. **Effets visuels et graphiques** : `background`, `border-radius`, `box-shadow`, `opacity`
> 5. **Transformations et transitions** : `transform`, `transition`, `animation`

Exemple :

```css
.card {
  /* 1. Positionnement */
  position: relative;
  z-index: 1;

  /* 2. Display et Box Model */
  display: inline-block;

  width: 20rem;
  padding: 1.5rem;

  /* 3. Typographie */
  font-size: 1rem;
  color: var(--text);

  /* 4. Effets visuels et graphiques */
  background: var(--surface);
  border-radius: 8px;
  box-shadow: 0 2px 8px rgb(0 0 0 / 0.1);

  /* 5. Transformations et transitions */
  transition: transform 0.2s ease;
}
```

### ◼︎ 1. Import de la police `Roboto` depuis Google Fonts

➡️ Chercher la police `Roboto` sur **[Google Fonts](https://fonts.google.com/)**, puis copier le code d'import de type `@import`.
Le coller en tout début de votre fichier CSS.

<details>
<summary>💡 Solution</summary>

```css
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100..900;1,100..900&display=swap");
```

</details>

### ◼︎ 2. Variables CSS

➡️ Pour cet exercice, le `:root` reste vide. Nous verrons dans l'exercice 3 comment l'utiliser pour définir des variables CSS.

```css
:root {
}
```

### ◼︎ 3. Réinitialiser les styles : Reset CSS

#### `box-sizing`

La propriété CSS `box-sizing` définit la façon dont la largeur et la hauteur totales d'un élément sont calculées : avec `border-box`, le `padding` et la bordure sont **inclus** dans la largeur et la hauteur déclarées.

[MDN : box-sizing](https://developer.mozilla.org/fr/docs/Web/CSS/box-sizing)

➡️ Écrire la règle CSS qui applique `border-box` à tous les éléments, et qui supprime les marges externes (`margin`) et le remplissage (`padding`) par défaut du navigateur.

<details>
<summary>💡 Solution</summary>

```css
/* Le sélecteur universel `*` sélectionne tous les éléments de la page. */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
```

</details>

### ◼︎ 4. Styles de base

➡️ Écrire les règles CSS qui :

- appliquent la police `Roboto` à la page, avec un padding et un fond gris très clair pour que le bouton blanc reste visible ;
- suppriment le soulignement de tous les liens (propriété `text-decoration`).

<details>
<summary>💡 Solution</summary>

```css
body {
  /* Applique la police Roboto à la page */
  font-family: "Roboto", sans-serif;
}

a {
  /* Supprime le soulignement des liens */
  text-decoration: none;
}
```

</details>

### ◼︎ 5. Styles du composant bouton

➡️ Styliser le bouton avec la classe `.btn` dans votre fichier CSS.
**Respectez l'ordre des propriétés** décrit plus haut.

#### / Display & Modèle de boîte

➡️ Pour qu'un lien accepte une largeur et une hauteur, il faut changer sa propriété `display`. Commencez par `display: inline-block;` : le lien reste dans le flux en ligne tout en acceptant les dimensions d'une boîte.

Ajoutez ensuite un `padding`, un `min-width` et un `min-height`.

- Le `padding` est exprimé en `em` : il se redimensionne proportionnellement à la `font-size` du bouton.
- Le `min-width` est exprimé en `ch`, unité à peu près égale à la largeur du caractère « 0 » de la police appliquée. C'est un garde-fou de rythme visuel : avec deux boutons côte à côte, « Partager » et « En savoir plus », sans `min-width` le premier serait brusquement plus court que le second.
- Le `min-height` garantit que le bouton est une cible suffisamment grande pour les appareils tactiles. La norme d'accessibilité WCAG 2.2 exige au minimum **24 × 24 px** (critère 2.5.8, niveau AA) et recommande **44 × 44 px** (critère 2.5.5, niveau AAA).

> [!IMPORTANT]
> **À observer :** où se place le texte dans le bouton ? Il est collé en haut ! `text-align` ne centre que **horizontalement**, et le texte ne remplit pas les 44 px de hauteur.

<details>
<summary>💡 Solution</summary>

```css
.btn {
  /* 2. Display et Box Model */
  display: inline-flex;
  align-items: center;
  justify-content: center;

  min-width: 10ch;
  min-height: 44px;
  padding: 0.25em 0.75em;
}
```

</details>

#### / Typographie & style de texte

➡️ Définir la famille de police, la taille et la graisse du texte du bouton, centrer le texte et définir sa couleur.

> [!NOTE]
> Utilisez la police **importée à l'étape 1** (Roboto) et une graisse qui existe (400, 500 ou 700).

<details>
<summary>💡 Solution</summary>

```css
.btn {
  /* … (suite du code précédent) */

  /* 3. Typographie */
  font-family: "Roboto", sans-serif;
  font-size: 1rem;
  font-weight: 500;
  text-align: center;
  color: #000;
}
```

</details>

#### / Effets visuels & graphiques

➡️ Définir la couleur de fond, le rayon de bordure et l'ombre portée du bouton.

> [!IMPORTANT]
> **Accessibilité :** le texte doit toujours avoir un contraste d'au moins **4,5:1** avec son fond pour rester lisible. Vérifiez vos couleurs avec le [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) ou les outils du navigateur (DevTools).

<details>
<summary>💡 Solution</summary>

```css
.btn {
  /* … (suite du code précédent) */

  /* 4. Effets visuels et graphiques */
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 3px 5px rgb(0 0 0 / 0.18);
}
```

</details>

#### / Styles d'état

À l'heure actuelle, le seul retour visuel qu'un utilisateur reçoit lorsqu'il interagit avec le bouton est le passage du curseur en « pointeur ». Il faut donc distinguer les états du bouton grâce aux **pseudo-classes**.

> [!TIP]
> Une pseudo-classe est une **classe virtuelle** qui permet de définir un style pour un élément dans un état particulier. Par exemple, `:hover` cible un élément lorsque le curseur est dessus.

Quatre états sont à traiter :

| Pseudo-classe | État             | Remarque                                    |
| ------------- | ---------------- | ------------------------------------------- |
| _(aucune)_    | normal           |                                             |
| `:hover`      | survolé          |                                             |
| `:active`     | en cours de clic | à écrire **après** `:hover` pour l'emporter |

➡️ Écrire les règles `.btn:hover`, `.btn:focus-visible` et `.btn:active`.

- Chan
- À l'appui, donner l'impression que le bouton s'enfonce (`transform` et `box-shadow`).

<details>
<summary>💡 Solution</summary>

```css
.btn:hover {
  color: #fff;
  background-color: #3c57ce;
}

.btn:focus-visible {
  outline: 3px solid #3c57ce;
  outline-offset: 3px;
}

.btn:active {
  box-shadow: none;
  transform: translateY(1px);
}
```

</details>

#### / Transition

➡️ Ajouter une transition sur la couleur de fond et la couleur du texte pour que le changement se fasse en douceur.

En CSS, la propriété `transition` est un raccourci pour définir les quatre propriétés individuelles : `transition-property`, `transition-duration`, `transition-timing-function` et `transition-delay`.

> [!NOTE]
> La `transition` se déclare dans la règle `.btn` (et **non** dans `:hover`) : elle s'applique ainsi à la fois à l'entrée (_over_) et à la sortie (_out_) du survol.

<details>
<summary>💡 Solution</summary>

```css
.btn {
  /* … (suite du code précédent) */

  /* 5. Transformations et transitions */
  transition:
    background-color 0.3s ease,
    color 0.3s ease;
}
```

</details>

---

## Exercice 3 : Basic Button + Custom Properties

➡️ **Modifier** votre code de l'exercice 2 pour utiliser des variables CSS.

Les **propriétés personnalisées CSS** (_custom properties_, aussi appelées variables CSS) sont des entités définies par les développeurs ou les utilisateurs d'une page web, contenant des valeurs réutilisables à travers le document.

- On les **déclare** avec un nom qui commence par deux tirets : `--main-color: black;`
- On les **utilise** avec la fonction `var()` : `color: var(--main-color);`
- On peut fournir une **valeur de repli**, utilisée si la variable n'existe pas : `color: var(--main-color, #333);`

Des sites et applications complexes ont des feuilles de style où de nombreuses valeurs sont répétées. Les propriétés personnalisées permettent de stocker une valeur à un seul endroit puis de la réutiliser : on **factorise** le code et les modifications deviennent plus simples.

### ◼︎ 1. Variables globales dans `:root`

➡️ Dans `:root`, déclarer des variables pour toutes les valeurs « de design » de votre bouton :

- les **couleurs** : surface (fond du bouton), texte, couleur principale (`#3c57ce`), texte sur la couleur principale ;
- la **police** de caractères ;
- le **rayon de bordure** ;
- l'**ombre portée** ;
- la **durée de transition**.

Remplacer ensuite toutes les valeurs « en dur » de `.btn` par des `var(--…)`.

### ◼︎ 2. Variables locales du composant

Pour préparer l'exercice 4, déclarer aussi dans la règle `.btn` des variables **propres au composant** :

- `--btn-bg` et `--btn-color` : couleurs de l'état normal ;
- `--btn-bg-hover` et `--btn-color-hover` : couleurs de l'état survolé.

Les propriétés `background-color` et `color` de `.btn` et de `.btn:hover` utilisent ensuite **ces variables locales**, qui elles-mêmes reprennent les variables globales.

> [!NOTE]
> Les variables locales se placent **en tête de la règle**, avant toutes les autres propriétés.
> Le nommages des variable s locales commence par le nom du composant (`btn`) pour éviter les collisions avec d'autres composants et sont sémantiques : `bg` pour background, `color` pour la couleur du texte, `hover` pour l'état survolé.
> Sémantique = on comprend à quoi sert la variable sans avoir à regarder sa valeur.

<details>
<summary>💡 Solution</summary>

```css
:root {
  /* Couleurs */
  --clr-white: rgb(250, 250, 250);
  --clr-black: rgb(23, 23, 23);
  --clr-gray: rgb(113, 113, 122);
  --clr-blue: rgb(60, 87, 206);

  /* Typographie */
  --font-family: "Roboto", sans-serif;

  /* Formes et effets */
  --radius: 8px;
  --shadow: 0 3px 5px rgb(0 0 0 / 0.18);

  /* Transition */
  --transition-duration: 0.3s;
}

.btn {
  /* 0. Variables locales du composant */
  --btn-bg: var(--clr-white);
  --btn-color: var(--clr-black);
  --btn-bg-hover: var(--clr-blue);
  --btn-color-hover: var(--clr-white);

  /* 2. Display et Box Model */
  display: inline-block;

  min-width: 10ch;
  min-height: 44px;
  padding: 0.25em 0.75em;

  /* 3. Typographie */
  font-family: var(--font-family);
  font-size: 1rem;
  font-weight: 500;
  text-align: center;
  color: var(--btn-color);

  /* 4. Effets visuels et graphiques */
  background-color: var(--btn-bg);
  border-radius: var(--radius);
  box-shadow: var(--shadow);

  /* 5. Transformations et transitions */
  transition:
    background-color var(--transition-duration) ease,
    color var(--transition-duration) ease;
}

.btn:hover {
  color: var(--btn-color-hover);
  background-color: var(--btn-bg-hover);
}

.btn:active {
  box-shadow: none;
  transform: translateY(1px);
}
```

</details>

### ◼︎ 3. Vérifier

➡️ Changer uniquement la valeur de `--color-primary` dans `:root` : le survol , sans toucher au reste du code.

➡️ **Question :** que se passe-t-il si vous écrivez `color: var(--color-inexistante);` ? Et avec `color: var(--color-inexistante, #333);` ?

### Documentation

- [MDN : Utiliser les propriétés personnalisées CSS](https://developer.mozilla.org/fr/docs/Web/CSS/Using_CSS_custom_properties)
- [CSS-Tricks : A Complete Guide to Custom Properties](https://css-tricks.com/a-complete-guide-to-custom-properties/)

---

## Exercice 4 : Basic Button + Variantes de style (BEM)

➡️ Ouvrir le fichier `exo4_btn_Styles_variants/index.html` et le fichier `exo4_btn_Styles_variants/css/style.css`.

### La convention BEM

[Documentation BEM](https://getbem.com/introduction/)

> [!NOTE]
> **BEM = Block – Element – Modifier** (Bloc – Élément – Modificateur)
>
> - Un **BLOC** est un composant autonome qui peut être réutilisé : `btn`
> - Un **ÉLÉMENT** est une partie d'un bloc qui n'a pas de sens en dehors de celui-ci : `btn__icon`
> - Un **MODIFICATEUR** est une variante d'un bloc ou d'un élément : `btn--small`
>
> Le BLOC est la classe de base qui définit les propriétés communes. Le MODIFICATEUR **s'ajoute** à la classe du bloc (il ne la remplace jamais) et ne définit que ce qui change.

### ◼︎ 1. Tailles

➡️ Dans le HTML, ajouter un bouton avec les classes `btn` **et** `btn--small`.

> [!NOTE]
>
> ```html
> <a href="#" class="btn btn--small">Small</a>
> ```

➡️ Dans le CSS, définir le MODIFICATEUR `btn--small` **en modifiant uniquement la taille de la police**.

> [!TIP]
> Comme le `padding` est en `em`, il se redimensionne proportionnellement à cette taille ; `min-width` et `min-height` veillent à ce que le bouton reste une zone tactile suffisante.

➡️ Créer de même un bouton `btn btn--large` avec une police plus grande.

<details>
<summary>💡 Solution</summary>

```css
.btn--small {
  font-size: var(--font-size-small, 1rem);
}

.btn--large {
  font-size: var(--font-size-large, 1.25rem);
}
```

</details>

### ◼︎ 2. Forme

➡️ Créer le MODIFICATEUR `btn--rounded` qui définit une bordure très arrondie (en forme de pilule).

> [!IMPORTANT]
> Un MODIFICATEUR a la **même spécificité** que le bloc (une seule classe). C'est donc l'**ordre dans le fichier** qui décide : écrivez toujours les modificateurs **après** la règle `.btn`.

### ◼︎ 3. Couleurs

➡️ Créer quatre MODIFICATEURS de couleur : `btn--primary` (bleu), `btn--success` (vert), `btn--warning` (jaune) et `btn--danger` (rouge).

> [!WARNING]
> **Le piège à éviter.** Si vous écrivez simplement :
>
> ```css
> .btn--danger {
>   background-color: #c62828;
> }
> ```
>
> le bouton devient rouge... mais au survol il repasse au bleu ! En effet, `.btn:hover` (2 sélecteurs : une classe + une pseudo-classe) est **plus spécifique** que `.btn--danger` (une classe) et l'emporte.
>
> La solution : **ne pas surcharger les propriétés, mais redéfinir les variables locales** de l'exercice 3 (`--btn-bg`, `--btn-color`, `--btn-bg-hover`, `--btn-color-hover`). Les règles `.btn` et `.btn:hover` restent inchangées et utilisent automatiquement les nouvelles valeurs.

<details>
<summary>💡 Exemple pour <code>btn--danger</code></summary>

```css
.btn--danger {
  --btn-bg: var(--clr-danger, #c62828);
  --btn-color: var(--clr-white, #fff);
  --btn-bg-hover: var(--clr-white, #fff);
  --btn-color-hover: var(--clr-danger, #c62828);
}
```

</details>

### ◼︎ 4. Combiner

➡️ Afficher toutes les combinaisons de classes suivantes, par exemple :

```html
<a href="#" class="btn btn--large btn--danger btn--rounded">Supprimer</a>
```

### ◼︎ Pour aller plus loin (facultatif)

- `btn--outline` : fond transparent et bordure colorée.
- `btn--block` : bouton sur toute la largeur du conteneur.

---

## Exercice 5 : Basic Button + Icônes

➡️ Ouvrir le fichier `exo5_btn_Icones/index.html` et le fichier `exo5_btn_Icones/css/style.css`.

Nous allons maintenant ajouter des icônes à nos boutons, avec la bibliothèque d'icônes [Heroicons](https://heroicons.com).

Le **SVG (Scalable Vector Graphics)** est un format d'image vectorielle basé sur le langage XML. Il permet de créer des images redimensionnables sans perte de qualité, contrairement aux images raster (JPEG, PNG).

> [!NOTE]
> **Deux façons d'intégrer un SVG dans une page HTML**
>
> **Avec l'élément `<img>`** : comme tous les formats d'image, un fichier SVG s'affiche avec `<img src="img/icon.svg" alt="">`. Le SVG étant externe, son contenu **ne peut pas être modifié en CSS** (la couleur de l'icône reste, par exemple, celle du fichier).
>
> **Directement dans le HTML (inline)** : la balise `<svg>` s'écrit dans le code de la page. Son contenu **peut être modifié en CSS**, notamment sa couleur.
>
> ```html
> <svg viewBox="0 0 24 24" width="24" height="24">
>   <!-- paths, shapes, etc. -->
> </svg>
> ```

➡️ Copier votre code de l'exercice 4 dans `exo5_btn_Icones`.
Ouvrir les fichiers `exo5_btn_Icones/index.html` et `exo5_btn_Icones/css/style.css`.

### ◼︎ 1. Icône avec `<img>`

➡️ Sur [heroicons.com](https://heroicons.com), choisir une icône (style _Outline_, taille 24) et la télécharger au format SVG dans `exo5_btn_Icones/img/`.

➡️ Dans le HTML, créer un bouton avec l'icône **à gauche du texte**, avec la balise `<img>`.

> [!NOTE]
> L'icône est purement décorative puisque le texte du bouton dit déjà la même chose : on écrit donc **`alt=""`**, ce qui la rend invisible pour les lecteurs d'écran.
>
> ```html
> <a href="#" class="btn">
>   <img class="btn__icon" src="img/icon.svg" alt="" />
>   Ajouter
> </a>
> ```

### ◼︎ 2. Icône avec `<svg>` inline

➡️ Créer un second bouton identique, mais en copiant cette fois le code **SVG** de l'icône depuis Heroicons (bouton « Copy SVG ») directement dans le HTML.

Nettoyer le code copié :

- supprimer la classe utilitaire fournie (`class="size-6"`) et la remplacer par `class="btn__icon"` ;
- vérifier que l'attribut `stroke="currentColor"` est bien présent ;
- ajouter `aria-hidden="true"` pour masquer l'icône décorative aux lecteurs d'écran.

```html
<a href="#" class="btn">
  <svg
    class="btn__icon"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    stroke-width="1.5"
    aria-hidden="true"
  >
    <!-- <path> copié depuis heroicons.com -->
  </svg>
  Ajouter
</a>
```

### ◼︎ 3. Styles

`btn__icon` est un **ÉLÉMENT** BEM : une partie du bloc `btn` qui n'a pas de sens en dehors de lui.

➡️ Dans le CSS :

- écrire la règle `.btn__icon` : une taille en `em` (pour qu'elle suive la `font-size` du bouton, donc les modificateurs `small` et `large`).

<details>
<summary>💡 Solution</summary>

```css
.btn__icon {
  width: 1.25em;
  height: 1.25em;
}
```

</details>

### ◼︎ 4. Comparer les deux méthodes

➡️ Survoler successivement le bouton `<img>` et le bouton `<svg>` inline. **Que constatez-vous sur la couleur de l'icône ?**

> [!TIP]
> `currentColor` est un mot-clé CSS qui vaut « la couleur du texte de l'élément ». L'icône inline en hérite, donc elle change en même temps que le texte au survol. L'icône chargée par `<img>` ne le peut pas.

➡️ Compléter le tableau suivant :

|                                             | `<img src="…">` | `<svg>` inline |
| ------------------------------------------- | --------------- | -------------- |
| Couleur modifiable en CSS (`currentColor`)  |                 |                |
| Fichier mis en cache par le navigateur      |                 |                |
| HTML plus léger et lisible                  |                 |                |
| Réutilisable simplement sur plusieurs pages |                 |                |

### ◼︎ Pour aller plus loin (facultatif)

- Créer un MODIFICATEUR `btn--icon` pour un bouton **avec icône seule** (sans texte), de 44 × 44 px minimum.

---

## Plus

- [CSS-Tricks : A Complete Guide to Links and Buttons](https://css-tricks.com/a-complete-guide-to-links-and-buttons/)
- [Modern CSS : CSS Button Styling Guide](https://moderncss.dev/css-button-styling-guide/)
- [Lea Verou : Custom properties with defaults](https://lea.verou.me/blog/2021/10/custom-properties-with-defaults/)
- [MDN : `:focus-visible`](https://developer.mozilla.org/fr/docs/Web/CSS/:focus-visible)
- [WCAG 2.2 : Target Size (Minimum)](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html)
- [WebAIM : Contrast Checker](https://webaim.org/resources/contrastchecker/)
