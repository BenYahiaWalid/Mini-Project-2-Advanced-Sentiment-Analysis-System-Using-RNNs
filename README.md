# Mini-Project-2-Advanced-Sentiment-Analysis-System-Using-RNNs

##  Présentation du projet et objectifs

Ce projet présente une chaîne complète d’apprentissage profond basée sur un modèle de **réseaux de neurones récurrents (RNN)**, plus précisément des **Bidirectional LSTM**, pour une classification binaire des sentiments.  
L’objectif est de concevoir, évaluer et déployer un modèle performant tout en prenant en compte les aspects de **performance, durabilité environnementale, éthique et contraintes des systèmes embarqués**.

Le projet couvre :
- Le prétraitement des données et l’entraînement du modèle
- L’analyse des performances et du surapprentissage
- L’évaluation de l’empreinte carbone lors de l’entraînement
- Les considérations éthiques et l’explicabilité du modèle
- L’optimisation et le déploiement avec **TensorFlow Lite**

---

##  Téléchargement du jeu de données et prétraitement

### Téléchargement du jeu de données / Jeu de données inclus dans le projet

[Le jeu de données IMDb Large Movie Review Dataset peut être téléchargé directement ici](https://ai.stanford.edu/~amaas/data/sentiment/)

Ce répertoire contient :
- `pos/` : critiques de films avec sentiment positif
- `neg/` : critiques de films avec sentiment négatif

Chaque fichier texte correspond à une critique de film.  
Le sentiment est automatiquement déduit du dossier (`pos` ou `neg`) lors du chargement des données.

---

##  Entraînement et évaluation du modèle

### Étapes d’entraînement du modèle

Le projet utilise un **modèle Bidirectional LSTM** pour classer les critiques de films en sentiments **positif** ou **négatif**.  

Les étapes principales sont les suivantes :

1. **Chargement et prétraitement des données**  
   - Nettoyage du texte : suppression des balises HTML, des caractères spéciaux, mise en minuscules et suppression des mots vides (*stop words*).
   - Transformation des critiques en texte normalisé.

2. **Tokenization et vectorisation**  
   - Utilisation de **Keras Tokenizer** pour créer un vocabulaire.
   - Conversion des textes en **séquences d’entiers**.
   - Application d’un **padding** pour uniformiser la longueur des séquences (ex: 200).

3. **Séparation des ensembles**  
   - Division en **train** et **test** (80% / 20%).

4. **Entraînement du modèle BiLSTM**  
   - Architecture :
     - Embedding Layer  
     - Deux couches **Bidirectional LSTM**  
     - Dropout  
     - Dense (sigmoid)  
   - Utilisation de **EarlyStopping** pour éviter le surapprentissage.

5. **Évaluation du modèle**  
   - Mesures de performance : **accuracy et loss** (train/validation).  
   - Analyse des courbes d’apprentissage.  
   - Test du modèle sur de nouvelles critiques pour évaluer sa capacité de généralisation.

---

##  Analyse de l’empreinte carbone

Afin de mesurer l’impact environnemental de l’entraînement et de l’optimisation du modèle, nous avons utilisé **CodeCarbon**.

### Résultats pour l’entraînement du modèle

- Énergie totale consommée : **0.058314 kWh**  
- Énergie CPU : **0.057124 kWh**  
- Énergie RAM : **0.001190 kWh**  
- Émissions de CO₂ : **0.0001741 kg CO₂**  
- Plateforme : Windows 11  
- CPU : AMD Ryzen 7 9800X3D (16 threads)  
- GPU : Non utilisé  

Ces résultats montrent que l’entraînement d’un modèle **Bidirectional LSTM** est significativement plus coûteux qu’un modèle de régression logistique, notamment en raison de la complexité des calculs séquentiels.

### Résultats pour l’optimisation des hyperparamètres

- Augmentation de la consommation énergétique liée aux essais multiples  
- Amélioration progressive de l’accuracy et réduction de la loss  

Dans ce cas, l’optimisation des hyperparamètres introduit un **compromis entre performance et impact environnemental**.

---

##  Considérations éthiques et explicabilité

L’utilisation de modèles d’apprentissage profond pour la classification de textes implique des **aspects éthiques importants** :  
- **Biais des données** : les datasets peuvent contenir des biais culturels ou linguistiques reproduits par le modèle.  
- **Manque de transparence** : les modèles deep learning sont souvent considérés comme des boîtes noires.  
- **Impact sur les utilisateurs** : les décisions doivent être justifiables et compréhensibles.

### Explicabilité avec SHAP et LIME

Pour analyser les prédictions du modèle, nous avons utilisé **SHAP** et **LIME** :

- **SHAP** permet d’attribuer un score à chaque mot en fonction de son impact sur la prédiction.  
- **LIME** fournit une explication locale pour une prédiction donnée.  
- Ces méthodes permettent de **mieux comprendre le comportement du modèle et d’identifier d’éventuels biais**.

---

##  Déploiement sur système embarqué (TensorFlow Lite)

Pour exécuter le modèle sur des systèmes contraints (mobile ou embarqué), il est nécessaire de l’optimiser.

### Étapes du déploiement

1. **Conversion du modèle**  
   - Transformation du modèle Keras en format **TensorFlow Lite**.

2. **Optimisation / quantification**  
   - Réduction de la précision des poids pour diminuer la taille du modèle.

3. **Comparaison des performances**  
   - Taille du modèle  
   - Temps d’inférence  
   - Précision avant/après conversion  

4. **Inférence optimisée**  
   - Exécution rapide sur appareils mobiles ou embarqués  
   - Réduction de la consommation mémoire  

Cela permet d’obtenir un modèle **plus léger et plus rapide**, adapté aux environnements à ressources limitées.

---

##  Responsabilités liées à la publication du code

Le code source est publié afin de :
- Garantir la reproductibilité des résultats
- Favoriser la transparence
- Permettre la réutilisation à des fins académiques et éducatives

---

##  Licence open-source

Pour ce projet, une **licence open-source** a été choisie afin de clarifier les droits et obligations liés à l’utilisation du code.  

### Licence choisie : MIT

- La licence **MIT** est **courte, permissive et largement utilisée**.  
- Elle permet à n’importe qui de **copier, modifier, distribuer et utiliser le code**.  

### Implications de la licence

1. **Transparence et collaboration**  
   - Favorise le partage et les contributions.

2. **Protection légale**  
   - Limite la responsabilité de l’auteur.

3. **Compatibilité**  
   - Compatible avec de nombreux projets open-source.

### Comparaison des licenses

- **GPL** : impose le partage du code dérivé  
- **Apache 2.0** : inclut une gestion des brevets  
- **MIT** : simple et adaptée aux projets académiques  

---

##  Pratiques de publication et collaboration

### 1. Code privé / non publié
- Transparence limitée  
- Collaboration impossible  

### 2. Publication partielle
- Difficulté de reproduction  

### 3. Publication complète avec licence open-source
- Transparence maximale  
- Collaboration facilitée  

### 4. Publication avec documentation détaillée
- Reproductibilité excellente  
- Maintenance facilitée  

---

##  Protocole de signalement et correction des bugs

1. **Signaler un bug** :  
   - Créer une **issue** sur GitHub  
   - Décrire le problème et les étapes de reproduction  

2. **Corriger un bug** :  
   - Créer une **pull request**  
   - Expliquer les modifications  

3. **Validation** :  
   - Revue avant intégration dans la branche principale  

---
