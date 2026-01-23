---
tags:
  - type/variable
  - context/hippique
  - category/cheval
category: Cheval
temperature: 🧊
importance: ⭐⭐⭐
format: integer
unit: km/h
description: Les données de Tracking désignent l'ensemble des mesures géospatiales et cinématiques collectées en temps réel sur le cheval et le driver.
---
# Les Données TRACKING

## 1. Définition 

Les données de Tracking désignent l'ensemble des mesures géospatiales et cinématiques collectées en temps réel sur le cheval et le driver (sulky) durant la course.

Contrairement aux données historiques statiques (ex: *Musique : 1a2a3a*), le tracking offre une résolution temporelle élevée (souvent 10 à 20 Hz, soit 10 à 20 points de données par seconde).

**Les métriques brutes incluent généralement :** 
* **Position GPS :** Coordonnées $(x, y, z)$ sur l'hippodrome.
*  **Vitesse instantanée :** Mesurée en km/h ou m/s. 
* **Accélération/Décélération :** Variations de vitesse. 
* **Fréquence de la foulée (Cadence) :** Crucial pour le trot. 
* **Longueur de la foulée :** Distance parcourue par cycle de mouvement.


## 2. Usage Algorithmique (Feature Engineering)

Pour un algorithme de prédiction, les données brutes sont trop bruitées. Il faut créer des **features** dérivées.
## A. Analyse de la Performance Physique 
* **Distribution de l'énergie :** Calcul de la dépense énergétique sur les différentes sections du parcours (départ, plaine, montée, tournant final). 
* **Vitesse de pointe vs Vitesse moyenne :** Capacité du cheval à produire une accélération violente ("le jump") vs sa capacité à maintenir un train élevé (cheval "dur"). 
* **Détection de fatigue :** Analyse de la courbe de décélération dans les 200 derniers mètres. 
	* *Formule potentielle :* $$Decay = \frac{v_{max} - v_{final}}{t_{finish} - t_{max}}$$
### B. Analyse Tactique (Spécifique au Trot) 
* **L'Effet de Traînée (Drafting) :** Quantifier combien de temps le cheval a passé "dans le dos" d'un autre (abri du vent). Un cheval qui a couru "caché" a souvent une meilleure pointe de vitesse finale. 
* **Trajectoire et Distance Réelle :** Un cheval courant en 3ème épaisseur (à l'extérieur) parcourt plus de distance. 
	* *Feature :* $$Ratio_{dist} = \frac{Distance_{réelle}}{Distance_{officielle}}$$
	* Si $Ratio_{dist} > 1.05$, le cheval a eu un parcours difficile.

### C. Analyse de l'Allure (Risque de Disqualification - DAI) 
Le trot impose une allure spécifique. Le tracking peut aider à prédire le risque de rupture (galop). 
* **Variance de la cadence :** Une irrégularité soudaine dans la fréquence ou la longueur de la foulée précède souvent la faute.
