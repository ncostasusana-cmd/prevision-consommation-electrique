# Prévision de la consommation électrique du lendemain

Projet final S7MOI1 « De la donnée à la décision » · ECAM-EPMI · Science des Données

## Problème et résultat

Un fournisseur d'électricité fictif achète chaque jour (avant 10 h) l'énergie du lendemain. Une mauvaise prévision lui coûte de l'argent : rachat en urgence si on sous-estime, revente à perte si on surestime.

**Résultat sur le test (233 jours jamais vus, du 03/02/2010 au 25/11/2010)**

| Méthode | Erreur moyenne MAE (kWh/jour) |
|---|---|
| Demain = aujourd'hui (situation actuelle) | 4,82 |
| Moyenne des 7 derniers jours | 4,18 |
| Random Forest (modèle retenu) | 4,19 |

Le modèle réduit l'erreur de **13,1 %** par rapport à la méthode actuelle (objectif de départ : 20 %, non atteint), mais pas par rapport à la moyenne des 7 derniers jours.

Sous nos hypothèses de prix, le gain estimé est de **127 600 € par an** pour 10 000 foyers face à la méthode actuelle (ROI de 155 % la première année). Face à la moyenne des 7 jours, le gain tombe à environ 21 600 € par an (ROI négatif). **Recommandation : un pilote de 3 mois avant tout déploiement.**

## Données

- **Source** : Hebrail, G. et Berard, A. (2012), *Individual Household Electric Power Consumption*, UCI Machine Learning Repository (id 235) : https://archive.ics.uci.edu/dataset/235/individual+household+electric+power+consumption
- **Licence** : Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Date de consultation** : 18/10/2026
- Un seul foyer (Sceaux, France), une mesure par minute, de décembre 2006 à novembre 2010.
- Le fichier brut (environ 130 Mo) n'est pas dans le dépôt : le notebook 01 le télécharge automatiquement.

## Contenu du dépôt

```
README.md
requirements.txt
01_cadrage_eda.ipynb      cadrage, qualité des données, analyse exploratoire
02_modelisation.ipynb     baselines, modèles, validation croisée, test
03_decision_roi.ipynb     coûts, ROI, scénarios
data/processed/           features_conso.csv, resultats_test.csv,
                          metriques_test.csv, comparaison_cv.csv
reports/                  rapport PDF et support de présentation
```

## Comment lancer

1. Installer les librairies : `pip install -r requirements.txt`
2. Depuis la racine du dépôt, exécuter les notebooks dans l'ordre (01, 02, 03) avec « Restart & Run All ». Les chemins sont relatifs et `random_state = 42`.
3. Sur Google Colab, une nouvelle session oublie les fichiers : les notebooks 02 et 03 demandent alors d'importer les fichiers de `data/processed/`.

## Usage de l'IA générative

Claude (Anthropic) a été utilisé comme assistant : relecture et vérification du code, contrôle des chiffres et aide à la rédaction du rapport et du support. Chaque membre de l'équipe peut expliquer le code de sa partie.

## Équipe

- Membre 1 : business et décision (axes 1, 6, 7) - Eurydice SEMASSOU
- Membre 2 : données et préparation (axes 2, 3) - Sabirath SOUMASSOU
- Membre 3 : modélisation et évaluation (axes 4, 5) - Susana NOGUEIRA COSTA
