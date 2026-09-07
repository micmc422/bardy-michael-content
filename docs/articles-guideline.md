# Guideline — Rédaction d'articles de blog (MDX + Next.js)

> Workflow : créer un fichier `.mdx` dans `content/blog/`, prévisualiser en dev sur `/blog/apercu/<slug>` (si présent dans `articles/`), et pousser sur main. Le site Next.js récupère les MDX dynamiquement via l'API GitHub (raw.githubusercontent.com + cache ISR 3600s). Pas de rebuild nécessaire.

## 1. Structure d'un article

### Frontmatter YAML (obligatoire)

```yaml
---
title: "Titre de l'article"
description: "Meta description 150-160 caractères. Résumé qui apparaît dans les cartes de liste et les moteurs de recherche."
publishedAt: 2026-09-07T10:00:00.000Z
updatedAt: 2026-09-07T10:00:00.000Z
image: "/blog/<slug>/2d89acac-7cff-46da-a8e0-6c0cba53f22c.png"
tags: ["tag1", "tag2", "tag3"]
author: "Michaël Bardy"
---
```

- `title` : h1 de la page (généré automatiquement, pas de `#` dans le corps)
- `description` : meta description, OG/Twitter, JSON-LD, résumé des cartes (150-160 car.)
- `publishedAt` / `updatedAt` : dates ISO 8601, tri des listes, JSON-LD `datePublished`/`dateModified`
- `image` : chemin `/blog/<slug>/<uuid>.png` — voir section Images
- `tags` : 2-4 tags, cliquables sur le site (`/blog/tags/<name>`)
- `author` : nom affiché (défaut : Michaël Bardy)

### Corps de l'article

- **Pas de `#` (h1)** dans le corps : le titre vient du frontmatter. Commencer à `##`.
- Les `##`/`###` génèrent des ancres cliquables (slug auto) → table des matières `HeadingNav` automatique.
- Paragraphes courts (2-4 phrases).
- Tableaux markdown (GFM) supportés → convertis en `Table` Once UI.
- `---` pour les séparations de sections.
- Terminer idéalement par une section FAQ (composant `<Faq />`) : bonus SEO (rich snippets).

## 2. Composants disponibles

### `<Faq />` — Accordéon + JSON-LD FAQPage (recommandé en fin d'article)

```jsx
<Faq title="FAQ : sujet de l'article" faq={[
  {
    title: "Question fréquente ?",
    content: "Réponse détaillée."
  },
  {
    title: "Autre question ?",
    content: "Autre réponse."
  }
]} />
```

Le composant génère automatiquement le JSON-LD `FAQPage` pour les rich snippets Google.

### `<Steps />` — Étapes numérotées + JSON-LD ItemList

```jsx
<Steps title="Procédure" steps={[
  { title: "Étape 1", content: "Description." },
  { title: "Étape 2", content: "Description." }
]} />
```

### Composants Once UI (registrement MDX)

Disponibles en JSX dans le corps : `Heading`, `Text`, `CodeBlock`, `InlineCode`, `Accordion`, `AccordionGroup`, `Table`, `Feedback`, `Button`, `Card`, `Grid`, `Row`, `Column`, `Icon`, `Media`, `SmartLink`, `OgCard`, `RDV`.

## 3. Blocs de code

Utiliser les fences markdown standard avec langage :

```js
// Code JavaScript
const x = 1;
``````

```bash
pnpm dev
``````

```css
.clamp {
  font-size: clamp(1rem, 2vw, 2rem);
}
``````

Le site compile correctement les fences (pas de restriction comme avec Wisp).

## 4. Liens

### Liens internes

```md
[Article sur Next.js](/blog/mon-article)
[Voir les projets](/realisations)
```

### Liens magiques (automatiquement transformés)

| URL du lien | Rendu automatique |
|---|---|
| `https://github.com/owner/repo.git` (finit par `.git`) | Carte résumé du repo GitHub (`GitHubRepoSummary`) |
| `https://raw.githubusercontent.com/...` | Bloc de code du fichier distant (`RawGithubFile`) |
| `https://codepen.io/...` | Embed CodePen (iframe 300px) |
| `/chemin-interne` | `SmartLink` Next.js |

## 5. Images et médias

### Image de couverture (obligatoire)

- **UUID fixe** : toutes les couvertures utilisent `2d89acac-7cff-46da-a8e0-6c0cba53f22c.png`
- **Emplacement** : `blog/<slug>/2d89acac-7cff-46da-a8e0-6c0cba53f22c.png` dans ce dépôt
- **Chemin frontmatter** : `/blog/<slug>/2d89acac-7cff-46da-a8e0-6c0cba53f22c.png`
- **En prod** : le site récupère l'image via `/api/content-image/...` (proxy GitHub)
- **En dev** : copier l'image dans `public/blog/<slug>/` du dépôt site

### Images dans le corps

```md
![Texte alternatif descriptif](/images/blog/image.png)
```

- Toujours renseigner l'alt (accessibilité + SEO)
- Héberger dans `public/images/blog/` du site ou via URL externe (imagedelivery.net, etc.)

## 6. Structure type d'un article

```mdx
Intro accrocheuse (2-3 phrases, la description ne doit PAS être recopiée mot à mot).

## Première section

Contenu…

```js:exemple.js
// Code commenté
```

## Deuxième section

![alt descriptif](url-image)

## Troisième section

Contenu avec <Faq title="FAQ" faq={[
  { title: "Question ?", content: "Réponse." }
]} />
```

## 7. Checklist avant push

- [ ] Frontmatter complet (title, description 150-160c, publishedAt, image, tags, author)
- [ ] Aucun `#` h1 dans le corps
- [ ] Image de couverture présente dans `blog/<slug>/2d89acac-7cff-46da-a8e0-6c0cba53f22c.png`
- [ ] Fences avec langage (`js`, `ts`, `bash`, `css`, `html`…)
- [ ] Alt sur toutes les images
- [ ] Liens internes en chemin absolu (`/blog/...`, `/realisations/...`)
- [ ] Ton : français, vouvoiement pro, orienté freelance/PME locale (Albi/Occitanie)
- [ ] Composant `<Faq />` en fin d'article (recommandé pour SEO)