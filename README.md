# Homelab Portal – Startpage HTML pour services auto-hébergés

Portail HTML **100% statique** pour centraliser l’accès à ton homelab : Proxmox, Docker, Zoraxy, Transmission, Home Assistant, Frigate, IA locale, etc.

- Interface sombre, ambiance **geek / cyber** 🧬  
- Gestion des raccourcis **directement dans le navigateur** (localStorage)  
- Bandeau de **caméras** en haut + vue détaillée en surimpression  
- Indicateurs d’état (UP / DOWN) des services  
- Onglets par **thème** (Serveurs, IA, Médias, Caméras, Domotique, etc.)  

---

## 🇫🇷 Version française

### ✨ Fonctionnalités principales

- **Page unique `index.html`** : aucun backend, aucun framework, juste HTML/CSS/JS vanilla.
- **Raccourcis dynamiques** :
  - Ajout / modification / suppression via le bouton `+` (en bas à droite).
  - Édition rapide via l’icône ✏️ sur chaque carte au survol.
  - Sauvegarde automatique dans le `localStorage` du navigateur.
- **Onglets thématiques** :
  - Tous, Serveurs, IA, Médias, Caméras, Domotique, Réseau, Custom.
  - Filtre en temps réel + barre de recherche.
- **Bandeau de caméras** (4 emplacements) :
  - Affichage de snapshots HTTP (via NVR / Frigate / Home Assistant…).
  - Clic sur une caméra → ouverture d’une **modale** avec :
    - rafraîchissement périodique de l’image (pseudo-stream),
    - bouton “Ouvrir dans un nouvel onglet” vers la page NVR / Frigate,
    - fermeture via bouton, clic en dehors ou touche `Échap`.
- **Indicateur d’état des services** :
  - Petit point en bas à droite de chaque tuile :
    - 🟢 vert : UP (réponse HTTP OK / no-cors),
    - 🔴 rouge : DOWN (erreur / timeout),
    - ⚪ gris : inconnu.
  - Vérification périodique via `fetch` (mode `no-cors`).
- **Personnalisation du portail** via l’icône ⚙ :
  - Titre du portail.
  - Sous-titre.
  - Texte du logo ou **logo image** (PNG/JPG/WebP/SVG, ~256 Ko max).
  - Thème visuel : `dark`, `neon`, `minimal`.
  - Configuration des 4 caméras :
    - nom,
    - URL de snapshot / flux HTTP,
    - URL clic (page NVR / Frigate / HA).

---

### 🧩 Structure du projet

- `index.html`  
  Contient **toute la logique** :
  - styles (`<style>`),
  - comportement JS (`<script>`),
  - gestion du `localStorage`,
  - modales, onglets, raccourcis, caméras, pings de services.

Aucun autre fichier n’est requis.  
Tu peux l’héberger :

- sur un simple **serveur web statique** (Nginx, Caddy, Apache, …),
- directement servi par **Docker** / un conteneur minimal,
- ou même ouvert en fichier local dans ton navigateur (idéalement via HTTP pour éviter certains blocages CORS).
