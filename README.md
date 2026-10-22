# Prévision de la consommation électrique du lendemain

Projet final S7MOI1 « De la donnée à la décision » · ECAM-EPMI · Science des Données

## Problème et résultat

Un fournisseur d'électricité fictif doit acheter chaque jour (avant 10 h) l'énergie du lendemain. Une mauvaise prévision lui coûte de l'argent : rachat en urgence si on sous-estime, revente à perte si on surestime.

**Résultat sur le test (233 jours jamais vus, du 03/02/2010 au 25/11/2010)** :

| Méthode | MAE (kWh/jour) |
|---|---|
| Demain = aujourd'hui (situation actuelle) | 4,82 |
| Moyenne des 7 derniers jours | 4,18 |
| Random Forest (modèle retenu) | 4,19 |

Le modèle réduit l'erreur de 13,1 % par rapport à la méthode actuelle (objectif de départ : 20 %, non atteint), mais pas par rapport à la moyenne des 7 derniers jours. Sous nos hypothèses de prix, le gain estimé est de 127 600 € par an pour 10 000 foyers face à la méthode actuelle, mais il devient faible face à la moyenne 7 jours (voir le rapport, axe 7). Recommandation : pilote de 3 mois avant tout déploiement.

## Données

- Source : UCI Machine Learning Repository, *Individual Household Electric Power Consumption* (id 235) : https://archive.ics.uci.edu/dataset/235/individual+household+electric+power+consumption
- Date de consultation : 18/10/2026
- Licence : [à confirmer sur la page UCI et à recopier ici]
- Un seul foyer (Sceaux, France), une mesure par minute, décembre 2006 – novembre 2010.
- Le fichier brut (133 Mo) n'est pas dans le dépôt : le notebook 01 le télécharge automatiquement.

## Structure du dépôt

```
├── README.md
├── requirements.txt
├── data/
│   └── processed/            # fichiers produits par les notebooks (features_conso.csv, résultats...)
├── notebooks/
│   ├── 01_cadrage_eda.ipynb      # cadrage, qualité des données, analyse exploratoire
│   ├── 02_modelisation.ipynb     # baselines, modèles, validation croisée, test
│   └── 03_decision_roi.ipynb     # coûts, ROI, scénarios, risques
├── src/                      # fonctions réutilisables
└── reports/                  # rapport PDF, slides, figures
```

## Comment lancer

1. Installer les librairies : `pip install -r requirements.txt`
2. Exécuter les notebooks dans l'ordre (01, 02, 03) avec « Restart & Run All ». Tous les chemins sont relatifs et `random_state = 42`.
3. Sur Google Colab, importer `features_conso.csv` dans `data/processed/` quand le notebook 02 le demande.

## Usage de l'IA générative

[À compléter avec la vérité de l'équipe : outil utilisé, pour quoi, par qui.]
Exemple : « Claude (Anthropic) a été utilisé comme assistant pour la relecture du code, la vérification des chiffres et la rédaction du rapport. Chaque membre peut expliquer le code de sa partie. »

## Équipe

- Membre 1 : business et décision (axes 1, 6, 7)
- Membre 2 : données et préparation (axes 2, 3)
- Membre 3 : modélisation et évaluation (axes 4, 5)
