# 🩺 Projet de Classification de Radiographies Pulmonaires
COVID-19, Pneumonie Virale et Cas Normaux

---

## 📌 Résumé du Projet
Ce projet de deep learning médical compare quatre architectures de réseaux de neurones pour classer automatiquement des radiographies pulmonaires en trois catégories : COVID-19, Pneumonie Virale et Normal. L'objectif est de fournir un outil d'aide au diagnostic rapide et précis, particulièrement utile dans des contextes de ressources limitées ou en soutien aux radiologues.

**Performance globale :**  
Le modèle ResNet50 atteint une précision de **98,29 %** sur l'ensemble de test, démontrant une forte capacité de généralisation.

---

## 🏗️ Modèles Comparés et Performances

| Modèle | Accuracy (Test) | Précision (macro) | Rappel (macro) | F1‑Score (macro) |
|--------|----------------|------------------|----------------|----------------|
| ResNet50 (Transfer Learning) | 98,29 % | 98,19 % | 97,25 % | 97,71 % |
| VGG16 (Transfer Learning) | 96,84 % | 97,00 % | 96,00 % | 96,00 % |
| DenseNet121 (Transfer Learning) | 92,55 % | 92,00 % | 91,00 % | 91,00 % |
| CNN Personnalisé (5 couches) | 91,69 % | 90,00 % | 91,00 % | 90,00 % |

**Conclusion :**  
Les modèles par transfert learning (ResNet50, VGG16) surpassent nettement l’architecture CNN classique, avec **ResNet50 offrant les meilleures performances globales**.

---

## 📊 Jeu de Données

**Répartition des images :**

| Classe | Entraînement | Validation | Test | Total |
|--------|--------------|------------|------|-------|
| COVID-19 | 3 301 | 1 195 | 362 | 4 858 |
| Normal | 7 134 | 2 038 | 1 020 | 10 192 |
| Pneumonie Virale | 941 | 269 | 135 | 1 345 |
| **Total** | 11 376 | 3 502 | 1 517 | 16 395 |

**Remarque :** Les classes sont déséquilibrées (beaucoup plus d’images « Normal »). Des poids de classe sont appliqués pendant l’entraînement pour compenser ce déséquilibre.

---

## ⚙️ Méthodologie Expérimentale

### 1. Prétraitement et augmentation des données
- **Redimensionnement :** 200×200 ou 224×224 px selon le modèle  
- **Normalisation des pixels** : valeurs entre 0 et 1  
- **Augmentation (uniquement sur l’ensemble d’entraînement)** :
  - Rotation (±15°)  
  - Translation horizontale/verticale (±10 %)  
  - Zoom (±10 %)  
  - Retournement horizontal  
  - Cisaillement (±10 %)

### 2. Architectures
- **Transfer Learning :** modèles pré‑entraînés sur ImageNet (VGG16, DenseNet121, ResNet50), fine‑tuning des dernières couches  
- **CNN personnalisé :** architecture légère à 5 blocs convolutionnels, normalisation par batch et dropout

### 3. Entraînement
- **Optimiseur :** Adam (learning rate = 1e‑4)  
- **Fonction de perte :** Entropie croisée catégorielle  
- **Callbacks :** Early Stopping (patience = 5), réduction du learning rate sur plateau, sauvegarde du meilleur modèle

### 4. Évaluation
- **Métriques :** Accuracy, Précision, Rappel, F1‑Score, AUC  
- Matrice de confusion et rapport de classification détaillé  
- Visualisation des courbes d’apprentissage

---

## 🔍 Analyse des Résultats (Modèle ResNet50)

**Performances par classe (test) :**

| Classe | Précision | Rappel | F1‑Score | Support |
|--------|-----------|--------|----------|---------|
| COVID-19 | 98,6 % | 96,1 % | 97,3 % | 362 |
| Normal | 98,3 % | 99,3 % | 98,8 % | 1 020 |
| Pneumonie Virale | 97,7 % | 96,3 % | 97,0 % | 135 |
| **Macro Avg** | 98,2 % | 97,2 % | 97,7 % | 1 517 |

**Analyse des erreurs :** 26 erreurs sur 1 517 images  
- COVID-19 → Normal : 14 erreurs (53,8 %)  
- Normal → COVID-19 : 4 erreurs  
- Normal → Pneumonie Virale : 3 erreurs  
- Pneumonie Virale → Normal : 4 erreurs  
- Pneumonie Virale → COVID-19 : 1 erreur  

**Interprétation :** La confusion la plus fréquente est entre COVID-19 et Normal.

---

## 🎯 Points Forts du Projet
- Comparaison systématique de 4 architectures  
- Gestion du déséquilibre via les poids de classes  
- Augmentation de données pour améliorer la généralisation  
- Optimisation avancée avec callbacks adaptatifs  
- Visualisations complètes (matrices de confusion, courbes d’apprentissage)  
- Sauvegarde des modèles et résultats pour reproductibilité

---

## ⚠️ Limitations et Perspectives

### Limitations actuelles
- Déséquilibre des classes  
- Taille d’image réduite pour raisons computationnelles  
- Absence de validation croisée  
- Manque d’interprétabilité (pas de Grad-CAM)

### Améliorations envisageables
- Collecte de données supplémentaires  
- Augmentation plus poussée (mixup, cutmix, style transfer)  
- Ensemble de modèles  
- Explicabilité : visualisation des régions d’intérêt  
- Déploiement sous forme d’API ou interface web

---

## 🚀 Utilisation Pratique
1. Charger le modèle ResNet50 pré‑entraîné  
2. Prétraiter une nouvelle radiographie (redimensionnement, normalisation)  
3. Effectuer la prédiction et obtenir la classe et un score de confiance  

**Note :** Ce modèle est une aide au diagnostic et **ne remplace pas l’expertise d’un médecin**.

---

## ✅ Conclusion
Le modèle ResNet50 atteint une performance exceptionnelle (**98,29 % d’accuracy**) sur la classification triple, surpassant les autres architectures.  
Le projet démontre l’efficacité du transfer learning dans le domaine médical et propose une base solide pour un outil clinique d’aide au triage rapide.
