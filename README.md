# KKC Payment Redirect - Pages de redirection Wave

Ce dossier contient les pages de redirection pour les paiements Wave de l'application KKC.

## 🚀 Déploiement sur Vercel

### 1. Structure des fichiers
```
kkc-payment-redirect/
├── public/
│   ├── paiement-reussi/
│   │   └── [id].html          # Page de succès
│   ├── paiement-echoue/
│   │   └── [id].html          # Page d'échec
│   └── _redirects             # Redirections Vercel
├── vercel.json                # Configuration Vercel
└── README.md                  # Ce fichier
```

### 2. Configuration Vercel
Le fichier `vercel.json` configure :
- **Routes dynamiques** pour gérer les IDs de réservation
- **Headers de sécurité** pour protéger les pages
- **Redirections** automatiques vers l'app mobile

### 3. Déploiement
1. Connectez ce dossier à votre projet Vercel
2. Déployez automatiquement
3. Les URLs seront :
   - Succès : `https://votre-domaine.vercel.app/paiement-reussi/{id}`
   - Échec : `https://votre-domaine.vercel.app/paiement-echoue/{id}`

## 📱 Deep Links

### Schéma d'app
- **Succès** : `myapp://paiement-reussi/{id}`
- **Échec** : `myapp://paiement-echoue/{id}`

### Configuration dans l'app
Assurez-vous que votre app Expo gère ces deep links dans `app.json` :

```json
{
  "expo": {
    "scheme": "myapp",
    "android": {
      "intentFilters": [
        {
          "action": "VIEW",
          "data": [
            {
              "scheme": "myapp",
              "host": "paiement-reussi"
            },
            {
              "scheme": "myapp",
              "host": "paiement-echoue"
            }
          ],
          "category": ["BROWSABLE", "DEFAULT"]
        }
      ]
    }
  }
}
```

## 🎨 Fonctionnalités

### Page de succès
- ✅ Design moderne avec animations
- ✅ Compte à rebours automatique (3 secondes)
- ✅ Redirection automatique vers l'app
- ✅ Bouton manuel de redirection
- ✅ Responsive design

### Page d'échec
- ❌ Design d'erreur avec animations
- ⏰ Compte à rebours (5 secondes)
- 📱 Redirection vers l'app
- 🔄 Bouton de retour manuel

## 🔧 URLs Wave

Dans votre fonction `create-payment`, utilisez :

```typescript
const payload = {
  success_url: `https://votre-domaine.vercel.app/paiement-reussi/${booking_id}`,
  error_url: `https://votre-domaine.vercel.app/paiement-echoue/${booking_id}`,
  // ... autres paramètres
};
```

## 🚨 Résolution des problèmes

### Erreur 404
Si vous avez encore des erreurs 404 :
1. Vérifiez que `vercel.json` est bien déployé
2. Redéployez le projet complet
3. Vérifiez les logs Vercel

### Deep links ne fonctionnent pas
1. Vérifiez la configuration `app.json`
2. Testez avec un deep link manuel
3. Vérifiez que l'app est installée

## 📞 Support

Pour toute question ou problème, vérifiez :
1. Les logs Vercel
2. La configuration des deep links
3. Les URLs dans votre fonction Wave
