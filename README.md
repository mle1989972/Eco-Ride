# EcoRide — TP Développeur Web & Web Mobile

> ## Liens utiles
> • Déploiement Front : https://…  
> • Déploiement API : https://…  
> • Dépôt GitHub (public) : https://github.com/mle1989972/Eco-Ride  
> • Board Kanban (Trello) : https://trello.com/b/a8347yxi/gestion-de-projet-ecoride

## Comptes de test (ECF)
- Admin : admin@ecoride.local / Admin123!
- Employé : employee@ecoride.local / Employee123!
- Chauffeur : driver@ecoride.local / Driver123!
- Passager : rider@ecoride.local / Rider123!

> ⚠️ Ces identifiants sont destinés au jury.  

---

## Livrables

Tous les livrables exigés par l’énoncé sont présents dans le dossier [`/livrables`](./livrables/).

- [Manuel d’utilisation](./livrables/Manuel_Utilisation.pdf)  
- [Charte graphique](./livrables/Charte_Graphique.pdf)  
- [Documentation technique](./livrables/Documentation_Technique.pdf)  
- [Documentation de gestion de projet](./livrables/Gestion_Projet.pdf)  
- [Wireframes](./livrables/Wireframes/)  
- [Mockups](./livrables/Mockups/)  

---

Projet **back + front** pour une plateforme de covoiturage.  
Objectifs ECF couverts : authentification, recherche et publication de trajets, participation avec double confirmation, gestion des crédits, avis & modération, incidents (employé), administration (employés + statistiques), **front statique** (HTML/CSS/JS), **base relationnelle (PostgreSQL)** et **NoSQL (MongoDB)**.

---

## Stack technique

- **Backend** : Node.js (ESM) / Express, PostgreSQL (pg), JWT (jsonwebtoken), Joi (validation), Nodemailer (emails)
- **NoSQL** : MongoDB (journalisation d’événements via `src/mongo/`)
- **Frontend** : HTML5 + CSS + JS (fetch), statique servi par Express (`/public`)
- **Sécurité** : Helmet, CORS, gestion d’erreurs centralisée
- **Outils** : Docker Compose (Postgres, Mongo, Mailhog, App), Vitest + Supertest (tests)

---

## Arborescence

```
Eco-Ride/
├── livrables/           # Livrables ajoutés
│   ├── Manuel_Utilisation.pdf
│   ├── Charte_Graphique.pdf
│   ├── Documentation_Technique.pdf
│   ├── Gestion_Projet.pdf
│   ├── Wireframes/
│   └── Mockups/
├── docs/
│   └── schema.sql
├── docker/
│   └── postgres/
│       └── init/
│           ├── 01-schema.sql
│           └── 02-seed.sql
├── public/
│   ├── index.html
│   ├── login.html
│   ├── register.html
│   ├── trip.html
│   ├── dashboard.html
│   ├── employee.html
│   ├── admin.html
│   └── assets/
│       ├── styles.css
│       ├── main.js
│       ├── login.js
│       ├── register.js
│       ├── trip.js
│       ├── dashboard.js
│       ├── employee.js
│       └── admin.js
├── scripts/
│   └── createAdmin.js
├── src/
│   ├── server.js
│   ├── app.js
│   ├── config/
│   │   └── db.js
│   ├── middlewares/
│   │   ├── auth.js
│   │   ├── errorHandler.js
│   │   ├── roles.js
│   │   └── validate.js
│   ├── routes/
│   │   ├── index.js
│   │   ├── admin.js
│   │   ├── auth.js
│   │   ├── participations.js
│   │   ├── reviews.js
│   │   ├── trips.js
│   │   ├── vehicles.js
│   │   ├── preferences.js
│   │   └── incidents.js
│   ├── controllers/
│   │   ├── adminController.js
│   │   ├── authController.js
│   │   ├── participationsController.js
│   │   ├── reviewsController.js
│   │   ├── tripsController.js
│   │   ├── vehiclesController.js
│   │   ├── preferencesController.js
│   │   └── incidentsController.js
│   ├── emails/
│   │   └── mailer.js
│   ├── mongo/
│   │   ├── client.js
│   │   └── log.js
│   ├── seed/
│   │   └── seed.sql
│   ├── tests/
│   │   ├── health.test.js
│   │   ├── auth.test.js
│   │   └── trips.test.js
│   └── utils/
│       └── credits.js
├── docker-compose.yml
├── Dockerfile
├── package.json
└── README.md
```

---

## Prérequis

- Node.js 18+ (recommandé : 20)
- PostgreSQL 14+
- (Optionnel) MongoDB 6+
- (Optionnel) Docker + Docker Compose

---

## Variables d’environnement (`.env`)

Copier `.env.example` vers `.env` puis compléter :

```
DATABASE_URL=postgres://user:pass@localhost:5432/ecoride
JWT_SECRET=change-me
# SMTP (optionnel - Mailhog en dev)
SMTP_HOST=localhost
SMTP_PORT=1025
SMTP_USER=
SMTP_PASS=
SMTP_FROM="EcoRide <no-reply@ecoride.local>"
# NoSQL (optionnel)
MONGODB_URI=mongodb://localhost:27017/ecoride
```

---

## Installation (local)

1) **Installer les dépendances**
```bash
npm install
```

2) **Créer la base** et le schéma
```bash
psql "$DATABASE_URL" -f docs/schema.sql
# (optionnel) données de démo
psql "$DATABASE_URL" -f src/seed/seed.sql
```

3) **Lancer l’app**
```bash
npm start
# Service: http://localhost:3000
```

4) **Créer un admin**
```bash
node scripts/createAdmin.js --email=admin@ecoride.local --pseudo=Admin --password=Admin123!
```

---

## Démarrage via Docker

1) **Lancer la stack**
```bash
docker compose up -d
```

- App : http://localhost:3000  
- Postgres : 5432 (DB `ecoride` / `ecoride` / `ecoride`)  
- Mongo : 27017  
- Mailhog (emails de dev) : http://localhost:8025

2) **Créer un admin dans le conteneur**
```bash
docker compose exec app node scripts/createAdmin.js --email=admin@ecoride.local --pseudo=Admin --password=Admin123!
```

---

## Parcours front

- `GET /` → page d’accueil (index.html) : recherche trajets + suggestion si aucun résultat
- `GET /trip.html?id=...` : détail trajet + double confirmation de participation
- `GET /login.html` / `GET /register.html`
- `GET /dashboard.html` : véhicules (CRUD), préférences, créer un trajet, mes trajets
- `GET /employee.html` : incidents, modération avis (employé/admin)
- `GET /admin.html` : gestion employés + statistiques trajets/crédits

---

## API — endpoints principaux

### Auth
- `POST /api/auth/register`
- `POST /api/auth/login`

### Santé
- `GET /api/health`

### Trajets & Participations
- `GET /api/trips` (filtres: ville, date, éco, prix, durée, note)
- `GET /api/trips/:id`
- `POST /api/trips` *(auth)*
- `POST /api/trips/:id/participations` *(auth)* — double confirmation

### Véhicules
- CRUD complet `/api/vehicles`

### Préférences
- `GET /api/preferences`
- `PUT /api/preferences`

### Avis
- `POST /api/reviews`
- `GET /api/reviews/pending`
- `POST /api/reviews/:id/moderate`

### Incidents
- `POST /api/incidents`
- `GET /api/incidents`
- `PATCH /api/incidents/:id`

### Admin
- `POST /api/admin/employees`
- `POST /api/admin/suspend/:userId`
- `GET /api/admin/stats`

---

## Tests (Vitest + Supertest)

Tests disponibles :
- `src/tests/health.test.js`
- `src/tests/auth.test.js`
- `src/tests/trips.test.js`

Lancer les tests :
```bash
npm run test
npm run test:watch
```

---

## Rôles & sécurité

- Rôles : `user` (défaut), `employee`, `admin`
- Authentification : JWT (Bearer Token)
- Middlewares de contrôle d’accès
- Emails : via SMTP (ou Mailhog en dev)

---

## Déploiement

- Image Docker `Dockerfile`
- Variables d’env à configurer : `DATABASE_URL`, `JWT_SECRET`, `MONGODB_URI`, SMTP
- Prévoir un reverse-proxy (Caddy/Nginx) + HTTPS

---

## Conseils & troubleshooting

- **Statique non servi** → vérifier `express.static` dans `src/app.js`
- **401 Unauthorized** → vérifier Authorization: Bearer + `JWT_SECRET`
- **Emails en dev** → Mailhog : http://localhost:8025
- **Base vide** → rejouer `docs/schema.sql` et `src/seed/seed.sql`

---

## 📜 Licence

Projet pédagogique dans le cadre de l’ECF TP DWWM.
