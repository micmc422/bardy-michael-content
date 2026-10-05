# Génération d'images de couverture — Nano Banana (FAL)

Méthode automatisée pour générer les illustrations des articles/projets via le modèle `fal-ai/nano-banana-pro` (Nano Banana Pro) hébergé sur FAL, payé avec les crédits de l'abonnement Nous Research.

## Prérequis

- Token Nous Research dans `~/.hermes/auth.json` → `providers.nous.access_token`
- `sharp` installé (déjà présent dans le projet)
- Dépôt de contenu `bardy-michael-content` initialisé (sous-module `content/`)

## Pipeline en 4 étapes

### 1. Génération via FAL

Le modèle `fal-ai/nano-banana-pro` s'appelle en 3 requêtes HTTP :

```python
import json, urllib.request, time

TOK = json.load(open('/home/occitaweb/.hermes/auth.json'))['providers']['nous']['access_token']
BASE = "https://fal-queue-gateway.nousresearch.com"
MODEL = "fal-ai/nano-banana-pro"

# 1. Soumettre le prompt
payload = json.dumps({
    "prompt": prompt,
    "num_images": 1,
    "aspect_ratio": "16:9",
    "output_format": "png"
}).encode()
req = urllib.request.Request(f"{BASE}/{MODEL}", data=payload, method="POST",
    headers={"Authorization": f"Bearer {TOK}", "Content-Type": "application/json"})
rid = json.loads(urllib.request.urlopen(req, timeout=120).read())["request_id"]

# 2. Polling du statut
url = f"{BASE}/{MODEL}/requests/{rid}/status"
while True:
    req = urllib.request.Request(url, headers={"Authorization": f"Bearer {TOK}"})
    st = json.loads(urllib.request.urlopen(req, timeout=30).read()).get("status")
    if st == "COMPLETED": break
    if st in ("FAILED", "ERROR"): raise Exception("Generation failed")
    time.sleep(5)

# 3. Récupérer l'image
req = urllib.request.Request(f"{BASE}/{MODEL}/requests/{rid}",
    headers={"Authorization": f"Bearer {TOK}"})
img_url = json.loads(urllib.request.urlopen(req, timeout=60).read())["images"][0]["url"]
# Télécharger img_url -> fichier local
```

### 2. Prompt

Le prompt combine un **thème** (spécifique à l'article) et un **STYLE commun** fixe :

```
Isometric 3D illustration, 16:9 landscape, designed as a full-bleed background.
Style: isometric 3D illustration, clean geometric volumes, soft ambient occlusion, subtle material shading, modern tech aesthetic.
Color palette: deep dark navy #0B1220 to #1A1030 gradient background, luminous teal #14B8A6 and violet #9900ff accents, warm orange #FA541C highlights.
IMPORTANT: the overall image must be DARK and low-contrast in the LEFT HALF (a dark veil will be overlaid there for white text), with the main object and its brightest highlights weighted to the RIGHT HALF.
Composition: single hero object, all elements fully inside the frame with clear margin.
Style reference: modern isometric tech illustration, no photorealism, no people, no faces.
IMPORTANT: absolutely no text, no letters, no words, no numbers anywhere in the image.
```

Le thème décrit le concept de l'article en une phrase + une métaphore visuelle.

### 3. Optimisation (sharp)

Deux fichiers produits depuis le PNG généré :

```javascript
import sharp from "sharp";

const src = "chemin/vers/image-generee.png";
const dir = "content/blog/<slug>";

// WebP : servi sur le site (léger, ~26 Ko)
await sharp(src).resize(1200, 630, { fit: "cover" })
  .webp({ quality: 82, effort: 6 }).toFile(`${dir}/image.webp`);

// PNG : réservé à la route OG (satori ne lit pas le WebP, ~260 Ko)
await sharp(src).resize(1200, 630, { fit: "cover" })
  .png({ compressionLevel: 9, palette: true, quality: 90 }).toFile(`${dir}/image.png`);
```

### 4. Installation

- Les deux fichiers vont dans `content/blog/<slug>/` du dépôt de contenu
- Le frontmatter MDX et les `![]()` du corps pointent vers `image.webp`
- Le `image.png` reste à côté pour la route OG (satori)

## Mise à jour du frontmatter MDX

```python
slug = "<slug-de-l-article>"
txt = open(f"content/content/blog/{slug}.mdx", encoding="utf-8").read()
txt = txt.replace(f"/blog/{slug}/image.png", f"/blog/{slug}/image.webp")
open(f"content/content/blog/{slug}.mdx", "w", encoding="utf-8").write(txt)
```

## Vérifications

- [ ] Image WebP ~26 Ko, PNG ~260 Ko dans `content/blog/<slug>/`
- [ ] Frontmatter `image:` pointe vers `.webp`
- [ ] Corps MDX `![]()` pointe vers `.webp`
- [ ] Route OG `/og?type=post&slug=<slug>` renvoie 200 avec l'illustration
- [ ] Proxy `/api/content-image/blog/<slug>/image.webp` renvoie 200

## Articles traités

| Slug | Statut |
|---|---|
| `pourquoi-le-ssg-avec-next-js-accelere-votre-site-et-votre-ca` | WebP + PNG |
| `protocole-flight-de-react-comment-livrer-des-sites-next-js-plus-rapide` | WebP + PNG |
| 6 autres (session du 4 oct.) | WebP + PNG |

## Notes

- Le PNG de l'OG n'est jamais servi aux visiteurs — il n'est lu que par le serveur pour composer l'image de partage
- Le site ne charge que le WebP (~26 Ko contre ~500 Ko pour l'ancien PNG)
- Les prompts par article sont dans `cover-prompts.md` (pour référence manuelle)
