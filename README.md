# R111

## Bonnes pratiques CSS

### Accessibilité et responsive

- Utiliser `rem` pour les tailles de texte afin de respecter les préférences d’agrandissement de l’utilisateur. Les unités `px` restent adaptées aux bordures, aux ombres et à certaines dimensions techniques.
- Privilégier des tailles fluides avec `clamp()` lorsque cela améliore l’adaptation aux différentes tailles d’écran.
- Vérifier le contraste des couleurs et conserver un indicateur de focus visible.

### Organisation et cascade

- Organiser les styles par responsabilité : base, composants et layout.
- Éviter les sélecteurs trop spécifiques et les règles qui se surchargent inutilement.
- Utiliser des classes plutôt que des sélecteurs d’éléments ou d’attributs pour éviter les conflits et faciliter la maintenance.

### Ordre des déclarations

Les déclarations sont regroupées par catégorie afin de faciliter la lecture et la maintenance :

1. Affichage, avec `display` et `visibility`
2. Positionnement, avec `position`, `inset` et `z-index`
3. Modèle de boîte, avec `width`, `height`, `margin`, `padding` et `gap`
4. Typographie, avec `font-*`, `line-height`, `text-*` et `color`,
5. Couleurs et effets visuels, avec `background`, `border` et `box-shadow`
6. Transformations et transitions

Cette organisation est une convention de lecture : elle doit rester cohérente dans tout le projet.

### Nommage et maintenance

- Utiliser des noms de classes explicites et cohérents, par exemple avec la convention BEM ou une convention équivalente.
- Centraliser les couleurs, espacements et autres valeurs récurrentes dans des variables CSS.
- Tester les pages sur plusieurs tailles d’écran et dans les principaux navigateurs.

## Références

- [Web.dev HTML](https://web.dev/learn/html/)
- [Web.dev CSS](https://web.dev/learn/css/)

- [Mozilla Developer Network (MDN) CSS](https://developer.mozilla.org/fr/docs/Web/CSS)

- [Guide CSS d’Alsacréations](https://github.com/alsacreations/guidelines/blob/master/Guidelines-CSS.md)
- [CUBE CSS](https://cube.fyi/)

## Outils et ressources

### Images et contenus temporaires

- [Picsum Photos](https://picsum.photos/)
- [Pexels](https://www.pexels.com/)
- [Pravatar](https://i.pravatar.cc/)
- [Doodle Ipsum](https://doodleipsum.com/)
- [Logoipsum](https://logoipsum.com/)

Exemple d’utilisation :

```html
<img src="https://picsum.photos/480/320" alt="" />
```
