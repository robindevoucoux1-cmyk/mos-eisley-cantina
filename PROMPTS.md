# PROMPTS.md

## Ex02 — Features grid (Cursor inline edit, Cmd+K)

### Prompt exact utilisé

```
Stack: single static HTML file using the Tailwind Play CDN (no build step, no custom config,
utility classes only).

Fill the selected empty <section id="features"> with a features grid:

- Keep the section wrapper, its id, and aria-labelledby as they are.
- Fill the <h2 id="features-title"> with "House rules" and style it as a section heading.
- Below the heading, a grid container: grid grid-cols-1 md:grid-cols-3 gap-6.
- One <article> per card, 3 cards total.
- Each card: dark glass palette bg-white/[0.03] border border-white/10 backdrop-blur,
  rounded corners, inner padding, and a hover lift with hover:-translate-y-1 (add a transition).
- Each card starts with an icon box: size-12 rounded-xl bg-violet-500/10 ring-1 ring-violet-400/20,
  centering an inline SVG icon (aria-hidden="true").
- Then an <h3> for the title and a <p> for the description.
- Any link must have a visible focus-visible:ring-2 with ring-offset on the slate-950 background.

Use this exact copy:
1. "Live music nightly." — "From sundown to sunrise, loud enough to drown out a bounty hunter."
2. "Smugglers welcome." — "No questions asked. Booths in the back, no records kept."
3. "Droids: see house policy." — "Limits on the dance floor. Powering down recommended."
```

### Corrections apportées après la génération

- **`hover:-translate-y-1` sans transition** : l'effet de levée était instantané et saccadé.
  Ajout de `transition duration-200` sur chaque `<article>` pour que le mouvement soit animé.
- **Classes inventées supprimées** : la génération avait ajouté des utilitaires qui n'existent pas
  dans Tailwind et n'avaient donc aucun effet visible dans le navigateur (vérifié avec l'inspecteur :
  aucune règle CSS générée). Remplacées par les équivalents réels
  (`shadow-lg`, `hover:border-white/20`).
- **Liens « Learn more » non demandés** : l'IA avait ajouté un lien en bas de chaque carte.
  Supprimés, car la consigne fixe le texte exact des cartes (icône + titre + paragraphe uniquement).
- **Boîte d'icône qui ne centrait pas l'icône** : `size-12 rounded-xl ...` était présent mais sans
  contexte flex. Ajout de `flex items-center justify-center` pour centrer le SVG.
- **Hiérarchie des titres** : les titres de cartes étaient en `<h2>`. Passés en `<h3>` pour rester
  sous le `<h2 id="features-title">` de la section.
- **Marges gérées par le parent** : des `mb-*` sur les cartes doublonnaient avec `gap-6` de la
  grille. Retirés pour laisser le `gap` gérer l'espacement.
