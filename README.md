# 🕵️ Undercover — Application Web PWA

Jeu de déduction sociale jouable **en local** (sur un seul appareil) et **en ligne** (chaque joueur sur son propre téléphone), avec un mode hors-ligne grâce au Service Worker.

## 🚀 Déploiement sur GitHub Pages (5 minutes)

### 1. Créer le dépôt GitHub

```bash
git init
git add .
git commit -m "🕵️ Initial Undercover game"
git branch -M main
git remote add origin https://github.com/TON_USERNAME/undercover.git
git push -u origin main
```

### 2. Activer GitHub Pages

1. Aller dans **Settings → Pages**
2. Source : **Deploy from a branch**
3. Branch : `main`, dossier : `/ (root)`
4. Sauvegarder → l'URL sera `https://TON_USERNAME.github.io/undercover/`

### 3. Configurer Firebase (pour le mode Online)

Le mode Online nécessite Firebase Realtime Database **gratuit** :

1. Aller sur [console.firebase.google.com](https://console.firebase.google.com)
2. Créer un projet (ex: `undercover-game`)
3. Activer **Realtime Database** → Choisir région Europe → Mode **Test** (lecture/écriture publique pendant 30 jours)
4. Copier l'URL de la base (ex: `https://undercover-game-default-rtdb.europe-west1.firebasedatabase.app`)
5. Dans `index.html`, remplacer la ligne :
   ```js
   const FB_URL = 'VOTRE_URL_FIREBASE_ICI';
   ```
   par votre URL Firebase.

### 4. Règles Firebase (pour la production)

Dans Firebase Console → Realtime Database → Règles :

```json
{
  "rules": {
    "rooms": {
      "$roomCode": {
        ".read": true,
        ".write": true,
        ".indexOn": ["_v"]
      }
    }
  }
}
```

### 5. Nettoyage automatique

Les salles expirent après 2h automatiquement (géré par le client hôte).

## 🎮 Fonctionnalités

- ✅ **Mode Local** — Tous sur un seul téléphone, distribution des cartes par glissement
- ✅ **Mode Online** — Chaque joueur sur son appareil, synchronisation temps réel
- ✅ **PWA Installable** — Bouton "Ajouter à l'écran d'accueil"
- ✅ **5 thèmes** — Dark, Light, Retro, Forest, Rose
- ✅ **Historique & Palmarès** — Persistants via localStorage
- ✅ **Minuterie de discussion** — Compte à rebours visuel
- ✅ **Lien de partage** — Copier le lien avec code de salle intégré

## 📁 Structure

```
undercover/
├── index.html      ← Jeu complet (tout-en-un)
├── manifest.json   ← PWA manifest
├── sw.js           ← Service Worker (offline)
├── icon-192.png    ← Icône PWA (à créer)
├── icon-512.png    ← Icône PWA (à créer)
└── README.md       ← Ce fichier
```

## 🎨 Icônes PWA

Pour créer les icônes, utiliser un emoji 🕵️ sur fond #7c5cfc :
- [favicon.io](https://favicon.io/emoji-favicons/detective/) → télécharger et renommer en `icon-192.png` et `icon-512.png`

