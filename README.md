# Data Quality & Anomaly Detection auf Luxury Cosmetics Datensatz

Projekt im Rahmen des Moduls **Big Data Management** (B.Sc. Informatik, TU Clausthal)
Betreuung: M.Sc. Denis Kruschinski

## Projektbeschreibung

Dieses Projekt untersucht Datenqualität und Anomalien im Datensatz *"Luxury Cosmetics Fraud
Analysis 2025"* (Kaggle). Ziel ist es, mithilfe von Datenprofiling, gezielten Quality-Checks
und einem Isolation-Forest-Modell  Betrugmuster zu identifizieren und diese
gegen die tatsächlich vorhandenen Fraud-Labels zu bewerten.

## Datensatz

- **Quelle:** [Luxury Cosmetics Fraud Analysis 2025 :Kaggle](https://www.kaggle.com/)
- **Umfang:** 2.133 Transaktionen, 16 Merkmale
- **Zielvariable:** `Fraud_Flag` (binär) — 66 Fraud-Fälle: das sind 3,09 % des Datensatzes vs. 2.067 reguläre
  Transaktionen 96,91 %

## Vorgehen

Das Projekt gliedert sich in drei Abschnitte, die im Notebook [`analyse.ipynb`](./analyse.ipynb)
umgesetzt sind:

1. **Datenprofiling** — Struktur, Vollständigkeit und Verteilung der Merkmale
2. **Quality-Check** - Implementierung von vier automatisierte Quality-Testen
3. **Anomalieerkennung mit Isolation Forest** — Feature Engineering (One-Hot-Encoding von
   5 kategorischen Merkmalen → 49-dimensionaler Feature-Vektor), Training, Vergleich der
   erkannten Anomalien mit den echten Fraud-Labels

## Ergebnisse

| Metrik | Wert |
|---|---|
| Accuracy | 0,94 |
| Precision/Recall/F1 ("Kein Fraud") | 0,97 |
| Precision/Recall/F1 ("Fraud") | 0,06 |
| ROC-AUC | 0,467 |

Die vorhandenen Merkmale korrelieren kaum mit `Fraud_Flag`; Isolation Forest erzielt hier
keine bessere Trennschärfe als eine Zufallsentscheidung (ROC-AUC < 0,5). Als
Handlungsempfehlung wird vorgeschlagen, zusätzliche verhaltensbasierte Merkmale einzubeziehen, um die Erkennungsleistung
zu verbessern.

## Repository-Struktur

```
├── analyse.ipynb                  # Vollständiges Analyse-Notebook
├── data/
│   └── luxury_cosmetics_fraud_analysis_2025.csv
├── figures/                       # Generierte Diagramme
│   ├── 1_fehlende_werte.png
│   ├── 2_fraud_verteilung.png
│   ├── 3_boxplots_merkmale.png
│   ├── 4_konfusionsmatrix.png
│   ├── 5_roc_auc_vergleich.png
│   ├── 6_precision_recall_f1_final.png
│   ├── score_verteilung_original.png
│   └── isolation_forest_streudiagramm.png
├── vorbericht.pdf                 
└── README.md
```

## Verwendete Methoden & Referenzen

- **Datenprofiling & Quality-Checks:** Ehrlinger, L. & Wöß, W. (2022). *A Survey of Data
  Quality Measurement and Monitoring Tools.* Frontiers in Big Data, 5:850611.
  https://doi.org/10.3389/fdata.2022.850611
- **Isolation Forest:** Liu, F. T., Ting, K. M. & Zhou, Z.-H. (2008). *Isolation Forest.*
  2008 Eighth IEEE ICDM, pp. 413–422. https://doi.org/10.1109/ICDM.2008.17

## Setup & Ausführung

```bash
pip install pandas numpy scikit-learn matplotlib seaborn
jupyter notebook analyse.ipynb
```

## Autor

Ramane Gbatkom Mouliom Abdel, B.Sc. Informatik, TU Clausthal

## Status

- [x] Datenprofiling
- [x] Quality-Check
- [x] Isolation-Forest-Anomalieerkennung
- [x] Präsentation 
- [ ] Schriftliche Ausarbeitung 
