# 📊 Analyse de l'Âge et des Conditions de Départ à la Retraite (Power BI)

## 🎯 Aperçu du Projet
Ce projet propose une exploration analytique des conditions de fin de carrière en France (2013-2020). L'objectif est de visualiser l'évolution de l'âge de départ, l'impact sur la santé et les périodes de transition entre l'emploi et la retraite, segmentées par **Catégories Socio-Professionnelles (CSP)**.

**Points clés analysés :**
* 📈 **Évolution de l'âge :** Suivi de l'âge conjoncturel moyen par CSP.
* 🏥 **Santé & Pénibilité :** Corrélation entre CSP et limitations de santé dès la première année de retraite.
* ⚠️ **Transition :** Analyse de la durée moyenne sans emploi ni retraite (période de précarité potentielle).


## 📂 Structure des Données
Le projet exploite le dataset `departretraite_parcsp.csv` qui regroupe les indicateurs suivants :

| Colonne | Description |
| :--- | :--- |
| **annee** | Année d'observation. |
| **categorie_socioprofessionnelle** | Segment professionnel (Artisans, Cadres, Ouvriers, etc.). |
| **age_conjoncturel_de_depart** | Âge moyen de liquidation des droits. |
| **proportion_de_personnes_fortement_limitees** | % de retraités déclarant de lourds problèmes de santé. |
| **duree_moyenne_en_emploi_hors_cumul** | Temps passé en activité réelle avant le départ. |
| **duree_moyenne_sans_emploi_ni_retraite** | Temps d'inactivité avant la liquidation des droits. |

## 🧠 Intelligence Analytique (DAX)
J'ai conçu des mesures spécifiques pour transformer les données brutes en indicateurs stratégiques :

### 1. Score de Pénibilité (Taux d'Invalidité Global)
Cette mesure combine les limitations fortes et modérées pour évaluer la santé réelle par CSP.
```dax
Taux Invalidité Global = 
SUM('departretraite_parcsp'[proportion_de_personnes_fortement_limitees_au_cours_de_la_premiere_annee_de_retraite]) + 
SUM('departretraite_parcsp'[proportion_de_personnes_limitees_mais_pas_fortement_au_cours_de_la_premiere_annee_de_retraite])

2. Benchmark (Écart vs Moyenne Nationale)
Permet de situer chaque CSP par rapport à la moyenne du pays.
Ecart vs Moyenne = 
VAR MoyenneGlobale = CALCULATE(AVERAGE('departretraite_parcsp'[age_conjoncturel_de_depart_a_la_retraite]), ALL('departretraite_parcsp'))
RETURN
AVERAGE('departretraite_parcsp'[age_conjoncturel_de_depart_a_la_retraite]) - MoyenneGlobale

🛠️ Méthodologie ETL & Modélisation
Power Query : Nettoyage des données, gestion des formats numériques et suppression des agrégats système pour éviter les doublons.

Insights Métier : Mise en évidence du "sas de précarité" (inactivité avant retraite) qui touche davantage les ouvriers et employés.

DataViz : Utilisation de graphiques de tendances et de corrélation pour faciliter la lecture des données complexes.

🚀 Utilisation
Accès aux données : Le fichier departretraite_parcsp.csv est disponible à la racine du dépôt.

Consultation : Les résultats et analyses sont documentés via les captures d'écran et les mesures DAX détaillées ci-dessus.

👤 Contact
Sébastien Henique 📧 heniquea38@gmail.com

🔗 www.linkedin.com/in/sébastien-henique



