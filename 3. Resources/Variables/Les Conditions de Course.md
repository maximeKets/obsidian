---
tags:
  - type/variable
  - context/hippique
  - category/cheval
format: integer
unit: km/h
importance: high
---
## 1. Définition
Les Conditions de Course définissent les règles d'éligibilité et les handicaps d'une épreuve spécifique. Elles sont rédigées par la société mère (LeTrot) et dictent qui a le droit de courir.

**Les variables clés au Trot :**
* **Le Plafond des Gains :** "Pour chevaux n'ayant pas gagné 100.000 €". C'est la limite supérieure de la classe.
* **Le Recul (Handicap de distance) :** "Recul de 25m à 50.000 €". Les chevaux les plus riches doivent parcourir plus de distance.
* **Le Mode de Départ :**
    * *Autostart :* Départ lancé derrière une voiture (vitesse pure, numéros 1 à 9 avantagés).
    * *Volte :* Départ viré (tactique, risque de faux départ).
* **L'Ouverture (Européenne/Internationale) :** La course est-elle ouverte aux étrangers ? (Souvent sous-classés aux gains par rapport à leur niveau réel).



## 2. Usage Algorithmique (Feature Engineering)

L'objectif est de quantifier la "qualité de l'engagement" pour chaque partant.

### A. Le "Bel Engagement" (Ratio au Plafond)
Au trot, on vise l'engagement "au plafond des gains". Un cheval ayant 99.000€ de gains dans une course fermée à 100.000€ est théoriquement le meilleur du lot (sur le papier).
* *Feature :* **Quality_Engagement_Ratio**
    * $$QER = \frac{\text{Gains du Cheval}}{\text{Plafond de la Course}}$$
    * *Interprétation :* Plus $QER$ est proche de 1.0, meilleur est l'engagement. Si $QER < 0.5$, le cheval monte de catégorie (tâche difficile).

### B. Impact du Recul (Le rendement de distance)
Rendre 25 mètres est une tâche lourde, surtout sur les petites pistes ou les courtes distances.
* *Feature :* **Distance_Penalty_Weight**
    * Il ne faut pas juste utiliser une variable binaire (0 ou 25m). Il faut la pondérer par la distance totale.
    * $$Impact = \frac{\text{Handicap (25m)}}{\text{Distance Totale}}$$
    * *Nuance :* Sur 2100m, 25m est énorme. Sur 4100m (Marathon), c'est négligeable.

### C. Le Biais du Numéro (Autostart)
Si la condition est "Départ à l'Autostart", le numéro de place derrière la voiture est une condition imposée critique.
* **Première ligne (1 à 9) :** Avantage théorique.
* **Seconde ligne (10 à 18) :** Désavantage (doivent subir la course).
* *Feature :* **Start_Position_Tier**.
    * Le numéro 1 (Corde) peut être un piège (enfermé). Les numéros 4, 5, 6 sont souvent statistiquement les meilleurs.

### D. Le Facteur "Déferrage" autorisé
Parfois, les conditions interdisent le déferrage (courses de jeunes ou apprentis).
* *Check algorithmique :* Si la condition interdit le D4 (Déferré des 4 pieds), exclure les stats "Record D4" du cheval et utiliser ses stats "Ferré".


## 4. Sources et Références

* **Règlementation :**
    * *Code des Courses au Trot (SECF) :* Pour comprendre les subtilités des priorités de participation (élimination des moins riches).
* **Concepts Stratégiques :**
    * *Le "Lag" des chevaux étrangers :* Les chevaux italiens ou suédois ont souvent moins de gains car les allocations sont plus faibles chez eux, mais ils ont un "moteur" supérieur aux chevaux français du même niveau de gains. L'algorithme doit appliquer un **coefficient multiplicateur** aux gains étrangers pour comparer ce qui est comparable.
* **Articles Connexes :**
    * [[Stratégies de l'Autostart]] (À créer)
    * [[Gains et Handicaps Étrangers]] (Comment normaliser les devises et niveaux)