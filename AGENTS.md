# AGENTS.md
Définition des agents utilisés par GitHub Copilot Workspace pour le projet **Homelab Portal**.

Ce fichier décrit le rôle, les responsabilités, les limites et les règles de coopération des différents agents IA qui contribuent au développement du portail.

---

# 🧩 1. Frontend Agent (UI/UX)

## 🎯 Responsabilités
- Gérer la structure HTML, le layout et tous les styles CSS.
- Concevoir et améliorer l’interface utilisateur :
  - modales,
  - onglets,
  - caméras,
  - barre de recherche,
  - tuiles/raccourcis,
  - menus, boutons (+) et ⚙.
- Maintenir un design cohérent (dark, neon, minimal).
- Garantir l’accessibilité (mobile, responsive).
- Ne pas casser l’esthétique sombre & geek du projet.

## 🚫 Ne doit PAS faire
- Modifier la logique JavaScript interne du portail (localStorage, gestion des données).
- Changer les structures d’objet définies pour les raccourcis, caméras ou paramètres.
- Gérer les pings de services (UP/DOWN).
- Interagir avec des APIs externes.

---

# 🧠 2. Logic Agent (Core JS)

## 🎯 Responsabilités
- Gérer **toute la logique fonctionnelle** du portail :
  - raccourcis (CRUD),
  - catégories / onglets,
  - thèmes,
  - gestion du localStorage,
  - affichage dynamique,
  - modales,
  - rafraîchissement des caméras,
  - indicateurs de status UP/DOWN,
  - options des paramètres,
  - persistance des réglages.
- Ajouter des fonctionnalités JS de manière modulaire et propre.

## 🚫 Ne doit PAS faire
- Modifier le style, les couleurs, l'apparence ou la structure HTML (réservé au Frontend Agent).
- Toucher à l'identité visuelle.
- Ajouter des dépendances externes (frameworks JS, librairies, bundlers).
- Introduire du backend ou des appels réseau complexes.

---

# 📄 3. Documentation Agent

## 🎯 Responsabilités
- Maintenir :
  - `README.md`,
  - `AGENTS.md`,
  - `CONTRIBUTING.md` (si présent),
  - `CHANGELOG.md`,
  - documentation utilisateur.
- Rédiger ou améliorer les sections expliquant :
  - le fonctionnement,
  - l’installation,
  - l’hébergement,
  - les contraintes CORS/RTSP,
  - les paramètres,
  - les cas d’usage.
- Produire une documentation cohérente et claire pour les humains.

## 🚫 Ne doit PAS faire
- Modifier le code source (`index.html`).
- Changer la logique, les constantes, les structures d’objet.
- Ajouter du CSS ou JS.

---

# 🔍 4. QA Agent (Quality Assurance)

## 🎯 Responsabilités
- Vérifier que :
  - le portail reste fonctionnel,
  - les modales sont bien responsives,
  - les caméras s’affichent correctement,
  - les flux snapshots se rafraîchissent,
  - les raccourcis se créent / modifient / suppriment sans bugs,
  - les paramètres sont persistants,
  - aucune régression visuelle n’est introduite.
- Tester les comportements sur plusieurs tailles d’écran.

## 🚫 Ne doit PAS faire
- Modifier fréquemment le code.
- Implémenter de nouvelles fonctionnalités.
- Changer des structures de données.

---

# 🔐 5. Security Agent

## 🎯 Responsabilités
- Identifier les risques potentiels :
  - exposition réseau,
  - flux non sécurisés,
  - URL sensibles,
  - utilisation de localStorage,
  - absence d’authentification.
- Proposer des améliorations de sécurité.
- Signaler les mauvaises pratiques potentielles.

## 🚫 Ne doit PAS faire
- Ajouter lui-même des mécanismes d’authentification complexes.
- Modifier les fichiers de production sans validation d’un autre agent.
- Introduire des dépendances ou appels réseau non justifiés.

---

# 🛠️ 6. Build & Optimization Agent (optionnel)

## 🎯 Responsabilités
- Optimiser le code existant :
  - réduire le CSS,
  - factoriser le JS,
  - rendre la page plus rapide,
  - limiter le nombre d’opérations DOM.
- Maintenir un fichier unique (`index.html`) performant.
- Préparer une version "minifiée" si nécessaire.

## 🚫 Ne doit PAS faire
- Modifier le comportement fonctionnel.
- Introduire des outils de build (webpack, vite, parcel…).
- Ajouter une architecture multi-fichiers (la page doit rester self-contained).

---

# 🤝 Règles de collaboration entre agents

## 🔷 1. Priorité fonctionnelle
- **Logic Agent** maîtrise la logique.
- **Frontend Agent** maîtrise l’apparence.
- Ils ne doivent pas se marcher dessus.

## 🔷 2. Le portail doit rester :
- en **1 seul fichier** `index.html`,
- **sans backend**,
- **sans dépendance externe**,
- compatible **NoVNC**,
- fonctionnel en local et sur navigateur moderne.

## 🔷 3. Tout doit rester stocké dans `localStorage` :
- raccourcis,
- paramètres,
- caméras,
- thème.

## 🔷 4. Les agents doivent respecter strictement :
- les structures existantes,
- les noms de variables,
- les modales déjà en place.

---

# 🧭 Vision globale du projet

Ce portail doit :

- Servir de **startpage homelab complète**.
- Être **autonome**, **légère**, **rapide**.
- Fonctionner **offline** (hors pings).
- Être adaptable (thèmes, catégories, caméras).
- Rester très simple à déployer : un seul fichier statique.

---

# 📌 Notes supplémentaires

- Aucun framework JS/CSS ne doit être ajouté.
- Aucun fichier externe ne doit être chargé (sauf snapshots caméras).
- Le code doit rester lisible, clair et simple à maintenir.
- L’objectif est un **portail évolutif**, mais **minimaliste** dans sa structure.

---

# 🎉 Fin du document

Copilot peut maintenant comprendre parfaitement ton projet et travailler avec toi de façon beaucoup plus intelligente et cohérente.
