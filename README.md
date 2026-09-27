# TP1 PLUS — Buttons Effects

Vous disposez de :

- **`index.html`** : la structure HTML avec les sections et les boutons (déjà fourni, ne pas modifier)
- **`css/default.css`** : les styles de mise en page globale (déjà fourni, ne pas modifier)
- **`css/style.css`** : votre fichier de travail, **pré-rempli jusqu'à la ligne 169** avec :
  - L'import de la police Roboto
  - Les variables CSS (`:root`)
  - Le reset CSS
  - Les styles de base du composant `.btn` (états normal, `:hover`, `:active`)
  - Le modifier `.btn--primary`

> **Objectif** : Compléter `style.css` à partir de la ligne 169 pour coder **10 effets de boutons** différents.

### Structure HTML de chaque bouton

Chaque bouton suit la même structure :

> ```html
> <section>
>   <h2>Nom de l'effet</h2>
>   <a href="" class="btn btn--modifier">texte</a>
> </section>
> ```

> ⚠️ Chaque effet est un **modifier BEM** (`.btn--xxx`) qui s'ajoute à la classe de base `.btn`. On ne réécrit pas tout, on **surcharge** uniquement les propriétés nécessaires.

---

## Effets de boutons CSS



https://github.com/user-attachments/assets/1f02f7da-76ff-4378-ac01-2646102a1c86


---

## Vue d'ensemble

| Ombres & couleurs     |     Dégradés animés     |     Pseudo-éléments & animations |
| ──────────────────    |    ──────────────────   |     ──────────────────────────── |
| 1. Neon               |  4. Duotone             | 7. Sticker  |
| 2. Neumorphism        | 5. Liquid               | 8. Terminal |
| 3. Press              | 6. Glass                | 9. Latéral |
|                       |                           |   10. Ink |

---

## Phase 1 — Ombres & Couleurs (effets 1 → 3)

> Objectif : maîtriser `box-shadow` (multiples, `inset`), `text-shadow`, `filter` et les formats de couleur (`rgba`, HEX alpha).

### Effet 1 — Neon

| Notion introduite      | Propriété CSS                             |
| ---------------------- | ----------------------------------------- |
| Ombre sur le texte     | `text-shadow`                             |
| Ombres multiples       | `box-shadow: ..., ...` (séparées par `,`) |
| Ombre intérieure       | `inset` dans `box-shadow`                 |
| Couleur HEX avec alpha | `#ff2bd61a` (2 derniers digits = opacité) |
| Fond transparent       | `background: transparent`                 |

---

### Effet 2 — Neumorphism

| Notion introduite        | Propriété CSS                                           |
| ------------------------ | ------------------------------------------------------- |
| Double ombre opposée     | `box-shadow: 8px 8px 16px #c3c4cc, -8px -8px 16px #fff` |
| Ombre intérieure au clic | `inset` dans `:active`                                  |

---

### Effet 3 — 3D Press

| Notion introduite                | Propriété CSS                                   |
| -------------------------------- | ----------------------------------------------- |
| Ombre solide (socle)             | `box-shadow: 0 8px 0 #9c1c27` (blur = 0)        |
| Filtre de luminosité             | `filter: brightness(1.05)`                      |
| Coordination ombre + déplacement | `translateY(8px)` + `box-shadow: 0 0 0`         |
| Transition multi-propriétés      | `transition: transform 0.12s, box-shadow 0.12s` |

---

## Phase 2 — Dégradés animés (effets 4 → 6)

> Objectif : maîtriser `linear-gradient`, `background-size`, `background-position`, `rgba()`, `backdrop-filter`.

### Effet 4 — Duotone

| Notion introduite       | Propriété CSS                                      |
| ----------------------- | -------------------------------------------------- |
| Dégradé à coupure nette | `linear-gradient(90deg, #ff2323 50%, #1489ff 50%)` |
| Fond surdimensionné     | `background-size: 220% 100%`                       |
| Animation par position  | `background-position: 0% → 100%`                   |

---

### Effet 5 — Liquid

| Notion introduite        | Propriété CSS                         |
| ------------------------ | ------------------------------------- |
| Dégradé multi-couleurs   | `linear-gradient(270deg, 5 couleurs)` |
| Fond très surdimensionné | `background-size: 400% 100%`          |
| Forme pilule             | `border-radius: 999px`                |
| Boucle fluide            | Dernière couleur = première couleur   |

---

### Effet 6 — Glassmorphism

| Notion introduite         | Propriété CSS                                 |
| ------------------------- | --------------------------------------------- |
| Flou d'arrière-plan       | `backdrop-filter: blur(10px)`                 |
| Fond semi-transparent     | `background: rgba(255, 255, 255, 0.16)`       |
| Bordure semi-transparente | `border: 1px solid rgba(255, 255, 255, 0.45)` |
| Dégradé diagonal          | `linear-gradient(135deg, ...)`                |
| Déplacement vertical      | `transform: translateY(-3px)`                 |
| Combinaison de transforms | `translateY(0) scale(0.97)`                   |

---

## Phase 3 — Pseudo-éléments & Animations (effets 7 → 10)

> Objectif : maîtriser `::before`, `::after`, `content`, `@keyframes`, `animation`, `position: relative/absolute`, `overflow: hidden`, `z-index`, `aspect-ratio`.

### Effet 7 — Sticker

| Notion introduite                  | Propriété CSS                       |
| ---------------------------------- | ----------------------------------- |
| Anneaux avec `box-shadow` (spread) | `0 0 0 4px #fff, 0 0 0 7px #17171a` |
| Rotation                           | `transform: rotate(-3deg)`          |
| Combinaison de transforms          | `rotate(0deg) scale(1.04)`          |

---

### Effet 8 — Terminal

| Notion introduite        | Propriété CSS                             |
| ------------------------ | ----------------------------------------- |
| Pseudo-élément `::after` | `.btn--terminal::after`                   |
| Propriété `content`      | `content: "_"`                            |
| Définition d'animation   | `@keyframes blink { 50% { opacity: 0 } }` |
| Application d'animation  | `animation: blink 1s steps(1) infinite`   |
| Timing `steps()`         | `steps(1)` → bascule instantanée on/off   |
| Police monospace         | `font-family: "Courier New", monospace`   |

---

### Effet 9 — Remplissage latéral

| Notion introduite                   | Propriété CSS                            |
| ----------------------------------- | ---------------------------------------- |
| Pseudo-élément `::before` graphique | `content: ""` (contenu vide)             |
| Positionnement absolu               | `position: absolute` + parent `relative` |
| Masquage du débordement             | `overflow: hidden`                       |
| Empilement                          | `z-index: 0` / `z-index: -1`             |
| Transition avec délai               | `transition: color 0.35s ease 0.1s`      |
| Ciblage hover + pseudo              | `.btn:hover::before`                     |

---

### Effet 10 — Encre circulaire

| Notion introduite                                    | Propriété CSS                                |
| ---------------------------------------------------- | -------------------------------------------- |
| Centrage absolu complet                              | `left: 50%; top: 50%; translate(-50%, -50%)` |
| Ratio d'aspect                                       | `aspect-ratio: 1/1`                          |
| Forme circulaire                                     | `border-radius: 50%`                         |
| Expansion depuis le centre                           | `width: 0` → `width: 300%`                   |
| Transitions multi-propriétés avec timings différents | `width 0.4s ease, opacity 0.4s ease`         |

---

## Récapitulatif — Notion introduite à chaque étape

| #   | Effet       | Nouvelles notions clés                                                         |
| --- | ----------- | ------------------------------------------------------------------------------ |
| 1   | Neon        | `text-shadow`, `box-shadow` multiples, `inset`, HEX alpha                      |
| 2   | Neumorphism | Double ombre opposée, `inset` au `:active`                                     |
| 3   | Press       | Ombre solide (blur 0), `filter: brightness()`, coordination translate/shadow   |
| 4   | Duotone     | `linear-gradient` coupure nette, `background-size/position`                    |
| 5   | Liquid      | Gradient multi-couleurs, `border-radius: 999px`                                |
| 6   | Glass       | `backdrop-filter: blur()`, `rgba()`, synthèse ombres + gradients               |
| 7   | Sticker     | Anneaux (spread), `rotate()`, combinaison transforms                           |
| 8   | Terminal    | `::after`, `content`, `@keyframes`, `animation`, `steps()`                     |
| 9   | Latéral     | `::before` graphique, `position`, `overflow`, `z-index`, transition avec délai |
| 10  | Ink         | `aspect-ratio`, centrage absolu, `border-radius: 50%`, expansion circulaire    |
