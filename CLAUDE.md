# The Stroller — Site vitrine de Lo

## Ce projet

Site vitrine / portfolio pour Lo, content creator et foodie concierge basee a Lisbonne. Le site presente ses services (creation de contenu pour restaurants/cafes/hotels, experiences foodie, concierge) et permet aux clients potentiels de la contacter.

Utilisateur : fondateur solo, non-developpeur. Toute modification passe par Claude ou par upload direct sur GitHub.

---

## Architecture du site

Site statique pur (HTML/CSS/JS, pas de framework). 6 pages :

| Fichier | Role |
|---------|------|
| `index.html` | Page d'accueil — hero + selection des services |
| `about.html` | A propos de Lo |
| `portfolio.html` | Portfolio video — 11 videos verticales (format TikTok/Reels) avec filtres |
| `content-creation.html` | Service B2B — creation de contenu pour venues et marques |
| `foodie-experience.html` | Service B2C — foodie concierge et date night concierge |
| `bookme.html` | Page de contact / reservation |
| `contact.html` | Redirection vers bookme.html (legacy) |

### Assets
- `assets/` — images, logos, fonts (Averia Serif Libre), videos
- `assets/portfolio-smash/` — videos du portfolio (ajoutees apres la v1)
- Videos : format vertical 9:16, MP4, generalement < 2 Mo chacune

### Technologies
- **Tailwind CSS** via CDN (cdn.tailwindcss.com) — version dev, a migrer vers CSS compile
- **Iconify** pour les icones
- **petite-vue** (v0.4.1) sur index.html uniquement
- Palette : vert `#5db689`, bleu `#00a8f0`, rouge `#ee7963`, dark `#0a0a0a`, light `#eeefea`

---

## Hebergement et infra

| Composant | Service | Detail |
|-----------|---------|--------|
| Hebergement | **Cloudflare Pages** | Gratuit, bande passante illimitee |
| Repo GitHub | `github.com/maxime-cln/site_thestroller` | Fork de `orsoneveraert/site_lo_codex` |
| Domaine | `thestroller.me` | Achete sur **GoDaddy** (compte Lo) |
| DNS / Nameservers | **Cloudflare** | `grannbo.ns.cloudflare.com` + `rajeev.ns.cloudflare.com` |
| SSL | Cloudflare (automatique) | Certificat universel gratuit |
| Formulaires | **FormSubmit.co** | Soumissions envoyees a `strollinglisbon@gmail.com` |
| Analytics | **Cloudflare Web Analytics** | Integre, sans cookie, gratuit |
| URL de preview | `site-thestroller.pages.dev` | Toujours accessible |

### Deploiement
Chaque push sur la branche `main` du repo GitHub declenche un deploiement automatique sur Cloudflare Pages (~30 secondes).

### Pour modifier le site
1. Modifier les fichiers (via Claude, GitHub direct, ou en local)
2. Upload sur GitHub (Add file > Upload files, ou commit direct dans le navigateur)
3. Cloudflare deploie automatiquement

---

## Formulaires

3 formulaires connectes a FormSubmit.co (envoi a `strollinglisbon@gmail.com`) :
- `bookme.html` — formulaire de contact principal (nom, email, sujet, WhatsApp, message)
- `content-creation.html` — formulaire pour les marques/venues
- `foodie-experience.html` — formulaire pour les experiences foodie

Configuration FormSubmit dans chaque formulaire :
- `action="https://formsubmit.co/strollinglisbon@gmail.com"`
- `method="POST"`
- Champs caches : `_subject` (sujet de l'email), `_next` (page de redirection apres envoi)

**Important** : au premier envoi, FormSubmit envoie un email de confirmation a Lo. Elle doit cliquer "Confirm" pour activer la reception.

---

## Decisions prises et pourquoi

| Decision | Raison |
|----------|--------|
| Cloudflare Pages plutot que Netlify | Bande passante illimitee gratuite. Netlify a un systeme de credits (300/mois) qui coupe le site quand epuises. |
| Cloudflare Pages plutot que GitHub Pages | GitHub Pages interdit l'usage commercial. |
| Cloudflare Pages plutot que Vercel | Vercel gratuit = non-commercial uniquement. |
| FormSubmit.co plutot que Formspree | Illimite et sans inscription vs 50 soumissions/mois. |
| Pas de Cloudflare R2 pour l'instant | Les videos font < 2 Mo, bien sous la limite de 25 Mo/fichier de Pages. |
| Pas de migration Hugo pour l'instant | Le site fonctionne, la migration retarderait la mise en ligne. A reconsiderer si la maintenance devient lourde. |

---

## Corrections appliquees (2026-03-16)

- [x] Formulaires connectes a FormSubmit.co (etaient en mode prototype)
- [x] Liens sociaux corriges dans le footer du portfolio (TikTok, Instagram pointaient vers #)
- [x] Liens Privacy/Terms placeholder supprimes du portfolio
- [x] Titres de page uniques + meta descriptions ajoutees pour le SEO

## A faire (non urgent)

- [ ] Compiler Tailwind CSS (remplacer le CDN dev par un fichier CSS statique)
- [ ] Ajouter les balises Open Graph (previews quand le site est partage sur les reseaux)
- [ ] Ajouter un favicon
- [ ] Tester les formulaires (declencher l'email de confirmation FormSubmit)
- [ ] Verifier le poids des 8 videos dans `portfolio-smash/`

---

## Comptes et acces

| Service | Compte | Qui a acces |
|---------|--------|-------------|
| GitHub | maxime-cln | Maxime |
| Cloudflare | strollinglisbon@gmail.com | Lo / Maxime |
| GoDaddy | compte de Lo | Lo |
| FormSubmit | pas de compte (lie a l'email) | Lo (via email) |
