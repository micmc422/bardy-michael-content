# Veille éditoriale — Octobre & Novembre 2026

> Plan de publication pour occitaweb.fr. Cadence cible : **1 article/semaine** (rythme observé juillet→septembre 2026).
> Période couverte : **semaine du 6 octobre → semaine du 24 novembre 2026** (8 articles).
> Sources vérifiées le 4 octobre 2026. Chaque sujet a une source primaire à citer dans l'article.

## Contexte éditorial

- **25 articles publiés**, dernier le 8 septembre 2026.
- **Tags dominants** : Next.js (6), performance (5), SEO (4), WordPress (3), Vercel (3).
- **Angle du site** : développeur web à Albi, cible TPE/PME et artisans locaux, ton « je vous explique sans jargon ».
- **Formats qui marchent** : guide pratique, retour d'expérience client, décryptage d'une actu technique.
- **Trous identifiés** dans le corpus : accessibilité, Core Web Vitals en détail, coût total de possession, IA et recherche locale, sécurité.

---

## Semaine 1 — 7 octobre 2026

### 1. Accessibilité numérique : qui est vraiment obligé en 2026 (et ce que ça change pour votre site)

**Angle** : lever la confusion entre la loi française de 2005 (seuil 250 M€) et l'European Accessibility Act (EAA, applicable depuis le 28 juin 2025, seuil 10 salariés / 2 M€, secteurs ciblés dont l'e-commerce). Beaucoup de dirigeants croient être concernés — ou pas — à tort.

**Points à traiter**
- Les deux régimes juridiques distincts : article 47 loi 2005-102 vs article 16 loi 2023-171 (transposition EAA).
- Seuils : 250 M€ de CA en France (personne morale, pas groupe consolidé) vs 10 salariés + 2 M€ dans les secteurs EAA.
- Exemption micro-entreprise : < 10 salariés **et** < 2 M€.
- Un site vitrine informatif peut rester hors obligation ; dès qu'il y a paiement, réservation ou espace client → service numérique soumis.
- Les 4 livrables : déclaration d'accessibilité, schéma pluriannuel (3 ans max), plan d'action annuel, bilan annuel.
- Sanctions : jusqu'à 50 000 € + 25 000 € pour défaut de publication.
- RGAA 4.1.2 est la référence ; RGAA 5 prévu fin 2026.

**Sources** : accessibilite.numerique.gouv.fr (champ d'application) · rgaa-ia.fr · numerique.gouv.fr (RGAA 5)

**Tags** : `accessibilite`, `rgpd`, `conformite`
**Composants** : `<Faq />` (3-4 questions), tableau comparatif des deux régimes

---

## Semaine 2 — 14 octobre 2026

### 2. Core Web Vitals en 2026 : les 3 chiffres qui décident de votre place sur Google

**Angle** : expliquer LCP / INP / CLS à un dirigeant, avec les vrais seuils et le fait que Google note sur données réelles (CrUX), pas sur Lighthouse.

**Points à traiter**
- Seuils officiels : **LCP ≤ 2,5 s**, **INP ≤ 200 ms**, **CLS ≤ 0,1** — évalués au **75ᵉ percentile** des visites réelles, par type d'appareil.
- Google classe sur le rapport CrUX (28 jours glissants) : un score Lighthouse de 100 ne change rien au classement.
- INP a remplacé FID le 12 mars 2024 — beaucoup de sites n'ont pas été réoptimisés depuis.
- Ce qui casse l'INP : JS bloquant, hydratation lourde, tâches longues sur le thread principal.
- Ce qui casse le LCP : images non optimisées, polices bloquantes, serveur lent.
- Démonstration : mesurer son propre site (PageSpeed Insights + Search Console → rapport Core Web Vitals).
- Contre-vérité à corriger : le seuil LCP **n'est pas passé à 2,0 s** en 2026 (rumeur circulante) — il reste 2,5 s.

**Sources** : developers.google.com/search (Core Web Vitals, FR) · support.google.com/webmasters (rapport CWV) · web.dev

**Tags** : `performance`, `seo`, `core-web-vitals`
**Composants** : tableau des seuils, `<Steps />` pour la méthode de mesure, `<Faq />`

---

## Semaine 3 — 21 octobre 2026

### 3. Votre site est lent ? Voici ce que ça coûte réellement (chiffres 2026)

**Angle** : traduire la performance en euros pour un dirigeant de TPE/PME. Article « business case » plutôt que technique.

**Points à traiter**
- 53 % des visiteurs mobiles quittent une page au-delà de 3 s de chargement.
- Chaque seconde de délai supplémentaire réduit les conversions (~7 %).
- Un site qui charge en 1 s convertit ~3× mieux qu'un site à 5 s.
- Taux de conversion moyen d'un site vitrine PME : 1 à 3 % — en dessous, il y a de la perte.
- Simulation concrète : 500 visiteurs/mois, passage de 3 s à 1,5 s → 3 à 4 contacts supplémentaires/mois, sans toucher au contenu.
- Poids médian d'un site de PME : 2,4 Mo, et 41 % dépassent 3 Mo (confort : < 1,5–2 Mo).
- Le cas des sites WordPress : 76 % du web PME, souvent chargés en plugins.

**Sources** : Baromètre TheWebLead 2026 (1 044 sites PME FR/BE) · Google/DoubleClick · WP Rocket 2025

**Tags** : `performance`, `conversion`, `commerce-local`
**Composants** : tableau avant/après, `<Faq />`

---

## Semaine 4 — 28 octobre 2026

### 4. Google Business Profile et IA : pourquoi votre fiche compte plus que votre site

**Angle** : la recherche locale a changé de nature en 2026. Les AI Overviews et Gemini lisent la fiche Google comme source primaire.

**Points à traiter**
- Les AI Overviews apparaissent sur ~68 % des requêtes à intention locale large, ~7 % des requêtes purement locales.
- **32 % de commerces en moins** dans les packs locaux générés par IA qu'en Map Pack classique → la sélection est plus concentrée.
- Le poids des signaux GBP : 32 % du classement en pack local classique, mais seulement 12 % en visibilité IA — où le **site** pèse le plus (24 %).
- GBP est devenu une source unique : Gemini agrège fiche + site + avis + mentions sociales comme **un seul flux de données** sur l'entité.
- Conséquence pratique : soigner les deux à la fois, pas l'un contre l'autre.
- Actions concrètes : catégories complètes, description 750 car., attributs, horaires, services, photos régulières, réponses aux avis.
- La complétude de la fiche est devenue un facteur de classement plus direct (core update de mars 2026).
- Les avis : analyse du **contenu** des avis par l'IA, pas seulement la note.

**Sources** : poster.ly (GBP guide 2026) · digitalapplied.com (core update mars 2026) · localo.com · Birdeye State of GBP 2026

**Tags** : `seo`, `commerce-local`, `ia`
**Composants** : `<Steps />` (audit de fiche), `<Faq />`

---

## Semaine 5 — 4 novembre 2026

### 5. WordPress ou Next.js en 2026 : le vrai calcul n'est pas le prix de départ

**Angle** : comparer sur le **coût total de possession sur 3 ans**, pas sur le devis initial. Sujet à fort potentiel commercial (le site tourne sous Next.js).

**Points à traiter**
- Le devis initial est plus élevé en Next.js (5 000–15 000 €) qu'en WordPress (2 000–8 000 €).
- Mais la maintenance s'inverse : WordPress = mises à jour core 4-5×/an, plugins hebdomadaires, thème, compatibilité, sauvegardes, sécurité. Next.js = dépendances npm trimestrielles, pas de plugins, pas de BDD à sauvegarder.
- Hébergement : 20–100 €/mois (WP managé) vs 0–20 €/mois (Vercel).
- Plugins premium : 200–1 500 €/an côté WP, 0 côté Next.js.
- Incidents sécurité : coût moyen 800–4 000 € côté WP, quasi nul sur un site statique.
- Le point de bascule se situe vers **mois 14–18**.
- Quand WordPress reste le bon choix : budget < 1 500 €, site vitrine simple, autonomie de publication quotidienne, pas d'ambition technique.
- Quand Next.js s'impose : SEO et performance critiques, fonctionnalités sur mesure, sécurité, scalabilité.
- Nuance honnête : la migration WordPress → Next.js coûte 6 000–12 000 € pour une vitrine, avec un plan de redirections 301 obligatoire (risque de -30 à -60 % de trafic organique sinon).

**Sources** : neuraweb.fr (TCO 3 ans) · lescreavores.fr · freshmarkom.fr (délais/budgets migration) · migratelab.com

**Tags** : `wordpress`, `nextjs`, `performance`
**Composants** : tableau TCO 3 ans, `<Faq />`

---

## Semaine 6 — 11 novembre 2026

### 6. Migrer de WordPress à Next.js sans perdre son référencement : la checklist

**Angle** : guide opérationnel. Complète l'article 5 (qui explique *pourquoi*), celui-ci explique *comment*.

**Points à traiter**
- Inventaire de l'existant : URLs, positions, backlinks, pages qui convertissent.
- Cartographie des redirections 301 — la cause n°1 des pertes de trafic.
- Ce qui doit rester identique : URLs quand c'est possible, balises title/description, structure Hn, contenu.
- Ce qui change : vitesse, rendu, données structurées.
- Ordre de déploiement : préprod indexable bloquée → bascule → vérification Search Console → surveillance 30 jours.
- Les pièges : images non migrées, JSON-LD perdu, canonical mal configuré, sitemap oublié.
- Suivi post-migration : Search Console (couverture, CWV), positions, trafic organique, conversions.
- Délais réalistes : 2-3 semaines (vitrine 5-15 pages), 3-5 semaines (blog 50-500 articles).

**Sources** : freshmarkom.fr · migratelab.com · retour d'expérience interne (le site a été migré)

**Tags** : `wordpress`, `nextjs`, `seo`
**Composants** : `<Steps />` (procédure), tableau des pièges, `<Faq />`

---

## Semaine 7 — 18 novembre 2026

### 7. Ce que Next.js 16.3 change concrètement pour la vitesse de votre site

**Angle** : décryptage d'actu technique, traduit en bénéfices client. Le site tourne sur 16.3.

**Points à traiter**
- Sortie le 3 août 2026. Chiffres vérifiables : jusqu'à **90 % de mémoire en moins** en dev, **22 % de requêtes en plus** sous charge.
- Le changement de fond : les web streams remplacés par les streams natifs Node.js dans le rendu App Router → moins de surcharge à chaque rendu SSR.
- **Instant Navigations** : suite opt-in qui apporte la réactivité d'une SPA sans perdre les Server Components (Stream / Cache / Block).
- **Partial Prefetching** : un shell réutilisable par route, mis en cache côté client.
- Cache disque activé par défaut → builds CI jusqu'à 5,5× plus rapides.
- Ce que ça change pour un client : navigation plus fluide, moins de latence perçue, meilleur INP.
- Ce qui ne change pas : pas de migration nécessaire, gains automatiques.
- Prudence : ne pas survendre — les gains sont mesurés par Vercel sur leurs benchmarks.

**Sources** : nextjs.org/blog/next-16-3 · appwrite.io · technspire.com · digitalapplied.com

**Tags** : `nextjs`, `performance`, `react`
**Composants** : tableau avant/après, `<Faq />`

---

## Semaine 8 — 25 novembre 2026

### 8. Sécurité d'un site web en 2026 : les 5 attaques qui visent réellement les TPE/PME

**Angle** : démystifier. Pas de jargon, des cas concrets, et ce qui protège vraiment.

**Points à traiter**
- Les attaques les plus fréquentes sur les sites de TPE/PME : injection de formulaires, force brute sur l'admin, DDoS volumétrique, dépendances obsolètes, hameçonnage via le formulaire de contact.
- Pourquoi WordPress est une cible privilégiée : écosystème de plugins, surface d'attaque large, mises à jour retardées.
- Ce qui protège réellement : HTTPS, en-têtes de sécurité (CSP, X-Frame-Options, nosniff), mises à jour, sauvegardes testées, principe du moindre privilège.
- Le cas du site statique : surface d'attaque réduite (pas de BDD exposée, pas de PHP).
- Ce qu'il faut faire en cas d'incident : isolation, sauvegarde, rotation des secrets, information.
- Obligations : RGPD (notification sous 72 h en cas de violation de données), et le lien avec l'accessibilité/l'EAA pour les services critiques.
- Checklist de vérification rapide pour un dirigeant.

**Sources** : retours d'expérience internes (DDoS déjà traité dans un article) · documentation OWASP · RGPD art. 33

**Tags** : `securite`, `rgpd`, `performance`
**Composants** : `<Steps />` (checklist), `<Faq />`

---

## Calendrier récapitulatif

| Semaine | Date | Article | Tags |
|---|---|---|---|
| 1 | 7 oct. | Accessibilité : qui est vraiment obligé en 2026 | accessibilite, conformite |
| 2 | 14 oct. | Core Web Vitals : les 3 chiffres qui décident | performance, seo |
| 3 | 21 oct. | Ce que coûte réellement un site lent | performance, conversion |
| 4 | 28 oct. | Google Business Profile et IA | seo, commerce-local, ia |
| 5 | 4 nov. | WordPress vs Next.js : le vrai calcul | wordpress, nextjs |
| 6 | 11 nov. | Migrer de WordPress à Next.js sans perdre son SEO | wordpress, nextjs, seo |
| 7 | 18 nov. | Ce que Next.js 16.3 change concrètement | nextjs, performance |
| 8 | 25 nov. | Sécurité : les 5 attaques qui visent les TPE/PME | securite, rgpd |

## Prolongements possibles (décembre et au-delà)

- **IA et référencement** : comment être cité par ChatGPT / Perplexity quand un client cherche un prestataire local (sujet déjà effleuré, à approfondir avec les données 2026).
- **Formulaires qui convertissent** : réduire les frictions sur la prise de contact (taux d'abandon, nombre de champs, mobile).
- **Contenu et IA générative** : écrire pour être lu ET cité, sans tomber dans le contenu de masse.
- **Hébergement : le vrai coût** (suite de l'article existant sur Vercel).
- **Bilan de performance d'un site après 1 an** : méthode d'audit annuel.

## Notes de production

- **Frontmatter obligatoire** : `title`, `description` (150-160 car.), `publishedAt`, `updatedAt`, `image`, `tags` (2-4), `author`.
- **Image de couverture** : `/blog/<slug>/2d89acac-7cff-46da-a8e0-6c0cba53f22c.png` (UUID fixe).
- **Pas de `#` (h1)** dans le corps — le titre vient du frontmatter.
- **Terminer par `<Faq />`** pour le JSON-LD FAQPage (rich snippets).
- **Liens internes absolus** (`/blog/...`, `/realisations/...`).
- **Chiffres** : chaque donnée citée doit avoir sa source nommée dans le texte — c'est ce qui distingue un article expert d'un contenu généré.
- **Publication** : PR sur `bardy-michael-content`, pas de rebuild du site nécessaire (cache ISR 3600 s).
