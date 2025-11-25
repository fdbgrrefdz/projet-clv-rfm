# Data Exploration 

### Cette partie du projet consiste à analyser et explorer le dataset Online Retail II afin de comprendre sa structure, vérifier la qualité des données et produire les premiers indicateurs utiles pour la suite (modélisation, segmentation, application Streamlit).

Le notebook utilisé est : 02_data_exploration.ipynb.

Il contient :
- Chargement des données brutes et intégration du nettoyage du Membre 2.
- Analyse descriptive (dimensions, types, valeurs manquantes, incohérences).
- Visualisations principales : évolution des ventes, distributions prix/quantités, analyse par pays.

# rfm clv formulee

Cette étape consiste à construire la table RFM complète, segmenter les clients selon leur comportement d’achat et estimer la Customer Lifetime Value (CLV) via une formule fermée. Le notebook utilise les données nettoyées fournies par le Membre 2.

### Contenu du travail

- **Préparation des données** : transactions sans doublons, retours exclus, montants corrigés.
- **Calcul RFM** :
  - Recency (jours depuis la dernière commande),
  - Frequency (nombre de factures distinctes),
  - Monetary (total dépensé par client).
- **Scores RFM** : attribution de scores 1–5 (quintiles) puis création du score combiné `RFM_Score = R*100 + F*10 + M`.
- **Segmentation marketing** : identification de segments opérationnels (Champions, Loyal, At-risk, Promising, Others).
- **Mesures clés** :
  - ARPU (revenu moyen par client actif),
  - r (taux de rétention mensuel).
- **CLV via formule fermée** :  
  `CLV = ARPU × r / (1 + d − r)`  
  avec un taux d’actualisation d = 1%.
  Résultats produits : CLV globale et CLV par segment RFM.
- **Export final** : fichier `clean_data/customers_rfm.xlsx` contenant RFM, scores, segments, ARPU et CLV pour exploitation dans l’application Streamlit.


# Customer Lifetime Value (CLV) Analysis – Empirical CLV

### Purpose
This part of the project calculates **customer-level** and **cohort-level Customer Lifetime Value (CLV)** from transaction data.
It also generates visualizations to understand customer value trends and distribution over time.

### Notebook
`notebooks/clv_empirical.ipynb`

### Tasks
* **Data Preparation**
  * Clean transactions and calculate transaction amount:
    Amount = Quantity × UnitPrice

* **Customer-level CLV**
  * Aggregate total spending per customer
  * Export results as `clv_customer.csv`

* **Cohort-level CLV**
  * Determine first purchase month (`AcqMonth`) per customer
  * Calculate cohort age (`CohortAge`) in months
  * Compute average CLV per cohort
  * Export results as `clv_cohort.csv`

* **Visualizations**
  * Cohort CLV heatmap (`clv_cohort_heatmap.png`)
  * Cumulative revenue per cohort (`clv_cumulative_trend.png`)
  * Customer-level CLV distributions (linear and log scale)
  * Count of zero CLV customers

### Outputs
All outputs are saved in `output_clv/`:
* `clv_customer.csv` – customer-level CLV
* `clv_cohort.csv` – cohort-level CLV
* PNG visualizations:
  * `clv_cohort_heatmap.png`
  * `clv_cumulative_trend.png`
  * `clv_customer_distribution_linear.png`
  * `clv_customer_distribution_log.png`

### Usage
1. Install dependencies:
pip install pandas numpy matplotlib seaborn pyarrow
2. Place cleaned transaction file in `clean_data/`:
clean_data/transactions_customers.parquet
3. Open and run the notebook:
jupyter notebook notebooks/clv_empirical.ipynb
4. Check the `output_clv/` folder for CSV files and charts.



