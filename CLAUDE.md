# CLAUDE.md - Guide de développement

Guide pour Claude Code et les contributeurs du projet **Homelab Control Hub**.

---

## Conventions de code

### Nommage
- **camelCase** pour toutes les variables et fonctions JavaScript
- **SCREAMING_SNAKE_CASE** pour les constantes globales (ex: `CONFIG`, `STORAGE_KEYS`)
- **kebab-case** pour les IDs et classes CSS

### Style JavaScript
- Fonctions fléchées pour les callbacks courts
- `const` par défaut, `let` si réassignation nécessaire
- Pas de `var`
- Optional chaining (`?.`) et nullish coalescing (`??`) autorisés

### Style CSS
- Variables CSS dans `:root`
- Sections clairement identifiées par commentaires
- Mobile-first avec media queries ascendantes

---

## Architecture du projet

```
Homelab-Control-Hub/
├── index.html          # Application complète (HTML + CSS + JS)
├── README.md           # Documentation utilisateur (FR/EN)
├── CLAUDE.md           # Ce fichier - guide de développement
├── AGENTS.md           # Rôles des agents IA (Copilot)
├── REVIEW.md           # Axes d'amélioration identifiés
└── LICENSE             # MIT
```

### Structure du fichier index.html

| Section | Lignes | Description |
|---------|--------|-------------|
| CSS Variables & Themes | 1-62 | Couleurs, rayons, ombres, z-index |
| Reset & Base | 64-108 | Reset box-sizing, focus visible, skip link |
| Layout Principal | 110-144 | App shell, matrix background |
| Header | 146-251 | Logo, titre, horloge |
| Recherche | 253-321 | Barre de recherche, tips |
| Caméras | 323-430 | Bandeau et modal caméra |
| Onglets | 432-474 | Navigation par catégories |
| Panel & Tiles | 476-701 | Grille de raccourcis, status dots |
| Footer | 703-717 | Informations |
| FAB | 719-776 | Boutons flottants (+, settings) |
| Modales | 778-855 | Styles des modales |
| Auth Overlay | 857-920 | Écran de connexion |
| Formulaires | 922-1042 | Inputs, selects, buttons |
| Boutons | 1044-1116 | Styles des boutons |
| Status & Feedback | 1118-1141 | Messages d'état |
| Responsive | 1143-1232 | Media queries |

### Structure JavaScript

| Section | Description |
|---------|-------------|
| 1. CONFIG | Constantes de configuration |
| 2. STATE | État global de l'application |
| 3. UTILITAIRES | Helpers ($, $$, storage, cookies) |
| 4. CRYPTO | SHA-256 (WebCrypto + fallback) |
| 5. MODALES | modalManager avec focus trap |
| 6. DONNÉES | Load/save localStorage |
| 7. AUTH | Gestion de session |
| 8. THÈME & UI | Application des paramètres |
| 9. TABS | Navigation par onglets |
| 10. TILES | Rendu des raccourcis |
| 11-12. MODALS | Raccourcis et paramètres |
| 13. CAMÉRAS | Rendu et rafraîchissement |
| 14. HEALTH CHECKS | Ping des services |
| 15. RECHERCHE | Filtrage avec debounce |
| 16. PASSWORD TOGGLE | Affichage mot de passe |
| 17. INIT | DOMContentLoaded |

---

## Contraintes techniques

### Obligatoires
- **Fichier unique** : tout dans `index.html`
- **Zéro dépendance** : pas de framework, pas de CDN
- **Zéro backend** : 100% client-side
- **localStorage** : persistance des données
- **Compatible file://**: doit fonctionner en page de démarrage

### Limites connues
- localStorage limité à ~5-10 Mo
- Images encodées en base64 (max 100 Ko recommandé)
- Health checks en mode CORS peuvent donner des faux positifs
- Pas de support RTSP natif (HTTP snapshots uniquement)

---

## Clés localStorage

| Clé | Version | Contenu |
|-----|---------|---------|
| `homelab-links-v3` | v3 | Raccourcis/services |
| `homelab-title-v2` | v2 | Paramètres du portail |
| `homelab-active-tab-v1` | v1 | Onglet actif |
| `homelab-auth-v1` | v1 | Identifiants (hash SHA-256) |

---

## Thèmes disponibles

| Theme | Accent | Description |
|-------|--------|-------------|
| `dark` | #38bdf8 (bleu) | Classique sombre |
| `neon` | #a855f7 (violet) | Cyber/Matrix |
| `minimal` | #22c55e (vert) | Clean |

---

## Changelog récent

### v2.0 (2026-01-12)
**Consolidation majeure du code**

#### Accessibilité
- Focus trap sur toutes les modales
- Skip link pour navigation clavier
- Navigation clavier dans les onglets (flèches)
- Attributs ARIA complets (role, aria-modal, aria-labelledby)
- Restauration du focus après fermeture modale

#### Refactoring JavaScript
- État global centralisé (`state`)
- `modalManager` pour gestion unifiée des modales
- Constantes regroupées (`CONFIG`, `STORAGE_KEYS`)
- Utilitaires factorisés (`$`, `$$`, `storage`, `cookies`)
- Debounce sur la recherche

#### CSS
- Variables regroupées par catégorie
- 17 sections clairement commentées
- Classe `.sr-only` pour lecteurs d'écran

#### Corrections
- Réduction de ~3078 à ~2987 lignes
- Code plus maintenable et lisible

---

## Axes d'amélioration futurs

### Priorité haute
- [ ] Endpoint healthcheck dédié (éviter faux positifs CORS)
- [ ] Migration IndexedDB pour les images (éviter saturation localStorage)

### Priorité moyenne
- [ ] Export/import de configuration (JSON)
- [ ] Drag & drop pour réorganiser les tiles
- [ ] Mode édition groupée des raccourcis

### Priorité basse
- [ ] Version minifiée optionnelle
- [ ] PWA avec service worker (mode offline complet)
- [ ] Intégration Home Assistant (API)

---

## Commandes utiles

```bash
# Ouvrir directement dans le navigateur
xdg-open index.html          # Linux
open index.html              # macOS
start index.html             # Windows

# Serveur local simple (optionnel)
python3 -m http.server 8080
npx serve .
```

---

## Tests manuels recommandés

1. **Authentification** : login admin/admin, changement de mot de passe
2. **Raccourcis** : CRUD complet, changement d'onglet
3. **Recherche** : filtrage temps réel
4. **Thèmes** : basculer entre dark/neon/minimal
5. **Caméras** : placeholder si pas configuré, modal plein écran
6. **Responsive** : tester sur mobile (< 480px)
7. **Clavier** : navigation Tab, Escape pour fermer
8. **localStorage** : vider et recharger (valeurs par défaut)

---

## Liens

- [Repository GitHub](https://github.com/enamaryn/Homelab-Control-Hub)
- [Issues](https://github.com/enamaryn/Homelab-Control-Hub/issues)
