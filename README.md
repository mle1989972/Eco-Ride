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

## 📦 Livrables

Tous les livrables exigés par l’énoncé sont présents dans le dossier [`/livrables`](./livrables/).

- [Manuel d’utilisation](./livrables/Manuel_Utilisation.pdf)  
- [Charte graphique](./livrables/Charte_Graphique.pdf)  
- [Documentation technique](./livrables/Documentation_Technique.pdf)  
- [Documentation de gestion de projet](./livrables/Gestion_Projet.pdf)  
- [Wireframes](./livrables/Wireframes/)  
- [Mockups](./livrables/Mockups/)  

---

## 🧱 Stack technique

- **Backend** : Node.js (ESM) / Express, PostgreSQL (pg), JWT (jsonwebtoken), Joi (validation), Nodemailer (emails)  
- **NoSQL** : MongoDB (journalisation d’événements via `src/mongo/`)  
- **Frontend** : HTML5 + CSS + JS (fetch), statique servi par Express (`/public`)  
- **Sécurité** : Helmet, CORS, gestion d’erreurs centralisée  
- **Outils** : Docker Compose (Postgres, Mongo, Mailhog, App), Vitest + Supertest (tests)  

---

## 📂 Arborescence

```
Eco-Ride/
├── livrables/           # <-- Nouveaux livrables ajoutés
│   ├── Manuel_Utilisation.pdf
│   ├── Charte_Graphique.pdf
│   ├── Documentation_Technique.pdf
│   ├── Gestion_Projet.pdf
│   ├── Wireframes/
│   └── Mockups/
├── docs/
│   └── schema.sql
├── docker/
│   └── postgres/init/01-schema.sql
│                      02-seed.sql
├── public/              # Front statique (HTML/CSS/JS)
├── src/                 # Code backend Node/Express
├── docker-compose.yml
├── Dockerfile
├── package.json
└── README.md
```

---

## ⚙️ Prérequis
- Node.js 18+ (recommandé : 20)  
- PostgreSQL 14+  
- (Optionnel) MongoDB 6+  
- (Optionnel) Docker + Docker Compose  

---

## 🔐 Variables d’environnement (`.env`)
*(inchangé, voir fichier `.env.example`)*  

---

## 🛠️ Installation locale
*(inchangé : `npm install`, `psql docs/schema.sql`, `npm start`)*  

---

## 🐳 Utilisation avec Docker
*(inchangé : `docker compose up -d`, accès http://localhost:3000 et http://localhost:8025)*  

---

## 🧭 Parcours front
*(inchangé : index, login, register, dashboard, employee, admin)*  

---

## 🔌 API — endpoints principaux
*(inchangé)*  

---

## 🧪 Tests
*(inchangé : vitest + supertest)*  

---

## 🔒 Rôles & sécurité
*(inchangé)*  

---

## 🚀 Déploiement
*(inchangé : Dockerfile + variables d’env)*  

---

## 📜 Licence
Projet pédagogique dans le cadre de l’ECF TP DWWM.

