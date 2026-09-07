# AGENTS.md — Contenu du site portfolio Michaël Bardy (occitaweb.fr)

> Fichier auto-chargé par les agents IA (Hermes, Copilot, Claude Code…). Source de vérité : le code.
> Dépôt associé : `bardy-michael-portfolio-cv` (site Next.js)
> Guideline rédaction : `docs/articles-guideline.md` · Index : `llms.txt`

## Rôle de ce dépôt

Dépôt de **contenu** du site portfolio/CV de Michaël Bardy, développeur web freelance à Albi (activité Occitaweb). Les fichiers MDX versionnés ici sont consommés dynamiquement par le site Next.js via l'API GitHub (raw.githubusercontent.com + cache ISR avec `unstable_cache`, revalidate 3600s).

**Pas de rebuild du site nécessaire** pour modifier le contenu : le site lit les MDX à la volée depuis ce dépôt distant.

## Structure

```
content/
├── blog/          # Articles au format MDX (frontmatter YAML + JSX)
│   └── <slug>.mdx # = un article
├── projects/      # Projets au format MDX
│   └── <slug>.mdx
├── ideas.json     # Brouillons / idées d'articles (non versionnés en prod)
blog/              # Images de couverture (copiées dans public/blog du site en dev)
articles/          # Brouillons non versionnés (workflow local)
docs/              # Documentation (guidelines, etc.)
```

## Pipeline de contenu

1. **Création** : un article est créé dans `content/blog/<slug>.mdx` (frontmatter YAML + corps MDX/JSX)
2. **Images** : les images de couverture sont placées dans `blog/<slug>/<uuid>.png` (UUID fixe : `2d89acac-7cff-46da-a8e0-6c0cba53f22c`)
3. **Aperçu dev** : en développement, le site copie `blog/` vers `public/blog/` et affiche l'article via `/blog/apercu/<slug>`
4. **Production** : le site récupère les MDX via l'API GitHub (raw) avec cache ISR 3600s

## Format MDX

### Frontmatter YAML

```yaml
---
titre: "Titre de l'article"
description: "Meta description 150-160 caractères."
publishedAt: 2026-09-07T10:00:00.000Z
image: "/blog/<slug>/2d89acac-7cff-46da-a8e0-6c0cba53f22c.png"
tags: ["tag1", "tag2"]
author: "Michaël Bardy"
---
```

### Composants disponibles dans le corps

Le composant `<Faq />` (accordéon + JSON-LD FAQPage automatique pour SEO) est disponible directement en JSX :

```jsx
<Faq title="FAQ" faq={[
  { title: "Question ?", content: "Réponse." },
]} />
```

Les composants Once UI (`Heading`, `Text`, `CodeBlock`, `Table`, etc.) sont enregistrés dans le registre MDX du site et peuvent être utilisés en JSX.

## Images de couverture

- **UUID fixe** : toutes les couvertures utilisent le même nom de fichier `2d89acac-7cff-46da-a8e0-6c0cba53f22c.png` (ou `.jpg`)
- **Chemin** : `/blog/<slug>/2d89acac-7cff-46da-a8e0-6c0cba53f22c.png` dans le frontmatter
- **En dev** : copier l'image dans `public/blog/<slug>/` du dépôt site
- **En prod** : le site récupère l'image via `/api/content-image/...` depuis ce dépôt

## Conventions

- **Pas de `#` (h1)** dans le corps : le titre vient du frontmatter
- **Ton** : français, vouvoiement pro, orienté freelance/PME locale (Albi/Occitanie)
- **Sections** : `##` et `###` génèrent des ancres cliquables + table des matières automatique
- **Fences** : utiliser ` ```lang ` (ex: ` ```js `) pour les blocs de code — le site compile correctement
- **Liens internes** : chemins relatifs (`/blog/...`, `/realisations/...`)

## Pièges connus

- Le chemin `content/blog/` (et non `blog/`) dans ce dépôt correspond aux articles du site
- Les articles dans `articles/` sont des brouillons non versionnés (workflow local uniquement)
- `ideas.json` n'est pas exposé en production — il sert de carnet d'idées local
- Les images dans `blog/` sont copiées vers `public/blog/` du site en dev via `sync-content.mjs` (ou manuellement)